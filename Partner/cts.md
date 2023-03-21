# Assignment And Pax Count Data Spec

## Overview
Vehicles will have CalAmps.  
Passio will build routes and stops and trips in Navigator.  

CTS will ingest GTFS from Navigator.  
CTS will assign vehicles to GTFS Blocks in TripMaster.  

Passio needs to show the vehicle's location, route, ETAs, etc on Passio GO.  
Passio needs to generate NTD Report.  
Passio cannot depend solely on vMDT because of many deviations the vehicle will do.  



We will use one data object that will be sent from ParaScope on driver pick up and perform events.




## Block Assignment lifecycle

| Event | Block Assignment | Service Status | Details |
| --- | --- | --- | --- |
| Driver pre-trip | None | Deadhead (OOS:1) | |
| Driver on way to first stop | Block Assignment | Deadhead (OOS:1) | |
| Driver at first stop | Block Assigment | Revenue (OOS:0) | |
| Driver doing work | Block Assignment | Revenue (OOS:0) | Will include `paxLoad`, `paxCount`, `paxOnOff` <br> `stopId` might be null or unknown due to vehicle performing deviated stop. If so, we will use last known stop |
| Driver getting ready to leave last stop | Block Assignment | Deadhead (OOS:1) | |
| Driver parked at yard ready to start post-trip | None | Deadhead (OOS:1) | We can also get OOS from yard geofence entry |

---

## Assignment Data Object

| Field | Description | Required | Expected Values + Details |
| --- | --- | --- | --- |
| agencyId | ID of agency | Yes | Should match `agency_id` in agency.txt | 2868 |
| vehicleId | ID of vehicle | Yes | CTS Internal ID. Will match up with our external ID |
| vehicleVIN | VIN of vehicle | No | For extra level of validation when ID is not unique due to multi-tenent db structure |
| driverName | First and last name of driver | Yes |  "Nick Hexum" |
| blockId | ID of GTFS Block. Should match `block_id` in trips.txt | Yes | 44678|
| stopId | ID of last stop. Should match `stop_id` in stops.txt | No | If not included, we will use vMDT or last known stop.<br>We will need to verify that stopId exists on tripId (when CTS is performing Deviated stop).<br>If not, we will ignore stopId and use last known stopId |
| tripId | ID of current trip. Should match `trip_id` in trips.txt | Yes | 32889 | 
| routeId | ID of current route. Should match `route_id` in routes.text | Yes | 88567 |
| outOfService | If the vehicle is revenue or deadhead | Yes | 1 = deadhead, 0 = revenue |
| paxLoad | How many passengers are on the vehicle right now | Yes | 14 |
| paxCount | Number of passengers that just got on or off | No | 2 |
| paxOnOff | If `paxCount` represents On or Off | No | 1 = on, 0 = off, null = no event |
| timestamp | When the record was generated | Yes | "2023-03-11 14:22:00" |


---

## Endpoint

Azure Storage Queue (owned by CTS)

https://cts.queue.core.windows.net/passio-assignments  


Passio will Peek, Process and Dequeue

Passio to provide REST endpoint to sanity check agencyId.  
Input: agencyId  
Output: agencyName  

---

## Assignment Sample Dataset with PaxCount

```
{
  "agencyId": "2868",
  "vehicleId": "123",
  "vehicleVIN": "JA3AU26U18U042758",
  "driverName": "Nick Hexum",
  "blockId": "234",
  "stopId": "345",
  "tripId": "765",
  "routeId": "987",
  "outOfService": "1",
  "paxLoad": "11",
  "paxOnOff": "0",
  "paxCount": "3",
  "timestamp": "2023-03-11 14:22:00"
}

```

## Assignment Sample Dataset when stop is serviced and no PaxCount

```
{
  "agencyId": "2868",
  "vehicleId": "123",
  "vehicleVIN": "JA3AU26U18U042758",
  "driverName": "Nick Hexum",
  "blockId": "234",
  "stopId": "345",
  "tripId": "765",
  "routeId": "987",
  "outOfService": "1",
  "paxLoad": "11",
  "paxOnOff": null,
  "paxCount": 0,
  "timestamp": "2023-03-11 14:22:00"
}

```

## Assignment Sample Dataset when deviated stop is serviced

```
{
  "agencyId": "2868",
  "vehicleId": "123",
  "vehicleVIN": "JA3AU26U18U042758",
  "driverName": "Nick Hexum",
  "blockId": "234",
  "stopId": "345443", //ignore this as it is not part of tripId 765
  "tripId": "765",
  "routeId": "987",
  "outOfService": "1",
  "paxLoad": "11",
  "paxOnOff": 1,
  "paxCount": 2, //will attached to last known fixed stop (I think this is okay)
  "timestamp": "2023-03-11 14:22:00"
}

```