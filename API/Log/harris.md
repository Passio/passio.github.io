# Passio Log API

## Rate limiting
This API can go back 30 days. It is advised to add filters and to not call more than one day at a time to avoid rate limiting.

## Token information
Get accessToken with this call:  
https://passio3.com/auth/login?username={username}&password={password}&extended=1

For username and password, contact Sonia

If password needs to be reset, visit this page - https://passio3.com/login/sendResetPassword


## API examples
Note, `location` can be used to get GPS data for arrival and departure times from a stop. https://passio3.com/harrisco/report/log/location.json?accessToken={token}

To merge location and log data, do a time series join using the `datetime` field.

Access Log for Today (JSON)  
https://passio3.com/harrisco/report/log/log.json?accessToken={token}

Access Log for Today (CSV)  
https://passio3.com/harrisco/report/log/log/?accessToken={token}

Access Log for data range (JSON)  
https://passio3.com/harrisco/report/log/log/2023-12-01/2023-12-20.json?accessToken={token}

Access Log for data range (CSV)  
https://passio3.com/harrisco/report/log/log/2023-12-01/2023-12-20/?accessToken={token}

You can also filter specific data using POST body. For example:  
`{"filter": {"cardId": {"!=": ["",null]}}}`  
Will return only records where the CardId is not null and not empty

You can also filter on multiple items. For example:  
`{"filter": {"stop": {"!=": ["",null]}, "created" : {"from" : "2025-03-11 18:28:00"}}}`  
Will return records with a stop and was created after 6:28pm on March 11. Note the seconds are populated. That is important.

### Sample dataset
```
[
  {
    "id": 1039067478,
    "date": "2025-08-13",
    "time": "05:22:52",
    "ms": 192,
    "bus": "6402",
    "driver": "Jimmie Carwell",
    "route": "Baytown 1 - Garth Road",
    "stop": "Garth at Park",
    "eta": "07:00",
    "count": "0",
    "customer": "harrisco",
    "device": "HARRIS-968100",
    "passengerType": "one",
    "onOff": "out",
    "latitude": "29.729536057",
    "longitude": "-94.969169617",
    "speed": "0.005144444294273853",
    "course": null,
    "heading": null,
    "distance": null,
    "cardId": null,
    "locationException": null,
    "address": null,
    "uploadDatetime": "2025-08-13 05:24:14",
    "hash": null,
    "dup": null,
    "userId": "3497",
    "uid": "2025-08-13 05:22:52.192",
    "paxLoad": "0",
    "more": null,
    "created": "2025-08-13 05:24:15",
    "datetime": "2025-08-13 05:22:52",
    "zohoStatus": null,
    "cardStatusId": null,
    "eta2": null,
    "routeBlock": "Baytown 1 - M-F",
    "deviceId": "424332",
    "busId": "13098",
    "driverId": "24268",
    "routeBlockId": "170337",
    "routeStopId": "1485832",
    "passengerTypeId": "36174",
    "trip": null,
    "tripId": "911316",
    "timePoint": null,
    "timePointId": "16797494",
    "syslogId": null,
    "firmware": null,
    "firmwareId": null,
    "logUpload": "2025-08-13 05:24:14",
    "logUploadId": "976439329",
    "busUpdateLogId": "1956106775",
    "createdUtc": "2025-08-13 10:24:15",
    "datetimeUtc": "2025-08-13 10:22:52"
    },
    {
    "id": 1039067493,
    "date": "2025-08-13",
    "time": "05:24:12",
    "ms": 837,
    "bus": "6402",
    "driver": "Jimmie Carwell",
    "route": "Baytown 1 - Garth Road",
    "stop": "Garth at Park",
    "eta": "07:00",
    "count": "0",
    "customer": "harrisco",
    "device": "HARRIS-968100",
    "passengerType": "autoOff",
    "onOff": "off",
    "latitude": "29.729547501",
    "longitude": "-94.969161987",
    "speed": "0.006173333618789911",
    "course": null,
    "heading": null,
    "distance": null,
    "cardId": null,
    "locationException": null,
    "address": null,
    "uploadDatetime": "2025-08-13 05:24:17",
    "hash": null,
    "dup": null,
    "userId": "3497",
    "uid": "2025-08-13 05:24:12.837",
    "paxLoad": "0",
    "more": {
    "OOS": 1
    },
    "created": "2025-08-13 05:24:17",
    "datetime": "2025-08-13 05:24:12",
    "zohoStatus": null,
    "cardStatusId": null,
    "eta2": null,
    "routeBlock": "Baytown 1 - M-F",
    "deviceId": "424332",
    "busId": "13098",
    "driverId": "24268",
    "routeBlockId": "170337",
    "routeStopId": "1485832",
    "passengerTypeId": "36186",
    "trip": null,
    "tripId": "911316",
    "timePoint": null,
    "timePointId": "16797494",
    "syslogId": null,
    "firmware": null,
    "firmwareId": null,
    "logUpload": "2025-08-13 05:24:17",
    "logUploadId": "976439352",
    "busUpdateLogId": "1956106775",
    "createdUtc": "2025-08-13 10:24:17",
    "datetimeUtc": "2025-08-13 10:24:12"
  }
]
```



