# Case 9 - Network Hunch

### Video Walkthrough

{% embed url="https://youtu.be/HOBKuS9qJyY" %}
Kusto Detective Agency - Season 2 - Case 9 Network Hunch - Video Walkthrough
{% endembed %}

### Intro

Kusto Detective Agency - Season 2 - Case 9 - Network Hunch

This week has us digging through network traffic looking for a breached admin machine.

### Walkthrough

The main points for this one:

* We're looking for machines that have confirmed vulnerabilities.
* We're looking for an admin machine.
* This one focuses on the **make-graph** and **graph-match** operators which are quite new.

```kusto
// Find machines with vulnerabilitites
let VulnMachines=
MachineLogs
| parse-where Message with Role " periodic scan completed, " TotalVuln:int " critical vulnerabilities were found."
| where TotalVuln > 0
| summarize by Role, Machine;
// Find incoming requests
let IncomingRequest=
MachineLogs
| where EventType == "IncomingRequest"
| parse-where Message with "Got request with TaskID=" CurrentTaskID " from " PreviousMachine
| extend CurrentMachine=Machine
// Join back in adding in the roles on vulnerable machines
| join kind=inner VulnMachines on Machine
| project Timestamp, CurrentMachine, PreviousMachine, CurrentTaskID, Role;
let TaskSpawns=
MachineLogs
| where EventType == "SpawnTask"
| extend CurrentMachine=Machine
| where CurrentMachine in ((VulnMachines | project Machine))
| parse-where Message with "TaskID=" CurrentTaskID ": spawning a sub-task with TaskID=" NextTaskID " on " NextMachine;
TaskSpawns
| make-graph CurrentTaskID --> NextTaskID with IncomingRequest on CurrentTaskID
| graph-match (start)-[relation*1..10]->(end)
    where start.Role == "Gateway" and end.Role == "Admin"
    project StartMachine=start.CurrentMachine, EndMachine=end.CurrentMachine, MachinesPath=relation.CurrentMachine
```
