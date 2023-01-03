# Case 3 - Bank robbery

### Intro

Kusto Detective Agency - Case 3 - Bank robbery. For this case we need to track down the suspects of a bank robbery. We've got a data set of cameras recording all the vehicles and their movements from 08:00AM till 11:00AM. We need to find the people who did it.

### Key Information

* There's been a bank robbery
* The bank is located at 157th ave / 148th street
* We need to locate the gang
* There is a timeframe of events:
  * 08:17 The gang arrived at the bank
  * 08:31 They pack up and get out
  * 08:40 The men were seen getting into three different cars and driving away
* The data was only captured on moving vehicles
* We know the cars weren't moving during the robbery which eliminates a lot of cars
* The gang split up into three groups but they'll need to meet up to divide the loot

### Tables

* Traffic
  * Timestamp
  * VIN
  * Ave
  * Street

### Walkthrough

First, I'm going to try and get a list of all the cars that were recorded during the robbery, then this can be used to exclude them later.

```
Traffic
| where Timestamp between ( datetime(2022-10-16 08:17:00.000) .. datetime(2022-10-16 08:40:00.000) )
```

The final query I came to is below. Basically we start by filtering by the street and ave that the bank is on during the timestamps of when the robbery took place. We could maybe buffer it a little bit to a wider search by a minute or two on each side but it turns out I didn't need to. The CCTV only catches moving cars.

Then we filter by VIN and join them back into the table. We then use the **arg\_max** operator to find the max timestamps, filtering by VIN.

We then throw in a count because we only want to find the 3 cars that have met eachother so we do a more than or equals to and that sorts us right out:

```
Traffic
| where Ave == 157 and Street == 148
| where Timestamp between ( datetime(2022-10-16 08:17:00.000) .. datetime(2022-10-16 08:40:00.000) )
| distinct VIN
| join Traffic on VIN
| where Timestamp > datetime(2022-10-16 08:40:00.000)
| summarize arg_max(Timestamp, *) by VIN
| summarize Count=count() by Ave, Street
| where Count >= 3
```
