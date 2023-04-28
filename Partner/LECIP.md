# LECIP - Passio Integration

This document defines how Passio Transit MDT app will send assignment information to LECIP farebox. 

## Key Info

| Key | Value |
| --- | --- |
| Protocal | UDP |
| Connection | Ethernet |
| IP | TBD |
| Port | TBD |
| Format | JSON |
| Frequency | Stop Geofence Entry<br>Every 30 seconds |



## Example Payload
```
{
  "gps": {
    "latitude": 34.832,
    "longitude": -82.3347,
    "speed": 11.2,
    "heading": 270
  },
  "Vehicle": {
    "id": 34773,
    "name": "2046"
  },
  "stop": {
    "id": 1234,
    "name": "GreenvilleLibrary",
    "sequence": 4
  },
  "route": {
    "id": 44566,
    "name": "12GreenvilleExpressOutbound",
    "shortName": "12",
    "color": "#2d9eaf"
  },
  "block": {
    "id": 99688
  },
  "driver": {
    "id": 322,
    "name": "BettyDriver"
  }"trip": {
    "id": 69993
  }
}
```

## Data Dictionary

| Entity |Description |
| --- | --- |
| `gps` | Object that describes geographic position of vehicle |
| `gps.latitude` | Latitude (N/S) in decimal degree format |
| `gps. longitude` | Longitude (E/W) in decimal degree format |
| `gps.speed` | Current speed in meters per second |
| `gps.heading` | Current direction in angular distance relative to north format<br>0-359 |
| `vehicle` | Object that describes this vehicle |
| `vehicle.id` | Internal ID |
| `vehicle.name` | Vehicle name used by agency |
| `stop` | Object that describes the last or current stop |
| `stop.id` | Internal ID. Can be resolved with GTFS `stops.txt` |
| `stop.name` | Text name of stop |
| `stop.sequence` | Stop order |
| `route` | The current route that is being ran by this vehicle |
| `route.id` | Internal ID |
| `route.name` | Long name. Used where there is room |
| `route.shortName` | Used in compact environments |
| `route.color` | Used to as background color in graphical settings |
| `block` | Object that describes the piece of work this vehicle is doing |
| `block.id` | Internal ID. Can be resolved in GTFS `trips.txt` |
| `driver` | Object that describes the person operating the vehicle |
| `driver.id` | Internal ID |
| `driver.name` | First and last name |
| `trip` | Object that describes the current trip being performed |
| `trip.id` | Internal ID. Can be resolved in GTFS `trips.txt` |
