# Case 1 - To bill or not to bill?

### Video Walkthrough

{% embed url="https://youtu.be/FPhCqbTLSCA" %}
Kusto Detective Agency Season 2 - Case 1 Walkthrough
{% endembed %}

### Intro

Kusto Detective Agency - Season 2 - Case 1 - To bill or not to bill?

In this case we work for the gas and electric board. Somehow customers bills have doubled out of nowhere, with no changes in the customers consumption, how odd. The cities billing system works on SQL, which is automatically translated by KQL, but we'll also need to optimise it a little bit. So, let's get right into it.

### Walkthrough

The initial SQL query used is below:

```kusto
SELECT SUM(Consumed * Cost) AS TotalCost
FROM Costs
JOIN Consumption ON Costs.MeterType = Consumption.MeterType
```

Pasting it into ADX will give us the answer but it's the wrong answer, let's start by using the **EXPLAIN** operator to translate the SQL to KQL:

```kusto
EXPLAIN
SELECT SUM(Consumed * Cost) AS TotalCost 
FROM Costs 
JOIN Consumption ON Costs.MeterType = Consumption.MeterType 
```

This gives us a KQL output, but an optimised version of that query would be:

```kusto
Consumption  
| summarize TotalConsumed = sum(Consumed) by MeterType  
| lookup Costs on MeterType  
| extend TotalCost = TotalConsumed*Cost  
| summarize sum(TotalCost) 
```

Now we can actually start digging into the data. Looking at one of the hints it suggests that data is sometimes re-transmitted, maybe that's what's happening and is causing people to be double billed? Another hint says that some data needs to be potentially discarded. So the pricing is clearly right in the **Costs** table that is being used to lookup the prices, but because there's extra reporting, people are being charged extra.

Using the below query we can see how far apart the timestamps are, it shows that each timestamp is a day apart:

```kusto
Consumption
| summarize by Timestamp
```

We can run a count to see how many readings are being taken per day. With the below query, we can see that some houses are being billed more than the normal amount. We should be seeing 2 meter readings, per house, per day. 1 for electricity and one for water.

```kusto
Consumption
| summarize count(MeterType) by HouseholdId, Timestamp
| where count_MeterType >2
```

The above shows that there are over 40,000 records that have recored more than twice, well that's our issue I bet. The final query below basically takes the larger of each type of bill, per house, per day. This leaves us with only 2 consumption records per day for each house. I took the larger of the bills as opposed to the lower mainly because I had to start somewhere, I'm sure if you dig into the data you can come up with a better reason for this, but, it worked.

Then we lookup the costs table to get the amount to bill the consumption by and do a sum to come up with the correct costs.

```kusto
Consumption
| summarize max(Consumed) by MeterType,HouseholdId,Timestamp
| lookup Costs on MeterType  
| summarize sum(max_Consumed * Cost) 
```

That's it for this one.&#x20;
