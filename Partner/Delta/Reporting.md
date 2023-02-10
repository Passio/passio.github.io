# Delta Reporting API Endpoints info

## Credentials

user: {Get from Bilal}  
pass: {Get from Bilal}  

Change Password here:  
`https://passio3.com`

Get accessToken with this call:  
`https://passio3.com/auth/login?username={username}&password={password}&extended=1`


## Active Driver

`https://passio3.com/passioTransit/activeDriver?userId=2072&from=yyyy-mm-dd&to=yyyy-mm-dd&outOfService=0&accessToken={accessToken}`

List of driver activity segmented by IS/OOS and vehicle  

Use `outOfService` query parameter to specify in service or out of service records. Leave out to include both.

```
{
  "busId": 8744,
  "driverId": 16620,
  "outOfService": 0,
  "from": "2022-10-01 00:00:01",
  "to": "2022-10-01 00:18:59"
}
```

| Field | Definition | 
| --- | --- |
| busId | Id of Vehicle. Can be resolved with [Bus API call](#tdb-bus) |
| driverId | Id of Driver. Can be resolved with [Driver API call](#tdb-driver)  |
| outOfService | If this record defines an [In Service (revenue)](#oos-revenue) period or [Out Of Service (deadhead)](#oos-deadhead) period  |
| from | Start of record period |
| to | End of record period |


## Headway

`https://passio3.com/passioTransit/headway?userId=2072&from=yyyy-mm-dd&to=yyyy-mm-dd&accessToken={accessToken}`

Show headway data for every stop by every vehicle for the given date range.

```
{
        "arrivalDatetime": {
            "value": "2022-10-01T13:18:31.000Z"
        },
        "routeId": 30873,
        "busId": 8717,
        "routeStopId": 897276,
        "arrivalArrivalDuration": 1181,
        "arrivalDepartureDuration": 1148,
        "departureArrivalDuration": 1199,
        "departureDepartureDuration": 1166,
        "broken": false
    },
```

| Field | Definition | 
| --- | --- |
| arrivalDatetime | Actual arrival time  |
| routeId | Id of Route servicing this stop. Can be resolved with [Route API call](#tdb-route) |
| busId | Id of Vehicle. Can be resolved with [Bus API call](#tdb-bus)|
| routeStopId | Stop being serviced. Can be resolved with [RouteStop API call](#tdb-route-stop) |
| arrivalArrivalDuration | Seconds between this arrival and previous arrival  |
| arrivalDepartureDuration | Seconds between this arrival and previous departure |  
| departureArrivalDuration | Seconds between this departure and previous arrival | 
| departureDepartureDuration | Seconds between this departure and previous departure | 
| broken | If there was a gap in servicing this stop based on the expected stop order | 



## Active Vehicle Count

`https://passio3.com/passioTransit/activeVehicle?userId=2072&from=yyyy-mm-dd&to=yyyy-mm-dd&accessToken={accessToken}`

Unique number of vehicles in service aggregated by hour.

You will have two counts per hour (xx:00 - xx:59). One count will be the number of vehicles that have an in service record between xx:00 and xx:59 and the other count will be the number of vehicles that have an out of service record between xx:00 and xx:59. Keep in mind that it is possible for a vehicle to have both and be counted in both counts
In service and out of service logic is same as Active Driver API

```
[{
    "date": "2022-10-01",
    "hour": 0,
    "outOfService": 0,
    "count": 44
},
{
    "date": "2022-10-01",
    "hour": 0,
    "outOfService": 1,
    "count": 20
}]
```

| Field | Definition | 
| --- | --- |
| date | Service date |
| hour | Service hour (0-23) |
| outOfService | If this record defines an [In Service (revenue)](#oos-revenue) period or [Out Of Service (deadhead)](#oos-deadhead) period |
| count | Number of vehicles in the IS/OOS state during this hour block |



## Addtional API Information


#### Route: {#tdb-route}
POST: `https://passio3.com/tdb/get/?accessToken={token}`  
JSON Body:  `{"type":"route","userId":"2072","field" : ["id", "name", "color", "shortName", "color", "textColor"], "limit" : 400}`

#### Bus: {#tdb-bus}
POST: `https://passio3.com/tdb/get/?accessToken={token}`  
JSON Body:  `{"type":"bus","userId":"2072","field" : ["id", "name", "vin"], "limit" : 400}`

#### Driver: {#tdb-driver}
POST: `https://passio3.com/tdb/get/?accessToken={token}`  
JSON Body:  `{"type":"driver","userId":"2072", "field" : ["name", "id","firstName", "lastName"],  "id" : 16620, "limit" : 400}`

#### Route Stop: {#tdb-route-stop}
POST: `https://passio3.com/tdb/get/?accessToken={token}`  
JSON Body:  `{"type":"routeStop","userId":"2072", "id" : 897276, "limit" : 400}`

## Definitions


#### outOfService: true || 1 {#oos-deadhead}  
Driver has tapped "Stop Service" on the MDT OR
Dispatcher has taken a driver or the vehicle they are in out of service OR
Driver has entered into a specific Yard geofence that has automatically taken them out of service

#### outOfService: false || 0  {#oos-revenue}  
Driver has tapped "Start Service" on the MDT
Dispatcher has assigned a driver or a vehicle to be in service on a job/route
Driver has entered the first geofence of the first stop of the route/job they are assigned to so the system automatically put them into service

Active Vehicle:
0 = 12am
You will have two counts per hour (xx:00 - xx:59). One count will be the number of vehicles that have an in service record between xx:00 and xx:59 and the other count will be the number of vehicles that have an out of service record between xx:00 and xx:59. Keep in mind that it is possible for a vehicle to have both and be counted in both counts
In service and out of service logic is same as Active Driver API

