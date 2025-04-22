# Denver Reporting API Endpoints info

## Credentials

user: {Get from Gavin}  
pass: {Get from Gavin}  

Change Password here:  
`https://passio3.com`

Get accessToken with this call:  
`https://passio3.com/auth/login?username={username}&password={password}&extended=1`


## Log API

Access Log for Today (JSON)  
https://passio3.com/flydenver/report/log/log.json?accessToken={token}

Access Log for Today (CSV)  
https://passio3.com/flydenver/report/log/log/?accessToken={token}

Access Log for data range (JSON)  
https://passio3.com/flydenver/report/log/log/2025-03-11/2025-03-14.json?accessToken={token}

Access Log for data range (CSV)  
https://passio3.com/flydenver/report/log/log/2025-03-11/2025-03-14/?accessToken={token}

You can also filter specific data using POST body. For example:  
`{"filter": {"onOff": {"=": ["on","off"]}}}`  
Will return only records where the onOff field is populated

You can also filter on multiple items. For example:  
`{"filter": {"onOff": {"=": ["on","off"]}, "created" : {"from" : "2025-03-11 18:28:00"}}}`  
Will return  records where the onOff field is populated and the record was created after 6:28pm on March 11. Note the seconds are populated. That is important.

### Other notes:  
All assignment data (route, stop, trip) is considered current. If assignment data is missing or null, it is because that vehicle was not assigned to a current piece of work. If the vehicle is between stops, the stop will be the last serviced stop. If the vehicle is between trips, the trip will show the last assigned trip.

## Sample Dataset
```
[{
    "id": 963035565,
    "date": "2025-04-22",
    "time": "00:00:02",
    "ms": 228,
    "bus": "320",
    "driver": "Scott, Nicholas",
    "route": "Airside C Concourse",
    "stop": "C CENTER CORE STOP",
    "eta": null,
    "count": "1",
    "customer": "flydenver",
    "device": "APS1-000B91A3A84A",
    "passengerType": "APS10",
    "onOff": "on",
    "latitude": "39.863671867",
    "longitude": "-104.673545183",
    "speed": null,
    "course": null,
    "heading": null,
    "distance": null,
    "cardId": null,
    "locationException": null,
    "address": null,
    "uploadDatetime": null,
    "hash": null,
    "dup": null,
    "userId": "5397",
    "uid": "2025-04-22 00:00:02.228",
    "paxLoad": "9",
    "more": null,
    "created": "2025-04-22 00:00:03",
    "datetime": "2025-04-22 00:00:02",
    "zohoStatus": null,
    "cardStatusId": null,
    "eta2": null,
    "routeBlock": "Airside C",
    "deviceId": "444094",
    "busId": "18352",
    "driverId": "93216",
    "routeBlockId": "160210",
    "routeStopId": "1437275",
    "passengerTypeId": "65928",
    "trip": null,
    "tripId": "856900",
    "timePoint": null,
    "timePointId": "15645015",
    "syslogId": null,
    "firmware": null,
    "firmwareId": null,
    "logUpload": null,
    "logUploadId": null,
    "busUpdateLogId": "1740544913",
    "createdUtc": "2025-04-22 06:00:03",
    "datetimeUtc": "2025-04-22 06:00:02"
  },
  {
    "id": 963035566,
    "date": "2025-04-22",
    "time": "00:00:05",
    "ms": 298,
    "bus": "319",
    "driver": "Habibullah Tareen",
    "route": "Pikes Peak West",
    "stop": "LEVEL 5 PICK-UP/DROP-OFF",
    "eta": null,
    "count": "1",
    "customer": "flydenver",
    "device": "APS2-000B91A3A531",
    "passengerType": "APS11",
    "onOff": "on",
    "latitude": "39.848564467",
    "longitude": "-104.672513833",
    "speed": null,
    "course": null,
    "heading": null,
    "distance": null,
    "cardId": null,
    "locationException": null,
    "address": null,
    "uploadDatetime": null,
    "hash": null,
    "dup": null,
    "userId": "5397",
    "uid": "2025-04-22 00:00:05.298",
    "paxLoad": "19",
    "more": null,
    "created": "2025-04-22 00:00:05",
    "datetime": "2025-04-22 00:00:05",
    "zohoStatus": null,
    "cardStatusId": null,
    "eta2": null,
    "routeBlock": "Pikes Peak West",
    "deviceId": "443996",
    "busId": "18351",
    "driverId": "98130",
    "routeBlockId": "160208",
    "routeStopId": "1437254",
    "passengerTypeId": "65929",
    "trip": null,
    "tripId": "856898",
    "timePoint": null,
    "timePointId": "15644993",
    "syslogId": null,
    "firmware": null,
    "firmwareId": null,
    "logUpload": null,
    "logUploadId": null,
    "busUpdateLogId": "1740544951",
    "createdUtc": "2025-04-22 06:00:05",
    "datetimeUtc": "2025-04-22 06:00:05"
  }...]
```


## Active Driver

`https://passio3.com/passioTransit/activeDriver?userId=5397&from=yyyy-mm-dd&to=yyyy-mm-dd&outOfService=0&accessToken={accessToken}`

List of driver activity segmented by IS/OOS and vehicle  

Use `outOfService` query parameter to specify in service or out of service records. Leave out to include both.

```
{
"busId": 18347,
"driverId": 93047,
"outOfService": 0,
"from": "2025-04-21 04:41:02",
"to": "2025-04-21 06:33:25"
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

`https://passio3.com/passioTransit/headway?userId=5397&from=yyyy-mm-dd&to=yyyy-mm-dd&accessToken={accessToken}`

Show headway data for every stop by every vehicle for the given date range.

```
{
"arrivalDatetime": {
"value": "2025-04-21T00:59:02.000Z"
},
"routeGroupId": 7029,
"routeId": 59996,
"busId": 18356,
"routeStopId": 1440032,
"arrivalArrivalDuration": null,
"arrivalDepartureDuration": null,
"departureArrivalDuration": null,
"departureDepartureDuration": null,
"broken": false
}
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

`https://passio3.com/passioTransit/activeVehicle?userId=5397&from=yyyy-mm-dd&to=yyyy-mm-dd&accessToken={accessToken}`

Unique number of vehicles in service aggregated by hour.

You will have two counts per hour (xx:00 - xx:59). One count will be the number of vehicles that have an in service record between xx:00 and xx:59 and the other count will be the number of vehicles that have an out of service record between xx:00 and xx:59. Keep in mind that it is possible for a vehicle to have both and be counted in both counts
In service and out of service logic is same as Active Driver API

```
[{
"date": "2025-04-21",
"hour": 0,
"outOfService": 0,
"count": 26
},
{
"date": "2025-04-21",
"hour": 0,
"outOfService": 1,
"count": 21
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
JSON Body:  `{"type":"route","userId":"5397","field" : ["id", "name", "color", "shortName", "color", "textColor"], "limit" : 400}`

#### Bus: {#tdb-bus}
POST: `https://passio3.com/tdb/get/?accessToken={token}`  
JSON Body:  `{"type":"bus","userId":"5397","field" : ["id", "name", "vin"], "limit" : 400}`

#### Driver: {#tdb-driver}
POST: `https://passio3.com/tdb/get/?accessToken={token}`  
JSON Body:  `{"type":"driver","userId":"5397", "field" : ["name", "id","firstName", "lastName"],  "id" : 16620, "limit" : 400}`

#### Route Stop: {#tdb-route-stop}
POST: `https://passio3.com/tdb/get/?accessToken={token}`  
JSON Body:  `{"type":"routeStop","userId":"5397", "id" : 897276, "limit" : 400}`

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
