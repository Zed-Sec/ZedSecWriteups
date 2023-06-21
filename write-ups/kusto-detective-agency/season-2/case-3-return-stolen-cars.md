# Case 3 - Return Stolen Cars!

### Video Walkthrough

{% embed url="https://youtu.be/cs-OrCDiE3Y" %}
Kusto Detective Agency Season 2 - Case 3 Walkthrough
{% endembed %}

### Intro

Kusto Detective Agency - Season 2 - Case 3 - Return Stolen Cars

For this one somebody is stealing cars. We've got a list of 20 stolen cars and another table that shows the traffic logs, this contains timestamps of when each car was spotted on which street. This isn't a very clever way to solve this one so feel free to take the piss out of me, I did win a prize for doing this one so quick though!

### Walkthrough

The main things for this one:

* The plates are being switched over, it takes a few minutes on average to switch the plates over.
* It's possible there's a few locations the thieves keep going to switch the plates over.
* Fake plates are being used for the switch, so when a car is switched over, a brand new plate will appear on that street a few minutes later.
* All cars are being taken to one place.

This query shows us the last place each car was being kept:

```kusto
CarsTraffic 
| where VIN in (StolenCars)
| summarize Last=arg_max(Timestamp, VIN, Ave, Street) by VIN
| summarize count() by Ave, Street
```

This gives us two places:

* Ave 122, Street 251
* Ave 223, Street 86

We now know where the cars are being switched, so let's build a query based on that information.

This time I grabbed the timestamp from the first car that showed up on my list **IN149152E**, the timestamp was **2023-06-10T14:10:00Z.** I looked for cars that showed up on the timestamps 2 minutes after that on the street where the car was last seen Ave == 223 and Street == 86.

```kusto
CarsTraffic
| where Timestamp == datetime(2023-06-10T14:12:00Z) and Ave == 223 and Street == 86
```

Then I grabbed the three cars that showed up in the results there and looked for the street they were last seen on. The VIN **IM722362S** turned out to be the answer. A very lucky way to solve this one and definitely not my finest solve...

```kusto
CarsTraffic
| where VIN in ('IM722362S','KI607436W','MU142329U')
| summarize Last=arg_max(Timestamp, VIN, Ave, Street) by VIN
```

But let's try to come up with something a tiny little bit more concrete because my "solution" is a bit cheeky and not actually in the spirit of the competition.

```kusto
let FakePlates =
CarsTraffic
| where (Ave == 223 and Street == 86) or (Ave == 122 and Street == 251)
| summarize arg_min(Timestamp, VIN, Ave, Street) by VIN;
CarsTraffic
| where VIN in (FakePlates)
| summarize Last=arg_max(Timestamp, VIN, Ave, Street) by VIN
| summarize count(VIN) by Ave, Street
```

And that's us for another week. These are getting tougher for me, not sure if I'm going to make it though all of the challenges at this rate...
