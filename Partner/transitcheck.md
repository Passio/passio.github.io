## Introduction

Passio uses TDB for API access. This involves an HTTP POST with JSON Body. The verb is in the URL.

## Access Token information

user: {Get from TBD}
pass: {Get from TBD}

Change Password here:
https://passio3.com

Get accessToken with this call:
https://passio3.com/auth/login?username={username}&password={password}&extended=1

## Driver Example

Shows driver name, userId and PIN from UGA where TransitCheck ID is 1683 or 1657
| Parameter | Value |
| --- | --- |
| URL | https://passio3.com/tdb/get/?accessToken={accessToken} |
| Method | POST |
| Body | `{ "type" : "driver", "userId" : 3994, "field" : ["name", "transitCheckUser", "transitCheckPin"], "filter" : {"transitCheckUser" : ["1683", "1657"]}}` |

### Result:

```
[
    {
        "type": "driver",
        "name": "Cam Jordan csj62560",
        "transitCheckUser": "1657",
        "transitCheckPin": "123456"
    },
    {
        "type": "driver",
        "name": "Clint Schuler cds95405",
        "transitCheckUser": "1683",
        "transitCheckPin": "123456"
    }
]
```

---

Shows driver info from UGA where TransitCheck ID is 1683 or 1657
| Parameter | Value |
| --- | --- |
| URL | https://passio3.com/tdb/get/?accessToken={accessToken} |
| Method | POST |
| Body | `{ "type" : "driver", "userId" : 3994, "filter" : {"transitCheckUser" : ["1683", "1657"]}}` |

### Result:
```
[
    {
        "type": "driver",
        "id": "28650",
        "name": "Cam Jordan csj62560",
        "userId": "3994",
        "email": null,
        "hideOnDevice": 0,
        "archive": 0,
        "pin": null,
        "testPassed": 0,
        "publicName": null,
        "luminatorCode": null,
        "available": 1,
        "phone": null,
        "paraPlanId": null,
        "firstName": "Cam",
        "lastName": "Jordan",
        "externalId": null,
        "training": 0,
        "allowOverlap": null,
        "image": null,
        "fareboxCode": null,
        "imageLength": null,
        "transitCheckUser": "1657",
        "transitCheckPin": "123456",
        "onDemandIsPaused": 0,
        "driverLicense": [],
        "onDemandDriverPauseLog": []
    },
    {
        "type": "driver",
        "id": "39144",
        "name": "Clint Schuler cds95405",
        "userId": "3994",
        "email": null,
        "hideOnDevice": 0,
        "archive": 0,
        "pin": null,
        "testPassed": 0,
        "publicName": null,
        "luminatorCode": null,
        "available": 1,
        "phone": null,
        "paraPlanId": null,
        "firstName": null,
        "lastName": null,
        "externalId": null,
        "training": 0,
        "allowOverlap": null,
        "image": null,
        "fareboxCode": null,
        "imageLength": null,
        "transitCheckUser": "1683",
        "transitCheckPin": "123456",
        "onDemandIsPaused": 0,
        "driverLicense": [],
        "onDemandDriverPauseLog": []
    }
]
```

---

Combine attributes to AND filter on multiple attributes\
Shows driver info from UGA where TransitCheck ID is 1657 and PIN is 123456
| Parameter | Value |
| --- | --- |
| URL | https://passio3.com/tdb/get/?accessToken={accessToken} |
| Method | POST |
| Body | `{ "type" : "driver", "userId" : 3994, "field" : ["name", "transitCheckUser", "transitCheckPin"], "filter" : { "transitCheckUser" : "1657", "transitCheckPin" : "123456"}}` |

### Result:
```
[
    {
        "type": "driver",
        "name": "Cam Jordan csj62560",
        "transitCheckUser": "1657",
        "transitCheckPin": "123456"
    }
]
```


## Vehicles Examples

Shows vehicle info from UGA where TransitCheck ID is 95129
| Parameter | Value |
| --- | --- |
| URL | https://passio3.com/tdb/get/?accessToken={accessToken} |
| Method | POST |
| Body | `{ "type" : "bus", "userId" : 3994, "field" : "name", "filter" : { "transitCheckVehicleId" : "95129"}}` |

### Result:
```
[
    {
        "type": "bus",
        "name": "95129"
    }
]
```





