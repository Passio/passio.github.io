# Assignment And Pax Count Data Spec

## Overview
Vehicles will have CalAmps.  
Passio will build routes and stops and trips in Navigator.  

CTS will ingest GTFS from Navigator.  
CTS will assign vehicles to GTFS Blocks in TripMaster.  

Passio needs to show the vehicle's location, route, ETAs, etc on Passio GO.  
Passio needs to generate NTD Report.  
Passio cannot depend solely on vMDT because of many deviations the vehicle will do.  



We will use two data objects  
[Assignment Data Object](#assignment-object): Will be sent from ParaScope on driver login, service start, break start, break end, service stop and pick up/perform events.  
[GPS Data Object](#gps): Will be sent from ParaScope every 30 seconds

### GPS Information
GPS was added to the spec on 2023-09-05. It serves mostly as a keep-alive packet for Passio to keep the device considered online, which is a critical element in dispatcher managment tools. It also enables a second GPS data source in Passio Navigator and enables future solutions where CTS could be primary GPS data source.

### Object Types {#object-types}
Object types were added to the spec on 2023-09-05 to differentiate between data types  

| ID | Description |
| --- | --- |
| 0 | Assigment Data |
| 1 | GPS Data |


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

## Assignment Data Object {#assignment-object}

| Field | Description | Required | Expected Values + Details |
| --- | --- | --- | --- |
| agencyId | ID of agency | Yes | Should match `agency_id` in agency.txt | 2868 |
| vehicleId | ID of vehicle | Yes | CTS Internal ID. Will match up with our external ID |
| dataType | ID of datatype | Yes | [Should be 0 for Assignment](#object-types) |
| vehicleVIN | VIN of vehicle | No | For extra level of validation when ID is not unique due to multi-tenent db structure |
| driverName | First and last name of driver | Yes |  "Nick Hexum" |
| blockId | ID of GTFS Block. Should match `block_id` in trips.txt | Yes | 44678|
| stopId | ID of last stop. Should match `stop_id` in stops.txt | No | If not included, we will use vMDT or last known stop.<br>We will need to verify that stopId exists on tripId (when CTS is performing Deviated stop).<br>If not, we will ignore stopId and use last known stopId |
| stopSequence | Stop order of current `stopId`. Should match `stop_sequence` in stop_times.txt | Yes | Used to reconcile the scenerio where the stop exists twice in a trip. Most commonly the first and last stop of a looping route |
| tripId | ID of current trip. Should match `trip_id` in trips.txt | Yes | 32889 | 
| routeId | ID of current route. Should match `route_id` in routes.text | Yes | 88567 |
| outOfService | If the vehicle is revenue or deadhead | Yes | 1 = deadhead, 0 = revenue |
| paxLoad | How many passengers are on the vehicle right now | Yes | 14 |
| paxCount | Number of passengers that just got on or off | No | 2 |
| paxOnOff | If `paxCount` represents On or Off | No | 1 = on, 0 = off, null = no event |
| timestamp | When the record was generated | Yes | "2023-03-11 14:22:00" |


---

## GPS Data Object {#gps}

| Field | Description | Required | Expected Values + Details |
| --- | --- | --- | --- |
| agencyId | ID of agency | Yes | Should match `agency_id` in agency.txt | 2868 |
| vehicleId | ID of vehicle | Yes | CTS Internal ID. Will match up with our external ID |
| dataType | ID of datatype | Yes | [Should be 1 for GPS](#object-types) |
| lat | Latitude of location | Yes | 34.829848 |
| lng | Longitude of location | Yes | -82.332448 |
| speed | Velocity of vehicle | No | 7.59 Should be meters per second |
| heading | Cardinal direction | No | 0 - 359.9 0 is true north |
| odometer | Last odometer reading | No | In meters |
| timestamp | When the reading was recorded | Yes | "2023-03-11 14:22:00" |

## Endpoint

Azure Storage Queue (owned by CTS)

https://cts.queue.core.windows.net/passio-assignments  


Passio will Peek, Process and Dequeue

Passio to provide REST endpoint to sanity check agencyId.  
Input: agencyId  
Output: true | false

Swagger docs available here - 
https://app.passiotransit.com/swagger/index.html

Browse to Internal section

Example usage to check agency 1901:
```
curl -X 'GET' \
  'https://app.passiotransit.com/api/v1/Internal/ValidAgency?agency=1901' \
  -H 'accept: text/plain'
```

---

## Assignment Sample Dataset with PaxCount

```
{
  "agencyId": "2868",
  "vehicleId": 123,
  "dataType" : 0,
  "vehicleVIN": "JA3AU26U18U042758",
  "driverName": "Nick Hexum",
  "blockId": 234,
  "stopId": 345,
  "stopSequence": 1,
  "tripId": 765,
  "routeId": 987,
  "outOfService": 0,
  "paxLoad": 11,
  "paxOnOff": 0,
  "paxCount": 3,
  "timestamp": "2023-03-11 14:22:00"
}

```

## Assignment Sample Dataset when stop is serviced and no PaxCount

```
{
  "agencyId": "2868",
  "vehicleId": 123,
  "dataType" : 0,
  "vehicleVIN": "JA3AU26U18U042758",
  "driverName": "Nick Hexum",
  "blockId": 234,
  "stopId": 345,
  "stopSequence": 1,
  "tripId": 765,
  "routeId": 987,
  "outOfService": 0,
  "paxLoad": 11,
  "paxOnOff": null,
  "paxCount": 0,
  "timestamp": "2023-03-11 14:22:00"
}

```

## Assignment Sample Dataset when deviated stop is serviced

```
{
  "agencyId": "2868",
  "vehicleId": 123,
  "dataType" : 0,
  "vehicleVIN": "JA3AU26U18U042758",
  "driverName": "Nick Hexum",
  "blockId": 234,
  "stopId": 345443, //ignore this as it is not part of tripId 765
  "stopSequence": 0, //ignore this as not a fixed stop
  "tripId": 765,
  "routeId": 987,
  "outOfService": 0,
  "paxLoad": 11,
  "paxOnOff": 1,
  "paxCount": 2, //will attached to last known fixed stop (I think this is okay)
  "timestamp": "2023-03-11 14:22:00"
}

```

## GPS Sample Dataset

```
{
  "agencyId": "2868",
  "vehicleId": 123,
  "dataType" : 1,
  "lat": 34.844836,
  "lng": -82.355144,
  "speed": 11.17, //25 mph
  "heading": 270, //due West
  "odometer": 72420480, // 45,000 miles in meters
  "timestamp": "2023-03-11 14:22:00"
}

```
