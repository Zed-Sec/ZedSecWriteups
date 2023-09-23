# Copy of Case 10 - It's a sEnd game

### Video Walkthrough

{% embed url="https://youtu.be/-4TJXeN3XN8" %}
Kusto Detective Agency - Season 2 - Case 10 sEnd game - Video Walkthrough
{% endembed %}

### Intro

Kusto Detective Agency - Season 2 - Case 10 - It's a sEnd game

This week has us shutting down a rogue virus and putting and end to Kuanda!

### Walkthrough

First I started by filtering through all the noise to find the logs that are lost in a sea of logs. This unveils a log called "Sending an encrypted message"

```kusto
KuandaLogs
| where Message !has "User entered the system"
| where Message !has "Captured user encryption token"
| where Message !has "encryption tokens are disposed"
| where Message !has "completed: user encryption token for this operation is disposed."
```

The main part of the KQL solution to this involves decrypting the messages. Messy, and no comments, naughty naughty. The most important part of this is the knowledge that when decrypting, the encoded message is going to be passed into the **Dekrypt** function. The key for this comes from concatenating the last three active keys for each user. I do this using the **Prev** function to add up the last three tokens to form the key. Once this is done we'll have a list of decrypted messages.

```kusto
let encryptedMessageUsers =
KuandaLogs
| where Message has "Sending an encrypted message"
| summarize by DetectiveId;
KuandaLogs
| join kind= inner encryptedMessageUsers on DetectiveId
// | where DetectiveId == 'kvc3fcd5cadf176592a67e'
| partition hint.strategy=native by DetectiveId
(
order by Timestamp asc
| scan with_match_id = id declare(StartTime:datetime, EndTime:datetime, Message: string) with (
step start output=none:
Message has 'User entered the system' or Message has 'User session reset' => StartTime = Timestamp;
step collectTokens output=all:
Timestamp > start.StartTime and Message has 'Captured user encryption token' or Message has 'user encryption token for this operation is disposed';
step completed output=last:
Message has 'Sending an encrypted message'
and (Timestamp > start.StartTime) =>
StartTime = start.StartTime, EndTime = Timestamp;
)
| extend id = strcat(id,'--', DetectiveId)
| order by id asc, Timestamp asc
)
| parse Message with * "Captured user encryption token: '" Token "'."
| parse Message with "Sending an encrypted message, will use Dekrypt(@'" Encoded "'," *
| where Message !has "disposed"
| extend RowNumber = row_number()
| extend PrevRowNumber1 = prev(Token, 1)
| extend PrevRowNumber2 = prev(Token, 2)
| extend PrevRowNumber3 = prev(Token, 3)
| extend ConcatenatedColumns = strcat(PrevRowNumber3, PrevRowNumber2, PrevRowNumber1)
| where Message has "Sending"
| project Key = tostring(ConcatenatedColumns), Message = tostring(Encoded)
| invoke Dekrypt()
| project Result
```

Now that you've got all the messages a bit of digging reveals a little bug they need to patch:

```
[2023-09-10T02:12:30.0000000Z] TODO [BUGBUG]: Validate: bitset_count_ones(hash_many('kvc178c8b4935bed382529', tostring($user_answer))) < 54! Leaving as-is for now, the chance it will actually happen is very low. (O boy, these non-AMD processors are literally melting down on invalid instruction sets!)
```

So we need to pass in the DetectiveID and then a key. I wrote a handy piece of KQL to pass in the tokens from earlier as the key and then hash it, then do a bit count on it, but that's not the solution :(

```kusto
let encryptedMessageUsers =
KuandaLogs
| where Message has "Sending an encrypted message"
| summarize by DetectiveId;
KuandaLogs
| parse Message with * "). Captured user encryption token: '" token "'." 
| parse Message with * "Operation id=" id " " Status " "*
| where DetectiveId in (encryptedMessageUsers)
// | where DetectiveId == "kvc178c8b4935bed382529"
// | where DetectiveId  == "kvc2f916b75d21076bc100"
| where token != ""
| order by Timestamp
| extend test = bitset_count_ones(hash_many(DetectiveId, tostring(token)))
| summarize by test
```

Someone in the community told me something interesting though, it's our own Kusto ID, which can be extracted from your Azure Data Explorer by going to **My cluster** this value changes for everybody. The key is a number between 0 and 200000000, which provides our answer, remember to swap the **{DetectiveID}** for your own ID:

```kusto
range answer from 0 to 200000000 step 1
| extend result = bitset_count_ones(hash_many('{DetectiveID}', tostring(answer)))
| where result > 54
| project answer, result
| limit 1
```

