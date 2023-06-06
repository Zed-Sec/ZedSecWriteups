# Case 2 - Catch the Phishermen!

### Video Walkthrough

{% embed url="https://www.youtube.com/watch?t=&v=9kJKdbeRFXI" %}
Kusto Detective Agency Season 2 - Case 2 Walkthrough
{% endembed %}

### Intro

Kusto Detective Agency - Season 2 - Case 2 - Catch the Phishermen!

This time it looks like somebody is phishing the people of the town. We've got a table called **PhoneCalls** which contains the phone logs. We need to dive into the logs and find the origin number of the person who is scamming.

### Walkthrough

There was a few assumptions I made about this one after reading through the scenario and taking a look at the data:

* We're going to assume that the person doing the phishing hides their number.
* The prospective targets probably hang up on the scammer more times than not.
* The scammer will be initiating the calls.

The first path I went down was to check the properties field, convert it to string instead of a dynamic object and run a summarise so we could see all the different disconnect reasons.

```kusto
PhoneCalls
| where EventType == "Disconnect"
| summarize by tostring(Properties)
| take 100
```

After running it though we see that there's only two options:

1. Disconnected by origin
2. Disconnected by destination

The final query I came up with was:

```kusto
PhoneCalls 
| extend Origin=tostring(Properties.Origin), Destination=tostring(Properties.Destination), Hidden=tobool(Properties.IsHidden) 
| where EventType == 'Connect' and Hidden == "true"
| join kind=inner 
   (
   PhoneCalls
   | extend Disconnector=tostring(Properties.DisconnectedBy)
   | where EventType == "Disconnect" and Disconnector == "Destination"
   ) on CallConnectionId
| summarize Distinct=dcount(Destination) by Origin
| top 1 by Distinct
```

The above query start by using the **Extend** operator to create some new columns. It breaks the **Properties** column into three different ones that summarise the origin, destination and whether the number was hidden.

Then we filter by connect events where the caller was hiding their numbers. Next, we do an inner join back into the PhoneCalls table by CallConnectionID. Using **tostring** again we break properties out to find for each call whether the caller or the destination disconnected the call. The **where** operator is then used to filter by calls where the recipient of the call hung up.

Finally, we grab a distinct count by origin number then filter by the top one. This gives us our number.
