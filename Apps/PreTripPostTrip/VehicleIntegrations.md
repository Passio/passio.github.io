# Vehicle Integration Spec

Passio Inspector can integrate with an agency's vehicle list. To do this, we need a URL that we can GET that contains JSON that adheres to the following spec.

Here is a working URL that conforms to this spec:  
https://app.passiotransit.com/api/v1/Internal/VehicleIntegration

Here is a working API call that pulls data from Demo Account:  
https://app.passiotransit.com/api/v1/Internal/Vehicles?agency=4

The agency can be changed to any userId in Passio3.  
Swagger Docs are available here (Scroll to Internal section):  
https://app.passiotransit.com/swagger/index.html



Current spec version 1.0, August 22, 2022
|      Property     |  Type  | Mandatory |                       Description                      |
|:-----------------:|:------:|:---------:|:------------------------------------------------------:|
| name              | string |    Yes    | Friendly name of vehicle                               |
| id                | string |    Yes    | Internal id of vehicle. Must be unique in json payload |
| description       | string |     No    | Additional information to describe the vehicle         |
| manufacturer      | string |     No    | Vehicle manufacturer (Proterra)                        |
| model             | string |     No    | Vehicle model (ZX5)                                    |
| yearOfManufacture | string |     No    | Year of manufacture (2021)                             |
| vin               | string |     No    | Vehicle Identification Number                          |
| doorCount         | int    |     No    | Number of rider facing doors                           |
| color             | string |     No    | Hexcode format (#2d9eaf)                               |
| adaAccessible     | bool   |     No    | If the vehicle is ADA accessible                       |
| more              | json   |     No    | Additional metadata to be included in submission       |



Here is an example of valid data:
```
[
  {
    "name": "311",
    "id": "ef442a98-216e-4e71-8a99-703b7ff90f30",
    "description": "2021 Proterra with Ramp",
    "manufacturer": "Proterra",
    "model": "ZX5",
    "yearOfManufacture": "2021",
    "vin": "1G8ZF5287XZ363384",
    "doorCount": 2,
    "color": "#2d9eaf",
    "adaAccessible": true,
    "more": "{\"stringKey\" : \"stringValue\", \"intKey\" : 311 }"
  },
  {
    "name": "420",
    "id": "42bf2c79-1cb2-4e21-b78b-916843d30538",
    "description": "2019 NewFlyer",
    "manufacturer": "New Flyer",
    "model": "Xcelsior",
    "yearOfManufacture": "2019",
    "vin": "2S3DA417576128786",
    "doorCount": 2,
    "color": "#2d9eaf",
    "adaAccessible": true
  }
]
```



