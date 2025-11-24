## Communication Protocol Specification

### 1. Overview
The onboard **MDT** communicates with **network connected devices** using a lightweight UDP-based protocol over a **closed Ethernet network**.  
Messages are pushed periodically in a “set-it-and-forget-it” manner, containing redundant JSON data describing the vehicle, route, and stop information.

---

### 2. Message Format

`[PROTOCOL_IDENTIFIER][FUNCTION][COUNT][LOAD][CHECKSUM]`


| Field | Description | Type | Notes |
|-------|--------------|------|-------|
| **Protocol Identifier** | Fixed ASCII string identifying protocol version | BYTE[7] | `"PASMPM1"` |
| **Function** | Message type identifier | BYTE | `0x01` = JSON |
| **Count** | Number of bytes in LOAD (big-endian) | DWORD | Any |
| **Load** | JSON payload | BYTE[] | Contains structured data |
| **Checksum** | CRC check | BYTE | Implementation-specific |

---

### 3. JSON Payload Schema

#### **Vehicle Object**
| Field | Type | Notes |
|-------|------|-------|
| driver_id | string | optional |
| driver_is_logged_on | boolean | `"true"` / `"false"` |
| heading | float | 0–360, only if GPS locked |
| gps_is_locked | boolean | required for heading, speed, location |
| gps_report_time | object | see *DateTimeOffset* |
| location | object | see *Location* |
| next_stop_requested | boolean | cleared on door open |
| on_route_status | enum | see *OnRouteStatus* |
| speed | float | meters per second |
| vehicle_name | string | optional |

#### **Task Object**
| Field | Type | Notes |
|-------|------|-------|
| destination_name | string | if on trip |
| direction_name | string | if on trip |
| next_stops | array\<Stop\> | up to 5, if on trip |
| pattern_id / name | string | if on trip |
| route_id / name | string | if on trip |
| task_type | enum | see *TaskType* |

#### **Stop Object**
| Field | Type | Notes |
|-------|------|-------|
| connected_routes | array\<ConnectedRoute\> | see below |
| estimated_arrive_time | DateTimeOffset | includes time zone bias |
| location | Location | approximate stop location |
| scheduled_arrive_time | DateTimeOffset | includes time zone bias |
| stop_code / name | string | any |
| stop_rank | uint32 | order along route |

#### **ConnectedRoute Object**
| Field | Type | Notes |
|-------|------|-------|
| connected_patterns | array\<ConnectedPattern\> | see below |
| route_id / name | string | any |

#### **ConnectedPattern Object**
| Field | Type | Notes |
|-------|------|-------|
| pattern_destination / direction | string | any |
| pattern_id / name | string | any |

#### **DateTimeOffset Object**
| Field | Type | Notes |
|-------|------|-------|
| time_zone_bias | int32 | −720 to +720 min |
| unix_time | uint64 | seconds since epoch |

#### **Location Object**
| Field | Type | Notes |
|-------|------|-------|
| latitude | float | −90 to 90 |
| longitude | float | −180 to 180 |

---

### 4. Enums

#### **OnRouteStatus**
- `on_route`
- `off_route`
- `no_gps_lock`
- `no_route`

#### **TaskType**
- `free`
- `no_active_task`
- `off_duty`
- `special_event`
- `trip`
- `tripper`
- `vehicle_check`

---

### 5. Workflow Summary
- The MDT sends UDP packets every 15 seconds.  
- Each message includes:
  - Vehicle telemetry (GPS lock required for heading, location, speed)
  - Timestamp of the last valid GPS report
  - Current task information (no next task)
  - Next five stops (only if on trip and on-route)

---

### 6. Example JSON Payload
```json
{
  "task": {
    "destination_name": "Greenlink Transit Center",
    "direction_name": "Outbound",
    "next_stops": [
      {
        "connected_routes": [
          {
            "connected_patterns": [
              {
                "pattern_destination": "Greenlink Transit Center",
                "pattern_direction": "Outbound",
                "pattern_id": "GLK001",
                "pattern_name": "Route 1 - Pendleton Street"
              }
            ],
            "route_id": "R1",
            "route_name": "Pendleton Street"
          }
        ],
        "estimated_arrive_time": {
          "time_zone_bias": "-300",
          "unix_time": "1732459200"
        },
        "location": {
          "latitude": "34.847244",
          "longitude": "-82.402132"
        },
        "scheduled_arrive_time": {
          "time_zone_bias": "-300",
          "unix_time": "1732459140"
        },
        "stop_code": "1001",
        "stop_name": "Greenlink Transit Center",
        "stop_rank": "1"
      },
      {
        "estimated_arrive_time": {
          "time_zone_bias": "-300",
          "unix_time": "1732459500"
        },
        "location": {
          "latitude": "34.841772",
          "longitude": "-82.405821"
        },
        "scheduled_arrive_time": {
          "time_zone_bias": "-300",
          "unix_time": "1732459440"
        },
        "stop_code": "1002",
        "stop_name": "Pendleton & Academy",
        "stop_rank": "2"
      },
      {
        "estimated_arrive_time": {
          "time_zone_bias": "-300",
          "unix_time": "1732459800"
        },
        "location": {
          "latitude": "34.835981",
          "longitude": "-82.411230"
        },
        "scheduled_arrive_time": {
          "time_zone_bias": "-300",
          "unix_time": "1732459740"
        },
        "stop_code": "1003",
        "stop_name": "Augusta & Main",
        "stop_rank": "3"
      }
    ],
    "pattern_id": "GLK001",
    "pattern_name": "Route 1 - Pendleton Street",
    "route_id": "R1",
    "route_name": "Pendleton Street",
    "task_type": "trip"
  },
  "vehicle": {
    "driver_id": "84",
    "driver_is_logged_on": true,
    "heading": 180.0,
    "gps_is_locked": true,
    "gps_report_time": {
      "time_zone_bias": "-300",
      "unix_time": "1732459100"
    },
    "location": {
      "latitude": "34.848472",
      "longitude": "-82.401952"
    },
    "next_stop_requested": false,
    "on_route_status": "on_route",
    "speed": 12.4,
    "vehicle_name": "GTA_1203"
  }
}
