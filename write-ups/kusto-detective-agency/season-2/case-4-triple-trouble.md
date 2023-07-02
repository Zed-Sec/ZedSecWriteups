# Case 4 - Triple Trouble!

### Video Walkthrough

{% embed url="https://youtu.be/uHhJLfPjI6w" %}
Kusto Detective Agency - Season 2 - Case 4 - Triple Trouble - Video Walkthrough
{% endembed %}

## Intro

Kusto Detective Agency - Season 2 - Case 4 - Triple Trouble

This week Gaia Budskott, the mayor of Digitown has been accused of leaking a bunch of documents from the network at the Digitown municipality office. We've been given network traffic and a table of IP info and we have to find the person who has been stealing the data.

### Walkthrough

The main points for this one:

* They might not be using the same IP for leaking the documents.
* The dataset is large, very large. Most of our usual queries that would be used for this will hit the data limits on Data Explorer on the free cluster.&#x20;

```kusto
NetworkMetrics
// Sum Bytes sent by 1 day timestamp bins and ClientIP
| summarize ActualUsage = sum(BytesSent) by Bin = bin(Timestamp, 1d), ClientIP
// Use ipv4_lookup operator to compare the IP information with the CIDR ranges in the IPInfo table
| evaluate ipv4_lookup(IpInfo, ClientIP, IpCidr)
// Tidy up so that we only have the information we need
| summarize by ActualUsage, Info, Bin
// Add group each ActualUsage and Bin into a series by Company name
| make-series ActualUsage = sum(ActualUsage) default = 0 on Bin step 1d by Info
// Detects anomalies in the series
| extend series_decompose_anomalies(ActualUsage, 24*7)
// Breaks the AD_score into separate rows so we can filter on them
| mv-expand series_decompose_anomalies_ActualUsage_ad_score
// Filter where teh AD Score is more than 5
| where series_decompose_anomalies_ActualUsage_ad_score >=4
```

To break this one down. First I did a **Sum** on the Bytes sent across the network, this sum was then put into 1 day bins by **timestamp** and **ClientIP**.

**ipv4\_lookup** allows us to look pass our IP addresses from **ClientIP** and can then show which CIDR range they belong to and which company uses that CIDR range. A quick summarize was then done to clean up the columns we had so-far.

**make-series** is used to group the **ActualUsage** into a series by **Bin** and **Info.**

**series\_decompose\_anomalies** is used to detect anomalies in our data. It assigns a baseline and then detects outliers and assigns them a score depending on how much of an outlier it is.

The few rows **mv-expand** breaks the **AD\_Score** out from the series into it's own rows by company. the final part of the query filters by **AD\_Score** where the socre is more than 4. This returns a bunch of outliers but most seem to be around the 4 range. One company has a score of 58 though, way higher than the others. That's our culprit.
