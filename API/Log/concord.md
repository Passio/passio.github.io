# Concord information for Passio Log API

username: {Get from Agency}  
password: {Get from Agency}
  

Get accessToken with this call:  
https://passio3.com/auth/login?username={username}&password={password}&extended=1

Access Log for Today (JSON)  
https://passio3.com/concordk/report/log/log.json?accessToken={token}

Access Log for Today (CSV)  
https://passio3.com/concordk/report/log/log/?accessToken={token}

Access Log for data range (JSON)  
https://passio3.com/concordk/report/log/log/2023-02-01/2023-02-04.json?accessToken={token}

Access Log for data range (CSV)  
https://passio3.com/concordk/report/log/log/2023-02-01/2023-02-04/?accessToken={token}

You can also filter specific data using POST body. For example:  
`{"filter": {"onOff": {"=": ["on","off"]}}}`  
Will return only records where the onOff field is populated

You can also filter on multiple items. For example:  
`{"filter": {"onOff": {"=": ["on","off"]}, "created" : {"from" : "2023-03-11 18:28:00"}}}`  
Will return  records where the onOff field is populated and the record was created after 6:28pm on March 11. Note the seconds are populated. That is important.

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



