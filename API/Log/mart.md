# Passio Log API for MART


## Rate limiting
This API can go back 30 days. It is advised to add filters and to not call more than one day at a time to avoid rate limiting.

## Token information
Get accessToken with this call:  
https://passio3.com/auth/login?username={username}&password={password}&extended=1

For username and passoword, contact Bledar Ramo.


## API examples
Access Log for Today (JSON)  
https://passio3.com/montachusett/report/log/log.json?accessToken={token}

Access Log for Today (CSV)  
https://passio3.com/montachusett/report/log/log/?accessToken={token}

Access Log for data range (JSON)  
https://passio3.com/montachusett/report/log/log/2024-03-01/2024-03-11.json?accessToken={token}

Access Log for data range (CSV)  
https://passio3.com/montachusett/report/log/log/2024-03-01/2024-03-11/?accessToken={token}

You can also filter specific data using POST body. For example:  
`{"filter": {"driverId": {"!=": ["",null]}}}`  
Will return only records where the Driver ID is not null and not empty

You can also filter on multiple items. For example:  
`{"filter": {"driverId": {"!=": ["",null]}, "created" : {"from" : "2024-03-11 18:28:00"}}}`  
Will return records with a Driver ID and was created after 6:28pm on March 11. Note the seconds are populated. That is important.

### Sample dataset
```
[
    {
        "id": 678279891,
        "date": "2024-03-11",
        "time": "18:29:30",
        "ms": 414,
        "bus": "4182",
        "driver": "Mendez Maria",
        "route": "2 Fitchburg/Leominster Fitchburg",
        "stop": "MART Garage (City Line Inbound), Fitchburg",
        "eta": null,
        "count": "1",
        "customer": "montachusett",
        "device": "APC2-A31221",
        "passengerType": "APS11",
        "onOff": "off",
        "latitude": "42.574057283",
        "longitude": "-71.789920517",
        "speed": null,
        "course": null,
        "heading": null,
        "distance": null,
        "cardId": null,
        "locationException": 1,
        "address": "true",
        "uploadDatetime": null,
        "hash": null,
        "dup": null,
        "userId": "2173",
        "uid": "2024-03-11 18:29:30.414",
        "paxLoad": "3",
        "more": null,
        "created": "2024-03-11 18:29:30",
        "datetime": "2024-03-11 18:29:30",
        "zohoStatus": null,
        "cardStatusId": null,
        "eta2": null,
        "routeBlock": "19664",
        "deviceId": "414324",
        "busId": "9164",
        "driverId": "17131",
        "routeBlockId": "59287",
        "routeStopId": "674597",
        "passengerTypeId": "16308",
        "trip": null,
        "tripId": "292469",
        "timePoint": null,
        "timePointId": "5338359",
        "syslogId": null,
        "firmware": null,
        "firmwareId": null,
        "logUpload": null,
        "logUploadId": null,
        "busUpdateLogId": "1035315439",
        "createdUtc": "2024-03-11 22:29:30",
        "datetimeUtc": "2024-03-11 22:29:30"
    },
    {
        "id": 678279915,
        "date": "2024-03-11",
        "time": "18:29:31",
        "ms": 446,
        "bus": "4182",
        "driver": "Mendez Maria",
        "route": "2 Fitchburg/Leominster Fitchburg",
        "stop": "MART Garage (City Line Inbound), Fitchburg",
        "eta": null,
        "count": "1",
        "customer": "montachusett",
        "device": "APC2-A31221",
        "passengerType": "APS11",
        "onOff": "off",
        "latitude": "42.574057283",
        "longitude": "-71.789920517",
        "speed": null,
        "course": null,
        "heading": null,
        "distance": null,
        "cardId": null,
        "locationException": 1,
        "address": "true",
        "uploadDatetime": null,
        "hash": null,
        "dup": null,
        "userId": "2173",
        "uid": "2024-03-11 18:29:31.446",
        "paxLoad": "2",
        "more": null,
        "created": "2024-03-11 18:29:32",
        "datetime": "2024-03-11 18:29:31",
        "zohoStatus": null,
        "cardStatusId": null,
        "eta2": null,
        "routeBlock": "19664",
        "deviceId": "414324",
        "busId": "9164",
        "driverId": "17131",
        "routeBlockId": "59287",
        "routeStopId": "674597",
        "passengerTypeId": "16308",
        "trip": null,
        "tripId": "292469",
        "timePoint": null,
        "timePointId": "5338359",
        "syslogId": null,
        "firmware": null,
        "firmwareId": null,
        "logUpload": null,
        "logUploadId": null,
        "busUpdateLogId": "1035315481",
        "createdUtc": "2024-03-11 22:29:32",
        "datetimeUtc": "2024-03-11 22:29:31"
    }
]
```



