# Information for Passio Telematic API

username: {Get from Rusty}  
password: {Get from Rusty}
  
  
### Accounts Enabled for User
  
| Account  | User | UserID |
| ------------- | ------------- | --- |
| City of Billings MET Transit | billings | 3901 |


Change Password here:  
https://passio3.com

Get accessToken with this call:  
https://passio3.com/auth/login?username={username}&password={password}&extended=1

Access Telematic Log for Today (JSON)  
https://passio3.com/billings/report/log/telematicLog.json?accessToken={token}

Access Telematic Log for Today (CSV)  
https://passio3.com/billings/report/log/telematicLog/?accessToken={token}

Access Telematic Log for data range (JSON)  
https://passio3.com/billings/report/log/telematicLog/2023-02-01/2023-02-04.json?accessToken={token}

Access Telematic Log for data range (CSV)  
https://passio3.com/billings/report/log/telematicLog/2023-02-01/2023-02-04/?accessToken={token}

You can also filter specific data using POST body. For example:  
`{"filter": {"busId": 9855}}`  
Will return data for the busId of 9855

### Sample dataset
```
{
        "id": "61690169",
        "userId": "2283",
        "created": "2023-02-09 05:43:52",
        "deviceId": "415789",
        "busId": "12894",
        "locationId": "9287105340",
        "odometer": 19884390,
        "eventCode": 152,
        "datetime": "2023-02-09 05:43:52",
        "createdUtc": "2023-02-09 11:43:52",
        "datetimeUtc": null,
        "hdop": 9,
        "rssi": -56,
        "satellites": 11,
        "engineTemp": 85,
        "engineSpeedRpm": 998.5,
        "dtcCount": 0,
        "engineRunTime": 0,
        "fuelLevelPct": 100,
        "maxThrottlePosition": 0,
        "minBatteryVoltage": 27.7,
        "fuelType": 0
    }
```
