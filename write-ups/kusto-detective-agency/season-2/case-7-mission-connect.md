# Case 7 - Mission 'Connect'

### Video Walkthrough

{% embed url="https://youtu.be/y30NIyBeIMA" %}
Kusto Detective Agency - Season 2 - Case 7 Mission 'Connect' - Video Walkthrough
{% endembed %}

### Intro

Kusto Detective Agency - Season 2 - Case 7 - Mission 'Connect'

This week has us analysing flight records to find a plane which our suspect jumped from mid-flight and where that plane landed.

### Walkthrough

The main points for this one:

* We've got a table full of airports and another that has the timestamps of where each plane was, including the location during the flight
* The planes would need to be near each other for several minutes for the jump to happen.
* The first plane would need to be at a higher altitude than the second one.

```kusto
// Set the range as 1KM
let s2_precision = 13; 
// List of planes that departed from the airport during the timeframe
let firstPlane =
Airports
| where municipality == 'Doha'
| extend key=geo_point_to_s2cell(lon, lat, s2_precision)
| join kind=inner (
    Flights
    | extend key=geo_point_to_s2cell(lon, lat, s2_precision)
    | where onground // Only consider planes that were on the ground
    | where Timestamp between (datetime(2023-08-11 03:30:00) .. datetime(2023-08-11 05:30:00))
) on key
| where geo_distance_2points(lon, lat, lon1, lat1) < 5000 // Assume a 5km radius is enough
| distinct callsign;
// Find the hashed location of each lat/lon combination during the flight
Flights
| where callsign in (firstPlane)
| where Timestamp > datetime(2023-08-11 05:30:00)
| where onground == "false"
| extend key=geo_point_to_s2cell(lon, lat, s2_precision)
// Join the list of first planes back to the flights table using the ID of the plane and the timestamp
| join kind=inner (
    Flights
    | extend key=geo_point_to_s2cell(lon, lat, s2_precision)
    | where Timestamp > datetime(2023-08-11 05:30:00)
) on key, Timestamp
// Remove duplicate entries, the first plane flagging itself as a match
| where callsign != callsign1
// Calculate the altitude difference between planes
| extend altitudeDifference = geoaltitude - geoaltitude1
// Filter out planes that aren't flying within altitude difference we're looking for.
| where altitudeDifference > 0 and altitudeDifference <1000

Flights
| where callsign == "HFID97"

// Find the final airport
Airports
| extend DistanceInMeters=round(geo_distance_2points(lon, lat, 2.07939861505682, 41.2981453919491))
| summarize arg_min(DistanceInMeters, Name, Type)
```
