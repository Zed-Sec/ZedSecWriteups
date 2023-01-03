# Case 5 - Big Heist

### Intro

Kusto Detective Agency - Case 5 - Big Heist. This is a walkthrough for the final case in the 2022 version of Kusto Detective Agency. There’s a heist that’s going to be happening soon. There’s 4 members.

This time we’ve just got chat logs to look at. There’s a table called ChatLogs with just two columns, timestamps and logs for users, we don’t have the actual messages themselves though. We need to try and find the IPs of the gang members then use the below tool to sneak into their IPs:

[https://sneakinto.z13.web.core.windows.net/](https://sneakinto.z13.web.core.windows.net/)\<ip>

We need to find the exact time and place for the heist.

### Walkthrough

We’re going to start by taking a few samples of the data to see what it actually looks like and how he can start to think about how we’re going to get these naughty boys:

```
ChatLogs
| take 20
```

Looks like there’s a few different messages that we can log based off of:

* User \<user> sent messages to the user \<User>
* User \<user> logged in from IP \<IP>
* User \<user> joined the channel \<channel>
* User \<user> left the channel \<channel>
* User \<user> logged out from the server

And I think that’s all the different ones we have. We basically need to parse these out into different columns.

We’re going to try and find the specific channel that the gang are logging into.

Okay, so we’ve written a query that parses out the user joining messages. Then it does a count by time bins of a minute with 4 users joining in that 1 minute. This gives us an output of two different potential channels:

* cf053de3c7b
* cf1d3ff8443

```
ChatLogs
| parse-where Message with "User '" user "' joined the channel '" channel "'"
| summarize Count = count() by channel, bin(Timestamp, 1m)
| where Count == 4
| distinct channel
```

Now, there’s probably a smarter way to solve this part for the channel, but I couldn’t think of one, I tried dialling in on a shorter time period in the bins but it actually gave me the wrong one. Instead I ran the following two queries which basically just outputs all the distinct users that have joined the channel. One only output 4 users, but the other output way more, meaning that the channel that only ever had 4 people join in its history was probably the channel we were looking for:

```
ChatLogs
| parse-where Message with "User '" user "' joined the channel '" channel "'"
| where channel == "cf053de3c7b"
| distinct user

ChatLogs
| parse-where Message with "User '" user "' joined the channel '" channel "'"
| where channel == "cf1d3ff8443"
| distinct user
```

Now we need to find their IP addresses. I pulled a list of the distinct users with:

```
ChatLogs
| parse-where Message with "User '" user "' joined the channel '" channel "'"
| where channel == "cf053de3c7b"
| distinct user
```

So our list of users is:

* uaf9f4fef17
* u8819ece9b0
* uf034c98df3
* uab8088061c

The following query parses the logon message and pulls out the IP address for your 4 users:

```
ChatLogs
| parse-where Message with "User '" user "' logged in from '" logon_ip "'"
| where user in (
"uab8088061c",
"uaf9f4fef17",
"u8819ece9b0",
"uf034c98df3"
)
| distinct user, logon_ip
```

The IP addresses we need are:

* 236.48.237.42
* 119.10.30.154
* 146.49.19.37
* 194.243.69.176

And the links we need to access their machines are:

* [https://sneakinto.z13.web.core.windows.net/](https://sneakinto.z13.web.core.windows.net/)236.48.237.42
* [https://sneakinto.z13.web.core.windows.net/](https://sneakinto.z13.web.core.windows.net/)119.10.30.154
* [https://sneakinto.z13.web.core.windows.net/](https://sneakinto.z13.web.core.windows.net/)146.49.19.37
* [https://sneakinto.z13.web.core.windows.net/](https://sneakinto.z13.web.core.windows.net/)194.243.69.176

On one of the machines there’s a util.txt file that contains a link to[https://tool.geoimgr.com/](https://tool.geoimgr.com/).

On IP **119.10.30.154** there’s a screenshot of an email that gives us some ideas of the direction we’re going to take for the task. We need to find the date that the picture we’re looking for was taken. But how do we find the picture we’re even looking for?

On **236.48.237.42** there’s a PDF with some pictures on, only one of the pictures on that PDF actually matches the images in the PDF, **image3.** I put the image into a metadata extractor and got:

* 2020-07-09

Next we have to grab the PS text from the start of the task and the key from the end of the last task and use it to decrypt the message in the **util.txt** file:

````
// Handy utils

// 1) Utility to discover secondary messages.
// Usage: ReadMessage(Message, Key)
let ReadMessage = (Message:string, Key:string) 
{
    let m = Message; let K = Key; let l = toscalar(print s = split(split(K,':')[1], ',') | mv-expand s | summarize make_list(tolong(s)));
    let ma = (i1:long, i2:long) { make_string(repeat(tolong(l[i1])-tolong(l[i2]), 1))}; 
    let ms = (d:dynamic, s:long, e:long) { make_string(array_slice(d, s, e)) };   
    let mc = m has '...';
    print s=split(split(replace_regex(m, @'[\s\?]+', ' '),substring(K,9,3))[1], ' ')
    | mv-expand with_itemindex=r s to typeof(string) | serialize 
    | where r in (l)
    | extend s = iif(r-1 == prev(r), replace_string(strcat(prev(s), s),'o','ou'), s)
    | where (r+1 != next(r))
    | summarize s=strcat_array(make_list(s), iff(mc, '+%2B', ' '))
    | extend k = series_subtract(series_add(to_utf8(K), l), repeat(23, 10))
    | project result=iif(mc, strcat(ms(k,0,3), ma(8,2), ms(k,4,6), ms(l,8,8), ms(k,7,7), ma(8,0), s), s)
};
ReadMessage(
```
PS:
Feeling uncomfortable and wondering about an elephant in the room: why would I help you?
Nothing escapes you, ha?
Let’s put it this way: we live in a circus full of competition. I can use some of your help, and nothing breaks if you use mine... You see, everything is about symbiosis.
Anyway, what do you have to lose? Look on an illustrated past, fast forward N days and realize the future is here.
)
```,
Key="wytaPUJM!PS:2,7,17,29,42,49,58,59,63");
````

This will give us the **Bing** link of:

* [https://www.bing.com/search?q=uncomfortable+%2Belephant+%2Bescapes+%2Bcircus+%2Bbreaks+%2Beverything+%2Btoulouse+%2Billustrated\&toWww=1\&redig=B015D33DE3A345348B2BF543B6260255](https://www.bing.com/search?q=uncomfortable+%2Belephant+%2Bescapes+%2Bcircus+%2Bbreaks+%2Beverything+%2Btoulouse+%2Billustrated\&toWww=1\&redig=B015D33DE3A345348B2BF543B6260255)

It basically ends up searching for an uncomfortable elephant breaking everything. This tells us this happened in **1891**. So now we’ve got all the info we need:

```
print make_datetime(2020, 07, 09) + (1891d % 1000d);
```

Which gives us the date of the heist:

* 2022-12-17

Finally, the image that we grabbed the created date from can be plugged into [https://tool.geoimgr.com/](https://tool.geoimgr.com/) and this will give us the lat, and lon of them. Which gives us our complete answer:

* 2022-12-17
* 3.38010413333333
* 58.9688665166667

That one was hard.
