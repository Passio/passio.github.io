# ByteCurve information for Passio API

username: {ranga.gopalan@bytecurve.com}  
password: {Get from Ranga}

## Client user names

| Username | Account | User ID |
| --- | --- | --- |
|   `ClemsonU`    |  Clemson University     | 793 |
|    `Clemson2`   |   Clemson Internal    | 1654 |


Get accessToken with this call:  
https://passio3.com/auth/login?username={username}&password={password}&extended=1

## Historical Location Data

Access Data for Today (JSON)  
https://passio3.com/{client_username}/report/log/location.json?accessToken={token}

Access Data for Today (CSV)  
https://passio3.com/{client_username}/report/log/location/?accessToken={token}

Access Data for data range (JSON)  
https://passio3.com/{client_username}/report/log/location/2026-02-01/2026-02-04.json?accessToken={token}

Access Data for data range (CSV)  
https://passio3.com/{client_username}/report/log/location/2026-02-01/2026-02-04/?accessToken={token}

You can also filter specific data using POST body. For example:  
`{"filter": {"bus": {"=": ["311","312"]}}}`  
Will return only records where the bus 311 or 312

You can also filter on multiple items. For example:  
`{"filter": {"bus": {"=": ["311","312"]}, "created" : {"from" : "2025-03-11 18:28:00"}}}`  
Will return  records where the onOff field is populated and the record was created after 6:28pm on March 11. Note the seconds are populated. That is important.

### Example of historical data

```json
[{"id": "25342792409","userId": "793","bus": "3096","route": "Blue East 2","latitude": "34.675823300","longitude": "-82.835272700","speed": "0","course": "60.9","heading": null,"created": "2026-02-24 09:37:10","datetime": "2026-02-24 09:37:10","invalid": 0,"correctedLatitude": "34.675835789","correctedLongitude": "-82.835282826","calculatedCourse": "146.30993247402023","paxLoad": "0","more": null,"deviceId": "450866","busId": "20352","routeBlockId": "178020","routeStopId": "1533231","trip": null,"tripId": "951056","timePoint": null,"timePointId": null,"manual": null,"accuracy": null,"provider": null,"device": "3096_CLEMSON_3A88","routeBlock": "Blue East 2","outOfService": 0,"driver": "Burt S.","driverId": "22041","stop": "Edwards Hall","stopId": "4506","point": null,"createdUtc": "2026-02-24 14:37:10","datetimeUtc": "2026-02-24 14:37:10"}]
```

## Realtime GPS data

You can use websockets, or GTFS-RT  

### Websockets:
URL: `wss://passio3.com/`  
JSON BODY: `{"subscribe" : "location", "userId" : [793,1654]}`  

With filter (only vehicles in revenue service)  
`{"subscribe" : "location", "userId" : [793,1654], "filter" : {"outOfService" : 0 }}`

Example  
```
9:34:49 : {"esn":4674921825,"latitude":34.791402,"longitude":-82.432434,"speed":25.27,"course":84,"created":"2026-02-24 09:34:47","more":{"eventCode":102,"hdop":8,"rssi":-70,"satellites":10},"deviceId":414862,"routeBlock":"102","userId":793,"datetime":"2026-02-24 09:34:49","createdUtc":"2026-02-24 14:34:47","datetimeUtc":"2026-02-24 14:34:49","eventCode":102,"busId":9244,"driverId":172227,"routeBlockId":202179,"stopId":20025,"routeStopId":1637587,"tripId":1066721,"timePointId":20321876,"paxLoad":2,"outOfService":0,"device":"4674921825","bus":"3547","driver":"Nathaniel C.","route":"102","stop":"Walmart Easley OB","invalid":0,"calculatedCourse":81.82778454832311,"correctedLatitude":34.791389,"correctedLongitude":-82.432433,"id":25342730971,"type":"location","action":"add"}
```

### GTFS Trip Updates (Stop ETAs)  
URL (Human): https://passio3.com/{client_username}/passioTransit/gtfs/realtime/tripUpdates.json  
URL (protobuf): https://passio3.com/{client_username}/passioTransit/gtfs/realtime/tripUpdates  

### GTFS Vehicle Positions (GPS)  
URL (Human): https://passio3.com/{client_username}/passioTransit/gtfs/realtime/vehiclePositions.json  
URL (Protobuf): https://passio3.com/{client_username}/passioTransit/gtfs/realtime/vehiclePositions  


## Other notes:  
All assignment data (route, stop, trip) is considered current. If assignment data is missing or null, it is because that vehicle was not assigned to a current piece of work. If the vehicle is between stops, the stop will be the last serviced stop. If the vehicle is between trips, the trip will show the last assigned trip.


