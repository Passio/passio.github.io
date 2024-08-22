# Passio Log API

## Rate limiting
This API can go back 30 days. It is advised to add filters and to not call more than one day at a time to avoid rate limiting.

## Token information
Get accessToken with this call:  
https://passio3.com/auth/login?username={username}&password={password}&extended=1

For username and password, contact support@passiotech.com

## User names

| Username | Account |
| --- | --- |
|   `SCAD`    |  Previous Savannah     |
|    `SCADatl`   |   Previous Atlanta    |
|    `scadsavannah`   |  New Savannah     |
|   `scadatlanta`    |  New Atlanta     |

## API examples
Access Log for Today (JSON)  
https://passio3.com/{username}/report/log/log.json?accessToken={token}

Access Log for Today (CSV)  
https://passio3.com/{username}/report/log/log/?accessToken={token}

Access Log for data range (JSON)  
https://passio3.com/{username}/report/log/log/2024-03-11/2024-04-11.json?accessToken={token}

Access Log for data range (CSV)  
https://passio3.com/{username}/report/log/log/2024-03-11/2024-04-11/?accessToken={token}

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
    "id": 767332840,
    "date": "2024-08-22",
    "time": "07:03:22",
    "ms": 777,
    "bus": "920",
    "driver": "Anthony Johnson",
    "route": "Yellow Route A Su24",
    "stop": null,
    "eta": null,
    "count": "0",
    "customer": "SCAD",
    "device": "SCAD-35190",
    "passengerType": "one",
    "onOff": "on",
    "latitude": null,
    "longitude": null,
    "speed": "-1",
    "course": null,
    "heading": null,
    "distance": null,
    "cardId": null,
    "locationException": null,
    "address": null,
    "uploadDatetime": "2024-08-22 07:03:23",
    "hash": null,
    "dup": null,
    "userId": "548",
    "uid": "2024-08-22 07:03:22.777",
    "paxLoad": "0",
    "more": {
      "OOS": 1
    },
    "created": "2024-08-22 07:03:23",
    "datetime": "2024-08-22 07:03:22",
    "zohoStatus": null,
    "cardStatusId": null,
    "eta2": null,
    "routeBlock": "Yellow Route A",
    "deviceId": "410693",
    "busId": "1450",
    "driverId": "2210",
    "routeBlockId": "82529",
    "routeStopId": "-1",
    "passengerTypeId": "195",
    "trip": null,
    "tripId": "-1",
    "timePoint": null,
    "timePointId": "-1",
    "syslogId": null,
    "firmware": null,
    "firmwareId": null,
    "logUpload": "2024-08-22 07:03:23",
    "logUploadId": "594809988",
    "busUpdateLogId": "1269946931",
    "createdUtc": "2024-08-22 11:03:23",
    "datetimeUtc": "2024-08-22 11:03:22"
  },
  {
    "id": 767333241,
    "date": "2024-08-22",
    "time": "07:04:20",
    "ms": 172,
    "bus": "607",
    "driver": "Brian Robinson",
    "route": "Silver Route C Su24",
    "stop": "Turner House",
    "eta": null,
    "count": "0",
    "customer": "SCAD",
    "device": "SCAD-35182",
    "passengerType": "one",
    "onOff": "on",
    "latitude": "32.062889099",
    "longitude": "-81.138145447",
    "speed": "16.890239715576172",
    "course": null,
    "heading": null,
    "distance": null,
    "cardId": null,
    "locationException": null,
    "address": null,
    "uploadDatetime": "2024-08-22 07:04:20",
    "hash": null,
    "dup": null,
    "userId": "548",
    "uid": "2024-08-22 07:04:20.172",
    "paxLoad": "0",
    "more": {
      "OOS": 1
    },
    "created": "2024-08-22 07:04:20",
    "datetime": "2024-08-22 07:04:20",
    "zohoStatus": null,
    "cardStatusId": null,
    "eta2": null,
    "routeBlock": "Silver Route C",
    "deviceId": "410660",
    "busId": "10358",
    "driverId": "56289",
    "routeBlockId": "135277",
    "routeStopId": "1305739",
    "passengerTypeId": "195",
    "trip": null,
    "tripId": "-1",
    "timePoint": null,
    "timePointId": null,
    "syslogId": null,
    "firmware": null,
    "firmwareId": null,
    "logUpload": "2024-08-22 07:04:20",
    "logUploadId": "594810681",
    "busUpdateLogId": "1269948106",
    "createdUtc": "2024-08-22 11:04:20",
    "datetimeUtc": "2024-08-22 11:04:20"
  }
]
```



