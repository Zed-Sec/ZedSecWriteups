# Welcome to the Kusto Detective Agency - Season 2!

Welcomes back, this is going to be my write-up series for the second season of the Kusto Detective Agency.

### What is Kusto Detective Agency?

So, Kusto Detective Agency is a set of challenges and puzzles that need to be solved using Kusto Query Language (KQL). It's basically a language for querying sets of data. The main area that I use this is when querying Microsoft Sentinel logs. But we won't be using Sentinel or a Log Analytics Workspace for these challenges, we'll be using Azure Data Explorer.  This is the second season of Kusto Detective agency and I had a lot of fun with the first one.&#x20;

This season consists of the intro challenge on this page and another challenge will be released every week or so until we've got access to all 10. Starting on the next case, case 1, all write-ups will be accompanied by video walkthroughs too. If you've not played before, feel free to checkout season 1 and take a look at my walkthroughs for that season if you get stuck.

### Getting Started

To start, you're going to want to head over to [https://detective.kusto.io/](https://detective.kusto.io/) and you'll be met with some basic instructions for getting started. Follow the instructions to:

* Create a free Kusto cluster which will be used throughout the tasks.
* Copy the Cluster URI, this will be needed later in this task.
* Paste the ingestion script into the query editor and run it to ingest the data.

### Changes from Season 1

With the first season you could get 3 hints for each case, that features remains. There is a new way to get help with season 2 though. There's a button **Train me for the case** which teaches you some of the commands you'll need to utilise to solve the case.

### What is the total bills amount in April?

For this case we've got a list of bounty programs and the detectives that solved them, we need to find the detective that earned the most money. The main thing to bear in mind in this one is that only the first detective to solve the case gets the bounty, meaning we're going to need to find the first person to solve each case and then add up all of the bounties for each detective.

First thing I did was found the cost of each bounty:

```kusto
DetectiveCases
// Find the bounty for each case
| where EventType == 'CaseOpened'
| extend Bounty = toreal(Properties.Bounty)
| distinct CaseId, Bounty
```

The first issue I spotted was that you only find out the bounty on the **CaseOpened** EventType and not the **CaseClosed** EventType. Only the **CaseClosed** types are actually associated with the detectives and their retrospective IDs.

The final solution I came up with was:

```kusto
DetectiveCases
// Find the bounty for each case
| where EventType == 'CaseOpened'
| extend Bounty = toreal(Properties.Bounty)
| distinct CaseId, Bounty
| join kind=inner 
    (
    DetectiveCases
    | where EventType == "CaseSolved"
    //Find the first solve for each case
    | summarize arg_min(Timestamp, DetectiveId) by CaseId
    ) on CaseId
    //Sum the total for each detective
    | summarize sum(Bounty) by DetectiveId
    //Grab the top person
    | top 1 by sum_Bounty
```

The solution is commented but I'll break it down a little bit. First we start by getting the bounty for each distinct ID and bounty. That data is joined back into the Detective case table but this time looking for the **CaseSolved** EventType. Then **arg\_min** is used to find the first timestamp and detective ID for each case.

So now we have the first detective who solved each case and the bounty associated with them. Then we throw a sum of the **Bounty** column and grab the top 1 person so we can see who earned the most.

That's it for the intro case!&#x20;
