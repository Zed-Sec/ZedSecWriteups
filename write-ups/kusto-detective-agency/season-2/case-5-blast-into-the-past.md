# Case 5 - Blast into the past

### Video Walkthrough



{% embed url="https://youtu.be/A6QR7owYZOk" %}
Kusto Detective Agency - Season 2 - Case 5 - Blast into the past - Video Walkthrough
{% endembed %}

### Intro

Kusto Detective Agency - Season 2 - Case 5 - Blast into the past

This week we've got the logs for Azure Blob storage. A podcast has uploaded its 900th episdode but had to remove it. A mistake has been made though and the podcast still exists somewhere in the dataset, we have to find the link for it.

### Walkthrough

The main points for this one:

* It's possible when the podcast was deleted, it wasn't fully deleted properly.
* The "Train me for the case" helps solve this one.

```kusto
// Create a variable that returns the host with the most reads but only one delete
let TopPodcast = 
StorageArchiveLogs
| parse EventText with TransactionType " blob transaction: '" BlobURI "'" *
| parse EventText with * "(" Reads:long "reads)" *
| extend Host = tostring(parse_url(BlobURI).Host)
// Count deletes
| summarize Deletes=countif(TransactionType  == 'Delete'), 
// Count Reads
        Reads=sumif(Reads, TransactionType == 'Read') by Host
| where Deletes == 1
| top 1 by Reads;
// Grab a list of URLS now that the host has been narrowed down
let PotentialLinks =
StorageArchiveLogs
| parse EventText with TransactionType " blob transaction: '" BlobURI "' backup is created on " BackupURI
| where TransactionType == "Create"
| extend Host = tostring(parse_url(BlobURI).Host)
| where Host in (TopPodcast)
| summarize by BlobURI;
// Filter the previous results by their delete event on items that were only partially deleted
let PartialDelete =
StorageArchiveLogs
| parse EventText with TransactionType " blob transaction: '" BlobURI "' backup" *
| where TransactionType == "Delete"
| where EventText has "partially"
| where BlobURI in (PotentialLinks)
| summarize by BlobURI;
// Grab the backup link
StorageArchiveLogs
| parse EventText with TransactionType " blob transaction: '" BlobURI "' backup is created on " BackupURI
| where TransactionType == "Create"
| where BlobURI in (PartialDelete)
```

To break this one down. First the first section parses out the Blob URIs adn tehe reads. Aggregate counts are then used to count for deletions and number of people who accessed the blob. A **where** is used to find URIs that have a delete value of 1 and then we grab the most read blob.

The next section of this we grab a list of URIs using the top host extracted from the last section. It's then summarized by the URI.

The third section of this query filters that list of potential links down to their delete events, filtered by blobs that were only partially deleted. This spits out one URI.

The final part of this takes the URI from the **PartialDelete** variable and filters for its **Create** event. The backup URI from this output is the answer we're looking for.
