# Assignment And Pax Count Data Spec

## Overview
Vehicles will have Calamps.  
Passio will build routes and stops and trips in Navigator.  

CTS will ingest our GTFS from Navigator.  
CTS will assign vehicles to GTFS Blocks in TripMaster.  

Passio needs to show the vehicle's location, route, ETAs, etc on Passio GO.  
Passio needs to generate NTD Report.  
Passio cannot depend solely on vMDT because of many deviations the vehicle will do.  

CTS will send us data packages every 30 seconds

## Data Object

| Field | Description | Required | Expected Values |
| --- | --- | --- | --- |
| vehicleId | ID of vehicle | Yes | CTS Internal ID. Will match up with our external ID |
| vehicleVIN | VIN of vehicle | Yes | For extra level of validation when ID is not unique due to multi-tenent db structure |
| driverName | First and last name of driver | Yes |  "Nick Hexum" |
| blockId | ID of GTFS Block. Should match `block_id` in trips.txt | Yes | 44678|
| stopId | ID of last stop. Should match `stop_id` in stops.txt | No | If not included, we will use vMDT or last known stop |
| tripId | ID of current trip. Should match `trip_id` in trips.txt | Yes | 32889 | 
| routeId | ID of current route. Should match `route_id` in routes.text | Yes | 88567 |
| outOfService | If the vehicle is revenue or deadhead | Yes | 1 = deadhead, 0 = revenue |
| paxLoad | How many passengers on on the vehicle right now | Yes | 14 |
| paxCount | Number of passengers that just got on or off | Yes | 2 |
| paxOnOff | If `paxCount` represents On or Off | Yes | 1 = on, 0 = off |
| timestamp | When the record was generated | Yes | "2023-03-11 14:22:00" |

## Endpoint

TBD. Either Azure Queue or AWS MQTT


## Sample Dataset

```
{
  "vehicleId": 123,
  "vehicleVIN": "JA3AU26U18U042758",
  "driverName": "Nick Hexum",
  "blockId": "44678",
  "stopId": "345",
  "tripId": "32889",
  "routeId": "88567",
  "outOfService": 1,
  "paxLoad": 11,
  "paxCount": 3,
  "paxOnOff": 0,
  "timestamp": "2023-03-11 14:22:00"
}

```
