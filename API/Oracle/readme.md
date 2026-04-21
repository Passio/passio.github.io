## ASK (Polling for Assignments and ETAs)

### Overview
A bus periodically requests its current assignment and ETA data.

### Questions Being Answered

#### Assignment
- What stop am I currently at or just completed?
- What route am I operating?
- What trip on that route am I assigned to?

#### ETA
- What are my predicted arrival times for upcoming stops?

### Polling Frequency
- Call every 10 seconds to start
- This can be adjusted based on performance and accuracy needs

### Response Handling

#### ETAs
- Store in `ETA` table
- Use upsert logic:
  - Update if record exists
  - Insert if new

**Primary Key**  
busId + routeStopId + tripId + tripIndex

**Notes**
- `routeStopId` must be derived from: stopId + stopSequence

**Side Effect**
- Each write creates a record in `etaLog`
- `etaLog` is used to evaluate prediction accuracy over time

#### Assignments
[FUTURE] Stored across two tables:

1. `bus`
   - Represents current assignment state
   - Includes last assigned timestamp

2. `busUpdateLog2`
   - Key value history of assignment changes
   - Tracks assignment transitions over time

During the first implementation, assignment data returned by this API will be written to new tables that mirror the existing `bus` and `busUpdateLog2` tables. These tables do not exist yet and will need to be created.

- The new `bus`-like table will store the current assignment state and the last assigned time.
- The new `busUpdateLog2`-like table will store assignment history as a key value record of changes over time.

---

## REGISTER (Declaring Planned Trips)

### Overview
A bus declares which trips it will service for the day.

### Example
BusId: 311  
Trips: [46744, 46745, 46746, 46747, 46748]

### When to Call
- Trigger in the after hook of `bus` update
- Only when `blockId` changes

---

## JSON BUNDLE (Daily Configuration)

### Overview
The transit agency publishes the full set of route and schedule data for the day.

### Contents
- trips.txt
- shapes.txt
- stops.txt
- stop_times.txt

### When to Call
- Every 24 hours at 12:01 AM
- Or whenever configuration is published

---

## How publish config works in Navigator

1. API endpoint
    - `passioTransit/router.js`
    - POST /system/publishConfig calls:publishConf(req.profile, req.body.userId, req.body.outOfService)
        
2. Publish implementation
    - `tdb/type/user/device/deviceEvent/publishConf.js`
    - It does three key things:
        - updates user publish metadata (publishConf, author, timestamps),
        - writes a syslog row with logAction: 'publishConf',
        - creates a deviceEvent per device with name: 'publishConf'.
            

### How to hook into event

2 options:

1. TDB hook on deviceEvent add
    - `tdb/type/user/device/deviceEvent/tdb.js` (add.after)
    - It already handles item.name === 'publishConf' and updates device.lastPublishConf.
    - Will be running in the same app boundary as Navigator
        
2. Realtime subscription (websocket)
    - `tdb/index.js` broadcasts add/update/delete via im.broadcast(...)
    - `im/wss2.js` supports subscribe by type (including deviceEvent, syslog, user)
    - So you can subscribe to:
        - deviceEvent filtered by name: 'publishConf', or
        - syslog filtered by logAction: 'publishConf'.
    - Could be running outside of Navigator


