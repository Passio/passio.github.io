# Concord information for Passio Log API

username: {Get from Agency}  
password: {Get from Agency}
  

Get accessToken with this call:  
https://passio3.com/auth/login?username={username}&password={password}&extended=1

Access Log for Today (JSON)  
https://passio3.com/concordkat/report/log/log.json?accessToken={token}

Access Log for Today (CSV)  
https://passio3.com/concordkat/report/log/log/?accessToken={token}

Access Log for data range (JSON)  
https://passio3.com/concordkat/report/log/log/2023-02-01/2023-02-04.json?accessToken={token}

Access Log for data range (CSV)  
https://passio3.com/concordkat/report/log/log/2023-02-01/2023-02-04/?accessToken={token}

You can also filter specific data using POST body. For example:  
`{"filter": {"onOff": {"=": ["on","off"]}}}`  
Will return only records where the onOff field is populated

You can also filter on multiple items. For example:  
`{"filter": {"onOff": {"=": ["on","off"]}, "created" : {"from" : "2023-03-11 18:28:00"}}}`  
Will return  records where the onOff field is populated and the record was created after 6:28pm on March 11. Note the seconds are populated. That is important.

## Other notes:  
All assignment data (route, stop, trip) is considered current. If assignment data is missing or null, it is because that vehicle was not assigned to a current piece of work. If the vehicle is between stops, the stop will be the last serviced stop. If the vehicle is between trips, the trip will show the last assigned trip.

### Sample dataset
```
[
    {
        "id": 504431795,
        "date": "2023-03-12",
        "time": "18:31:56",
        "ms": 383,
        "bus": "506",
        "driver": "Rita Helms",
        "route": "Yellow Route",
        "stop": "Rt 29 & Beechwood Ave",
        "eta": null,
        "count": "1",
        "customer": "concordk",
        "device": "APC1-A1A356",
        "passengerType": "APS10",
        "onOff": "on",
        "latitude": "35.436168100",
        "longitude": "-80.604288000",
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
        "userId": "1901",
        "uid": "2023-03-12 18:31:56.383",
        "paxLoad": "3",
        "more": null,
        "created": "2023-03-12 18:31:57",
        "datetime": "2023-03-12 18:31:56",
        "zohoStatus": null,
        "cardStatusId": null,
        "eta2": null,
        "routeBlock": "Yellow Weekends",
        "deviceId": "410518",
        "busId": "8053",
        "driverId": "16385",
        "routeBlockId": "104012",
        "routeStopId": "269484",
        "passengerTypeId": "15151",
        "trip": null,
        "tripId": "520105",
        "timePoint": null,
        "timePointId": "9902536",
        "syslogId": null,
        "firmware": null,
        "firmwareId": null,
        "logUpload": null,
        "logUploadId": null,
        "busUpdateLogId": "657251303",
        "createdUtc": "2023-03-12 22:31:57",
        "datetimeUtc": "2023-03-12 22:31:56"
    },
    {
        "id": 504432026,
        "date": "2023-03-12",
        "time": "18:34:12",
        "ms": 499,
        "bus": "506",
        "driver": "Rita Helms",
        "route": "Yellow Route",
        "stop": "Rt 73 & Southampton Dr (Outbound)",
        "eta": null,
        "count": "1",
        "customer": "concordk",
        "device": "APC1-A1A356",
        "passengerType": "APS10",
        "onOff": "off",
        "latitude": "35.430264100",
        "longitude": "-80.612956800",
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
        "userId": "1901",
        "uid": "2023-03-12 18:34:12.499",
        "paxLoad": "2",
        "more": null,
        "created": "2023-03-12 18:34:13",
        "datetime": "2023-03-12 18:34:12",
        "zohoStatus": null,
        "cardStatusId": null,
        "eta2": null,
        "routeBlock": "Yellow Weekends",
        "deviceId": "410518",
        "busId": "8053",
        "driverId": "16385",
        "routeBlockId": "104012",
        "routeStopId": "269485",
        "passengerTypeId": "15151",
        "trip": null,
        "tripId": "520105",
        "timePoint": null,
        "timePointId": "9902547",
        "syslogId": null,
        "firmware": null,
        "firmwareId": null,
        "logUpload": null,
        "logUploadId": null,
        "busUpdateLogId": "657252116",
        "createdUtc": "2023-03-12 22:34:13",
        "datetimeUtc": "2023-03-12 22:34:12"
    }
]
```

## Key Definitions

| Field | Definition | 
| --- | --- |
| id | databaseId |
| date time ms | Record timestamp |
| bus | Vehicle name |
| driver | Driver name |
| route | Route name |
| count | The number of people that go on or off |
| customer | Internal customer name |
| device | Name of device that generated the log record |
| passengerType | Type of passenger for reporting purposes |
| onOff | If the count reflects on or off (string) |
| lat lng | Coordinates of log location |
| speed course heading distance | GPS related data |
| userId | Internal customer Id |
| paxLoad | Number of riders on bus right now |
| more | Additional information in JSON format |
| created | When the record was created on the device |
| datetime | When the record was received by the server |
| deviceId | Id of device. Can be resolved with [Device API call](#tdb-device) 
| busId | Id of Vehicle. Can be resolved with [Bus API call](#tdb-bus) |
| driverId | Id of Driver. Can be resolved with [Driver API call](#tdb-driver)  |
| routeStopId | Id of route stop. Can be resolved with [Route Stop API call](#tdb-route-stop)  



## Addtional API Information


#### Route: {#tdb-route}
POST: `https://passio3.com/tdb/get/?accessToken={token}`  
JSON Body:  `{"type":"route","userId":"1901","field" : ["id", "name", "color", "shortName", "color", "textColor"], "limit" : 400}`

#### Bus: {#tdb-bus}
POST: `https://passio3.com/tdb/get/?accessToken={token}`  
JSON Body:  `{"type":"bus","userId":"1901","field" : ["id", "name", "vin"], "limit" : 400}`

#### Device: {#tdb-device}
POST: `https://passio3.com/tdb/get/?accessToken={token}`  
JSON Body:  `{"type":"device","userId":"1901","field" : ["id", "name"], "limit" : 400}`

#### Driver: {#tdb-driver}
POST: `https://passio3.com/tdb/get/?accessToken={token}`  
JSON Body:  `{"type":"driver","userId":"1901", "field" : ["name", "id","firstName", "lastName"],  "id" : 16620, "limit" : 400}`

#### Route Stop: {#tdb-route-stop}
POST: `https://passio3.com/tdb/get/?accessToken={token}`  
JSON Body:  `{"type":"routeStop","userId":"1901", "id" : 897276, "limit" : 400}`

#### Assigment and Revenue/Deadhead Information:
POST: `https://passio3.com/tdb/get/?accessToken={token}`  
JSON Body: `{"type":"busUpdateLog","userId":"1901", "filter" : {"created" : {">" : "2023-04-10"}, "busId" : "8053"}, "limit" : 3}`  
This can be referenced to see if the vehicle was in (Revenue) or out of service (Deadhead) during a date range. This log shows the source of the assignment and the revenue state of the vehicle at the time the record was created.




