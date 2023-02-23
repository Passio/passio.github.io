# CNRL information for Passio Log API

username: {Get from Todd}  
password: {Get from Todd}
  
  
### Accounts Enabled for CNRL
  
| Account  | User | UserID |
| ------------- | ------------- | --- |
| Canadian Natural Resources Limited (CNRL)  | cnrl | 2768 |


Change Password here:  
https://passio3.com

Get accessToken with this call:  
https://passio3.com/auth/login?username={username}&password={password}&extended=1

Access Log for Today (JSON)  
https://passio3.com/cnrl/report/log/log.json?accessToken={token}

Access Log for Today (CSV)  
https://passio3.com/cnrl/report/log/log/?accessToken={token}

Access Log for data range (JSON)  
https://passio3.com/cnrl/report/log/log/2023-02-01/2023-02-04.json?accessToken={token}

Access Log for data range (CSV)  
https://passio3.com/cnrl/report/log/log/2023-02-01/2023-02-04/?accessToken={token}

You can also filter specific data using POST body. For example:  
`{"filter": {"cardId": {"!=": ["",null]}}}`  
Will return only records where the CardId is not null and not empty

You can also filter on multiple items. For example:  
`{"filter": {"cardId": {"!=": ["",null]}, "created" : {"from" : "2023-02-22 18:28:00"}}}`  
Will return records with a CardId and was created after 6:28pm on Feb 22. Note the seconds are populated. That is important.

### Sample dataset
```
[
    {
        "id": 496618040,
        "date": "2023-02-21",
        "time": "03:56:44",
        "ms": 558,
        "bus": "66222",
        "driver": "Solomon Kidane",
        "route": "MRM - FMM AM M-Th Mainline 4B",
        "stop": "MRM Truck Shop",
        "eta": "06:10",
        "count": "1",
        "customer": "cnrl",
        "device": "CNRL-968408",
        "passengerType": "98",
        "onOff": "on",
        "latitude": "56.659370422",
        "longitude": "-111.147125244",
        "speed": "0.03086666576564312",
        "course": null,
        "heading": null,
        "distance": null,
        "cardId": "478446",
        "locationException": null,
        "address": null,
        "uploadDatetime": "2023-02-21 04:01:31",
        "hash": null,
        "dup": null,
        "userId": "2768",
        "uid": "2023-02-21 03:56:44.558",
        "paxLoad": "1",
        "more": null,
        "created": "2023-02-21 04:01:31",
        "datetime": "2023-02-21 03:56:44",
        "zohoStatus": null,
        "cardStatusId": "98",
        "eta2": null,
        "routeBlock": "MRM - FMM AM M-Th Mainline 4B",
        "deviceId": "419673",
        "busId": "11478",
        "driverId": "21128",
        "routeBlockId": "98593",
        "routeStopId": "1053808",
        "passengerTypeId": "25299",
        "trip": null,
        "tripId": "491593",
        "timePoint": null,
        "timePointId": "9298520",
        "syslogId": null,
        "firmware": null,
        "firmwareId": null,
        "logUpload": "2023-02-21 04:01:31",
        "logUploadId": "234500761",
        "busUpdateLogId": "639990043",
        "createdUtc": "2023-02-21 11:01:31",
        "datetimeUtc": null
    },
    {
        "id": 496621598,
        "date": "2023-02-21",
        "time": "04:20:22",
        "ms": 861,
        "bus": "66222",
        "driver": "Solomon Kidane",
        "route": "MRM - FMM AM M-Th Mainline 4B",
        "stop": "6028",
        "eta": null,
        "count": "1",
        "customer": "cnrl",
        "device": "CNRL-968408",
        "passengerType": "98",
        "onOff": "on",
        "latitude": "56.674304962",
        "longitude": "-111.332435608",
        "speed": "0.048872221261262894",
        "course": null,
        "heading": null,
        "distance": null,
        "cardId": "469694",
        "locationException": null,
        "address": null,
        "uploadDatetime": "2023-02-21 04:20:27",
        "hash": null,
        "dup": null,
        "userId": "2768",
        "uid": "2023-02-21 04:20:22.861",
        "paxLoad": "4",
        "more": null,
        "created": "2023-02-21 04:20:27",
        "datetime": "2023-02-21 04:20:22",
        "zohoStatus": null,
        "cardStatusId": "98",
        "eta2": null,
        "routeBlock": "MRM - FMM AM M-Th Mainline 4B",
        "deviceId": "419673",
        "busId": "11478",
        "driverId": "21128",
        "routeBlockId": "98593",
        "routeStopId": "1053832",
        "passengerTypeId": "25299",
        "trip": null,
        "tripId": "491593",
        "timePoint": null,
        "timePointId": "-1",
        "syslogId": null,
        "firmware": null,
        "firmwareId": null,
        "logUpload": "2023-02-21 04:20:27",
        "logUploadId": "234507235",
        "busUpdateLogId": "639999231",
        "createdUtc": "2023-02-21 11:20:27",
        "datetimeUtc": null
    }
]
```



