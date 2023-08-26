# Case 8 - Catchy Run

### Video Walkthrough

{% embed url="https://youtu.be/y30NIyBeIMA" %}
Kusto Detective Agency - Season 2 - Case 7 Mission 'Connect' - Video Walkthrough
{% endembed %}

### Intro

Kusto Detective Agency - Season 2 - Case 8 - Catchy Run

This week has us analysing runner information in Barcelona

### Walkthrough

The main points for this one:

* The first part of the task is a magic cube. Each row of the cube has to add up to a specific number. In this case, 33, you can find this by adding up the diagonal values, then use this information to fill in the missing numbers
* Krypto runs 3-4 times a week.
* Each run is 8-12KMs each.
* He's run 10KM at least once.
* He always runs with two bodyguards.
* He stops for shakes after some of his runs.

```kusto
// Secret Message intercepted    
let city_code=datatable(c1:long,c2:long,c3:long,c4:long)
[1, 14, 14, 4,
11, 7, 6, 9,
8, 10, 10, 5,
13, 2, 3, 15];    
print Key=SecretCodeToKey(city_code), Message=
@'0SOHpSdTgidfqXFOYeIOjktOjXFcjktPjwzHgSABgsctZknJZKfEjBAygipOgS\\pBNEjknCVedTpSdyjk7EZKFHVSOa8i7E8SOCZedfgSOTgSA'
@'tYPFaYB4TjXFHZ[\OVkNT17mzgSv\VPFHjknHjKFnVedygSvuVBvOYBxDgS4HgiztVkAyYyFujPFupwgEpiztjKFmVaIOVaImV[nHgS\\pBNEYB'
@'d\Z[\OjXFb8SNEjk4yYyFujPFb8SNEKbIFqEbo7adbgSjOZwgEVBAbqXFc6KFDVeO\VXFCV[tyZkIOYyfEjBAygipOgiv5Zk2DgSnupXFeZwjOY'
@'PFBYBAcgSAtYPFfZwI5gKFzjPF\VaOb8SOTjyfEp[NEY[\\VSfE8knbjknH8kjngSAtYPFOjBjuYaIHgidTpSODgiI5jKFqIssEZeztVkzDjwME'
@'ZBdTjk4b8XFupwgEjBdOpXxvXJJEZ[4TVBAbgiv5ZwzOgiIuVyFcpkv5gS4bgiI58wMEpSOcjKfEZadbgizOYe7EZwvHpwzOjXfEp[NEZwzOgiz'
@'tVBnmVBYEVedygXzHVkAQjKFbjwvbYygDgSzupSEEjBOapwz\pSO[jk2ngS4TjXF2pkObjKFD8wIOYB4DViJT17mN8Sdngiv5Zk2DgSdxYSAHjK'
@'Fb8SNEKbIFzeMEp[d\8[nOYevOYyF\VB7E8SdyZk2JgSObYyFOYSOCgSIup[nBZk2DqEbo17mUVeYDgS2OpXFtYyF\jSIyjwvHgiI5jKFcZwIbj'
@'wgEV[ZEVwJEp[dDVXtPjkOTjyxEKKFtVBIOYavbZknJgiI5Zw7EpS\OYBNE8wMEZKFaYBd\pXFJjk4DgSABgSvtYBOuY[Ob6KFyjkp\YBImVBYE'
@'VwJEY[4BjwInqPrvXJ2OpXFcjKF\YevtYBNE6kAtqXFmpXFeZwMEZk2DgSsEVk4bpSdygSABgSOcYSdCZ[4PVSNEpSOc8knaqPFUVyFJVedPpXF'
@'c6KFCV[nTjkvb8knagSjD8kp5pXFeZwMEZkxEjw\fjwzmjknCjKFujPF\gS2mjBdb8ktOg7bodSAugSz\jXFc6KFDpkpaZkpOgSj\8k2OjXFbVy'
@'FlV[OTgStOgSATgiI58wMEpS\y8k2D8knagSmupwzTjwJ\g15m175vXJztpXFBjk4ygSnupXfEVwJEjazmjknJYyfEVSd\pBOTjyFb8SOTjeMEp'
@'SREZ[\\VBvOgSOHgSnupXFc6KFHpiODjKxEKKF5ZwjOgS4HY[dcZB2OjXF\giIOZkbEV[ZEVSAnZkfEZBAJ6kptZwzJYyfvXap5VyFcVejOgipm'
@'pSEEVkNEVSOQjKFOVidH8wjOgiF5ZknbV[tHqXFOVavtYBOTjyFc6KFmVajmVBvmZBOD8wInqPFFpXF\VaJEj[O[jkxEpSOcjKfEZw7EVSd\Ye7'
@'EpipugSABgiI5jkbEjSOHZezOjwID67boY[\\jSAegStngSd[jwzngStupBNDgSd[jkxEjidy8knagStngSdx8SODZwz\pSOTjyFypknHgiI5YB'
@'Atj[EEpS\OgSvmpiJTg4Iypk2nqXFzgSjOjkfEpknbVedC8S4PVSNTgs4TjXFDjw7EVkNEpSdDVXFnVeND17mb8SOHgSvmpiJE8wMEZKF58kIJj'
@'kxEj[dcgKFzpXFujBjOYaMEZkxEZkztVBI\VBvOgSABgSt\YajOVSAtYyFHYSAbYyFe8SdyjKFuVBNEZ[4TgSOTjidDj[NE8kxEZKFyjkjyjwv5'
@'8knagiv5ZkcOgS4BpSdy17mCV[n2pkdy8knagSsEZazOZwI5pS4Q8knag1sfKyFypkxTgsObgSOHgSsEYSdyjBdCpXFPVSdTjXFujPFc8wvC8SO'
@'OjPF\VB7EYBdlpwjOVB4b8kATqXF\gSIOVSOa8iIBpkfEZ[ATZ[ACpSOuVPFb8S4bgSjtjk2HgStngivbYBdTjeI5qEbo17m0VyfEVwJEjBdDVS'
@'AegizujedOYyfEVSdbgidHgScOjwrEVedygSdnjwMEjBOxjk7EV[xEpS\OgiI\YBpOpXxEKKFe8k2DgizOpBd\VXFcVezOgSIOpS4mViMEZkzup'
@'w7EVedygiFDZknHgSOTgSItjKFb8ktOqPrvXOFyjwF\YBNE6kAtYavOVijOYyFbVyFe8wITjwvHgiI5jKFHYSdCpS4Cpk2\YPFJVepTjB4DVXFu'
@'jPFb8SNEKbIFqXF\YyFejKFyjk2OVaIDjwvHViJEjizmVSfE8knbVyFmpiMEZ[AyjKF\pXFBpk2DgivfjkdJg7bogrboKeznYiIu'
| invoke Dekrypt()
| project Result

let runnerSchema =
Runs
| join kind=leftsemi (
Runs
| summarize count() by RunnerID, bin(Timestamp, 7d)
| where count_ between (3 .. 4)
) on RunnerID /// 3-4 times in week
| join kind=leftsemi (
Runs
| summarize Max = max(Distance) by RunnerID
| join kind=inner (
Runs
| summarize Min = min(Distance) by RunnerID
) on RunnerID
| where Min >= 8 and Max <= 12
) on RunnerID // 8-12km distances
| join kind=leftsemi (
Runs
| summarize max(Distance) by RunnerID
| where max_Distance > 10
| distinct RunnerID
) on RunnerID // Has run 10km at least once
| extend Timestamp = bin(Timestamp, 25s)
| extend key=geo_point_to_s2cell(StartLon, StartLat, 22);
let geolocation = runnerSchema
| summarize count() by Timestamp, key
| sort by count_
| summarize countif(count_ == 2) by key
| top 1 by  countif_
| project key;
runnerSchema
| where key in (geolocation)
| extend Link = strcat('https://www.google.com/maps/@', StartLat, ',', StartLon,',3a,75y,252.01h,89.45t/data=!3m6!1e1!3m4!1s-1P!2e0!7i16384!8i8192')
```
