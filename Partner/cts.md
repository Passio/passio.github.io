# Assignment And Pax Count Data Spec

## Overview
Vehicles will have Calamps.  
Passio will build routes and stops and trips in Navigator.  

CTS will ingest our GTFS from Navigator.  
CTS will assign vehicles to GTFS Blocks in TripMaster.  

Passio needs to show the vehicle's location, route, ETAs, etc on Passio GO.  
Passio needs to generate NTD Report.  
Passio cannot depend solely on vMDT because of many deviations the vehicle will do.  



We will use two data objects:

| Name | Purpose | Frequency Now | Frequency Planned |
| --- | --- | --- | --- |
| Assignment | Tell Passio which vehicle is doing which piece of work <br> including trip, stop, route, driver and paxLoad | 30 secs | Real-time |
| PaxCount | Tell Passio how many people got on and off at each stop | 24 hrs | Near real-time |


## Block Assignment lifecycle

| Event | Block Assignment | Service Status | More |
| --- | --- | --- | --- |
| Driver Pre Trip | None | Deadhead (OOS:1) | |
| Driver on way to first stop | Block Assignment | Deadhead (OOS:1) | |
| Driver at first stop | Block Assigment | Revenue (OOS:0) | |
| Driver doing work | Block Assignment | Revenue (OOS:0) | |
| Driver getting ready to leave last stop | Block Assignment | Deadhead (OOS:1) | |
| Driver parked at yard ready to start post trip | None | Deadhead (OOS:1) | |



## Assignment Data Object

| Field | Description | Required | Expected Values |
| --- | --- | --- | --- |
| agencyId | ID of agency | Yes | Should match `agency_id` in agency.txt | 2868 |
| vehicleId | ID of vehicle | Yes | CTS Internal ID. Will match up with our external ID |
| vehicleVIN | VIN of vehicle | No | For extra level of validation when ID is not unique due to multi-tenent db structure |
| driverName | First and last name of driver | Yes |  "Nick Hexum" |
| blockId | ID of GTFS Block. Should match `block_id` in trips.txt | Yes | 44678|
| stopId | ID of last stop. Should match `stop_id` in stops.txt | No | If not included, we will use vMDT or last known stop |
| tripId | ID of current trip. Should match `trip_id` in trips.txt | Yes | 32889 | 
| routeId | ID of current route. Should match `route_id` in routes.text | Yes | 88567 |
| outOfService | If the vehicle is revenue or deadhead | Yes | 1 = deadhead, 0 = revenue |
| paxLoad | How many passengers are on the vehicle right now | Yes | 14 |
| timestamp | When the record was generated | Yes | "2023-03-11 14:22:00" |


## PaxCount Data Object

| Field | Description | Required | Expected Values |
| --- | --- | --- | --- |
| agencyId | ID of agency | Yes | Should match `agency_id` in agency.txt | 2868 |
| vehicleId | ID of vehicle | Yes | CTS Internal ID. Will match up with our external ID |
| vehicleVIN | VIN of vehicle | No | For extra level of validation when ID is not unique due to multi-tenent db structure |
| driverName | First and last name of driver | Yes |  "Nick Hexum" |
| blockId | ID of GTFS Block. Should match `block_id` in trips.txt | Yes | 44678|
| stopId | ID of stop where on or off took place. Should match `stop_id` in stops.txt | Yes | 69332 |
| tripId | ID of current trip. Should match `trip_id` in trips.txt | Yes | 32889 | 
| routeId | ID of current route. Should match `route_id` in routes.text | Yes | 88567 |
| outOfService | If the vehicle is revenue or deadhead | Yes | 1 = deadhead, 0 = revenue |
| paxLoad | How many passengers are on the vehicle right now | PENDING DISCUSSION | 14 |
| paxCount | Number of passengers that just got on or off | Yes | 2 |
| paxOnOff | If `paxCount` represents On or Off | Yes | 1 = on, 0 = off |
| timestamp | When the record was generated | Yes | "2023-03-11 14:22:00" |

## Endpoint

Azure Storage Queue (owned by CTS)

https://cts.queue.core.windows.net/passio-assignments  
https://cts.queue.core.windows.net/passio-paxcount

Passio will Peek, Process and Dequeue


## Assignment Sample Dataset

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
  "timestamp": "2023-03-11 14:22:00"
}

```

## PaxCount Sample Dataset

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
