# Information for Passio TSP API

username: {Get from Cameron}  
password: {Get from Cameron}
  
  
### Accounts Enabled for User
  
| Account  | User | UserID |
| ------------- | ------------- | --- |
| NC State University | ncstateuni | 3827 |


Change Password here:  
https://passio3.com

Get accessToken with this call:  
https://passio3.com/auth/login?username={username}&password={password}&extended=1

Access Telematic Log for Today (JSON)  
https://passio3.com/ncstateuni/report/log/tspAdherenceLog.json?accessToken={token}

Access Telematic Log for Today (CSV)  
https://passio3.com/ncstateuni/report/log/tspAdherenceLog/?accessToken={token}

Access Telematic Log for data range (JSON)  
https://passio3.com/ncstateuni/report/log/tspAdherenceLog/2025-03-01/2025-03-11.json?accessToken={token}

Access Telematic Log for data range (CSV)  
https://passio3.com/ncstateuni/report/log/tspAdherenceLog/2025-04-01/2025-03-11/?accessToken={token}

You can also filter specific data using POST body. For example:  
`{"filter": {"busId": 13898}}`  
Will return data for the busId of 13898

### Sample dataset
```
{
    "id": "124255",
    "userId": "3827",
    "created": "2025-03-01 08:12:04",
    "createdUtc": "2025-03-01 13:12:04",
    "adherence": "-17.916666667",
    "threshold": "4.000000000",
    "busId": "13898",
    "routeBlockId": "157819",
    "blockId": "33281",
    "tripId": "843527"
}
```
