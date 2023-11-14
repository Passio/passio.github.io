# Passio Log API

## Rate limiting
This API can go back 30 days. It is advised to add filters and to not call more than one day at a time to avoid rate limiting.

## Token information
Get accessToken with this call:  
https://passio3.com/auth/login?username={username}&password={password}&extended=1

For username and password, contact support@passiotech.com


## API examples
Access Log for Today (JSON)  
https://passio3.com/uga/report/log/log.json?accessToken={token}

Access Log for Today (CSV)  
https://passio3.com/uga/report/log/log/?accessToken={token}

Access Log for data range (JSON)  
https://passio3.com/uga/report/log/log/2023-12-01/2023-12-20.json?accessToken={token}

Access Log for data range (CSV)  
https://passio3.com/uga/report/log/log/2023-12-01/2023-12-20/?accessToken={token}

You can also filter specific data using POST body. For example:  
`{"filter": {"cardId": {"!=": ["",null]}}}`  
Will return only records where the CardId is not null and not empty

You can also filter on multiple items. For example:  
`{"filter": {"stop": {"!=": ["",null]}, "created" : {"from" : "2023-11-11 18:28:00"}}}`  
Will return records with a stop and was created after 6:28pm on Nov 11. Note the seconds are populated. That is important.

### Sample dataset
```
[
    {
        "id": 614157731,
        "date": "2023-11-14",
        "time": "06:01:53",
        "ms": 444,
        "bus": "2018",
        "driver": null,
        "route": "JMU ICS Weekdays",
        "stop": null,
        "eta": null,
        "count": "1",
        "customer": "harrisonburg",
        "device": "APS1-000B91A34C97",
        "passengerType": "APS10",
        "onOff": "on",
        "latitude": "38.454084600",
        "longitude": "-78.853302800",
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
        "userId": "2868",
        "uid": "2023-11-14 06:01:53.444",
        "paxLoad": "1",
        "more": {
            "OOS": 1
        },
        "created": "2023-11-14 06:01:53",
        "datetime": "2023-11-14 06:01:53",
        "zohoStatus": null,
        "cardStatusId": null,
        "eta2": null,
        "routeBlock": "JMU ICS 10",
        "deviceId": "418328",
        "busId": "11358",
        "driverId": null,
        "routeBlockId": "114354",
        "routeStopId": null,
        "passengerTypeId": "26896",
        "trip": null,
        "tripId": null,
        "timePoint": null,
        "timePointId": null,
        "syslogId": null,
        "firmware": null,
        "firmwareId": null,
        "logUpload": null,
        "logUploadId": null,
        "busUpdateLogId": "896953513",
        "createdUtc": "2023-11-14 11:01:53",
        "datetimeUtc": "2023-11-14 11:01:53"
    },
    {
        "id": 614157775,
        "date": "2023-11-14",
        "time": "06:02:12",
        "ms": 991,
        "bus": "2018",
        "driver": null,
        "route": "JMU ICS Weekdays",
        "stop": null,
        "eta": null,
        "count": "1",
        "customer": "harrisonburg",
        "device": "APS1-000B91A34C97",
        "passengerType": "APS10",
        "onOff": "off",
        "latitude": "38.454084100",
        "longitude": "-78.853305600",
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
        "userId": "2868",
        "uid": "2023-11-14 06:02:12.991",
        "paxLoad": "0",
        "more": {
            "OOS": 1
        },
        "created": "2023-11-14 06:02:12",
        "datetime": "2023-11-14 06:02:12",
        "zohoStatus": null,
        "cardStatusId": null,
        "eta2": null,
        "routeBlock": "JMU ICS 10",
        "deviceId": "418328",
        "busId": "11358",
        "driverId": null,
        "routeBlockId": "114354",
        "routeStopId": null,
        "passengerTypeId": "26896",
        "trip": null,
        "tripId": null,
        "timePoint": null,
        "timePointId": null,
        "syslogId": null,
        "firmware": null,
        "firmwareId": null,
        "logUpload": null,
        "logUploadId": null,
        "busUpdateLogId": "896953667",
        "createdUtc": "2023-11-14 11:02:12",
        "datetimeUtc": "2023-11-14 11:02:12"
    }
]
```



