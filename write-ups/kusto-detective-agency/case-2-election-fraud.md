# Case 2 - Election Fraud?

### Intro

Kusto Detective Agency - Case 2 - Election Fraud? The difficulty continues to ramp up in this one. This time there's 4 candidates in the local election. The polls expected a much different outcome than the one we got. It looks like Poppy the Goldfish got the most votes, which doesn't seem right. So, we've been asked to investigate it.

### Key Information

* 5 million people voted in the election
* Four candidates made it to the final round:
  * Kastor the Elephant
  * Gaul the Octopus
  * William the Tortoise
  * Poppy the Goldfish
* The polls predicted a close call between Kator and Gaul, but the fish got a whopping 51.7% of all the votes.
* We need to prove if the fraud happened and the percentage of votes each candidate actually got.
* We have access to the IP of the voting machine, anonymised ID, vote, date-time, and the vote counting function.

### Tables

* Votes
  * Timestamp
  * vote
  * via\_ip
  * voter\_hash\_id

### Walkthrough

So, we basically need to add up the votes and find the percentage of each candidate. Teh vote counting query used it:

```
Votes
| summarize Count=count() by vote
| as hint.materialized=true T
| extend Total = toscalar(T | summarize sum(Count))
| project vote, Percentage = round(Count*100.0 / Total, 1), Count
| order by Count
```

We can see with the above query that Poppy definitely has the most votes. I wanted to throw the votes per candidates into time buckets. this can be done using the **bin** operator. I started by chucking all the timestamps into 1 hour buckets, then down to 15 minutes, 1 minute, 30 seconds, 15 seconds, and finally, 1 second until I basically had no candidates getting more than 1 vote per second, except Poppy, who had way more per second:

```
Votes
| summarize Count=count() by bin(Timestamp, 1s), via_ip, vote
```

Using the above query we can see that something dodgy is definitely afoot. So the final query I came to basically uses the **iff** conditon which is similar to an if statement. Basically if the count for that column is more than 1, it invalidates it and sets it to 0. Since we know that the only person getting more than 1 vote per seconds per IP is Poppy, we know that this is cheeting and therefore can be chucked in the bin, the actual bin, not the data bucket bin. The second part of the query re-runs the vote counting from our initial query and outputs the actual accurate voting.

<pre><code><strong>Votes
</strong>| summarize Count=count() by bin(Timestamp, 1s), via_ip, vote
| extend Count = iff(Count > 1, 0, Count)
| summarize Count=sum(Count) by vote
| as hint.materialized=true T
| extend Total = toscalar(T | summarize sum(Count))
| project vote, Percentage = round(Count*100.0 / Total, 1), Count
| order by Count
</code></pre>

That's it for case 2!
