# Introduction

This document will highlight the best practices and usage for Passio Connect

## Important Links
Dispatch dashboard - https://dispatch.passioconnect.com  
Beta version - https://dispatch-beta.passioconnect.com  
[Product Roadmap](https://docs.google.com/spreadsheets/d/18iymPnGkeL0na0wA71oNjePomudTgxhVxNo4TivmnyI/edit?usp=sharing)

### Need Assistance?

For immediate support, please contact us at [support@passiotech.com](mailto:support@passiotech.com). We're here to help!

## Recent updates
- Drivers can now get SMS notifications  
- Dispatch will now ding when there is a new trip

## Route Assignment (editing existing)
1. Edit Assignment (Pencil icon)
2. Set the name (if desired - will default to route name)
3. Set the Route
4. Set the Vehicle
5. Set the Driver
6. Set the Services if needed[^1]
7. Set the start and end date if needed[^2]
8. Click Save Changes
9. Make sure the active driver slider is green if the driver is ready to be assigned trips.

## End of driver shift (done by dispatcher)
1. Cancel or reassign any trips in the list
2. Close assignment  
   - If you want to reuse the assignment in the future, click the "Remove driver and vehicle" button (clear icon) which will un-assign the driver and vehicle.  
   - If you will not reuse the assignment, click the "Remove assignment" button (trash can) to remove the assignment.


## Route Assignment (creating  new if needed)
1. Click New Assignment
2. Set the name (if desired - will default to route name)
3. Set the Route
4. Set the Vehicle
5. Set the Driver
6. Set the Services, if needed[^1]
7. Set the start and end date, if needed[^2]
8. Click Save Changes
9. Make sure the active driver slider is green if the driver is ready to be assigned trips.

## Auto Update Manifest (beta)
<img width="361" alt="Screenshot 2025-01-03 at 8 01 49 AM" src="https://github.com/user-attachments/assets/1546147e-89d6-4edd-b692-8c0acff7be60" />

When a new trip is assigned, the system intelligently reorders trips for optimal execution. Pick up and drop off times are automatically updated to reflect the new sequence, ensuring a seamless experience. Riders will see the updated ETAs in the app in real time. To enable this functionality for a specific assignment, simply check the ‘Auto Update Manifest’ option in the Assignment details.

## Driver notifications

<img width="420" alt="Screenshot 2024-09-19 at 8 29 15 AM" src="https://github.com/user-attachments/assets/b6d23ca0-8c27-4dc0-9974-861ddbdb47d1">

The MDT will automatically ding and say "New Ride Requested" when there is a new trip.  
If a driver will not always be at their vehicle, or they would like an additional notification, a SMS can be sent to their phone.  
Here is how to enable SMS notifications:  
1. In Passio Navigator, click Configuration, then Services
2. Select the Service to enable for SMS notifications, the Service details will open in the right hand drawer
3. Enable the "Send SMS on new Trip" checkbox
4. In the top menu bar of Configuration, click Drivers
5. For each Driver that would like SMS notifications
    1. Click their name in the list, the Driver details will open in the right hand drawer
    2. Enter their phone number in the Phone field
    3. Click Save

## Driver login on MDT
> These instructions are for version 40.06 or newer. [Update instructions here](#How-to-update-MDT-version)
1. Select Driver Name 
2. Make sure the MDT is showing the Route list instead of the Grid view. Then tap On Demand
3. The "Start Service" Screen will show
> If the Start service screen does not show  
> 1. Click Show Hidden
> 2. Find the Route for the driver that does not have information about another bus or another driver. The "blank" one will be theirs. Click that route and the manifest will show. If there are assigned trips, those will be shown in 30 seconds or so.
  
4. Tap on Start Service
5. See Trips to be performed or "Awaiting Trips" if none are assigned yet.

> When selecting an On Demand route, ensure that the MDT displays routes in a list format rather than a grid. Using the grid view may cause trips to display incorrectly on the MDT. We are currently working on a software update to automatically prevent the grid view from appearing when On Demand is selected.

## How to use the map on MDT

To access the map, the driver must be using version 40.03 or later. Then, they can tap the Map icon located under the "New Ladder" text.  
<img width="159" alt="Screenshot 2024-09-19 at 8 29 15 AM" src="https://github.com/user-attachments/assets/e483e9cc-0e72-4012-8ff8-0d05a6b3c891">

The map will automatically load based on the driver's current location. The manifest remains visible but appears in a smaller format, allowing the driver to view both the map and their stops.  
<img width="350" alt="Screenshot 2024-09-19 at 8 36 26 AM" src="https://github.com/user-attachments/assets/8a91f8e3-63c4-4ec8-8643-fe3dc7781acd">

To view trip details on the map, the driver can select a stop from the manifest and tap "Show on Map." The map will then zoom out to display both the pickup and drop-off locations for that trip. The driver can use the standard two-finger gesture to zoom or pan the map as needed.  
<img width="350" alt="Screenshot 2024-09-19 at 8 39 51 AM" src="https://github.com/user-attachments/assets/cfeb240c-8d61-4182-8b65-a7b957635c97">


---

## Using the MDT to Capture Walk-Up Riders

<img width="689" alt="Screenshot 2024-11-13 at 2 57 42 PM" src="https://github.com/user-attachments/assets/8155f95a-5161-479f-9435-22a0cc9f4136">


Walk-up riders are an essential part of on-demand transportation. Here’s how to effectively capture walk-up riders and integrate them into your on-demand system:

Step 1: Rider Boards the Vehicle
- When a rider gets on the vehicle, tap 'Type' on the MDT to access the passenger type screen. This screen allows you to categorize different passenger types, including walk-up riders.

Step 2: Confirm Settings
- Double-check that 'Count on tap' is unchecked. This ensures that you will manually log each rider as they board and exit, which is important for tracking individual walk-up riders accurately.

Step 3: Assign a Walk-Up Rider Icon
- Tap one of the available rider icons to represent the walk-up rider. There are three unique icons specifically used to represent individual walk-up riders. This is crucial for tracking multiple walk-up riders effectively. After selecting an icon, tap 'ON' in the upper right-hand corner to confirm the rider's boarding status.

Step 4: Remember Icon Assignment
- Make a mental note of which icon represents the rider. Properly remembering icon assignments is crucial, especially when multiple walk-up riders are on board, to avoid confusion and ensure accurate data entry.

Step 5: Dropping Off a Walk-Up Rider
- When the rider reaches their destination, tap the same rider icon that represents that rider and then tap 'OFF' in the lower right-hand corner. This action logs the completion of the trip for that specific rider.

Step 6: Handling Multiple Walk-Up Riders
- If another walk-up rider boards the vehicle while an existing walk-up rider is still on board, select one of the remaining two available icons to represent this new rider. Each walk-up rider must have a unique icon to ensure clear tracking of their journey.


## How to update MDT version

> If you have a BYOD, or tablet with Google Play, ONLY install the version that ends in _GP. If you have a Passio MDT, do NOT use the version that ends in _GP
1. Click Hardware Menu button
2. Tap "Preferences"
3. Enter PIN
4. Tap "Updates and Addons"
5. Tap "Firmware updates"
6. Tap "List all Passio Transit Versions and addons"
7. Wait for the list to load from server
8. Tap the desired version and follow prompts to install


# On-Demand Ridership Reporting in Navigator

We now support multiple ways of capturing on-demand ridership in Navigator. These updates mean that any fixed route report that includes ridership metrics will also work with on-demand trips.

There are two supported methods for including passenger type data in reports:

### Option 1 – Service-level passenger type
When a rider is picked up or dropped off, the system automatically records an 'on' or 'off' count using the passenger type configured for the service.

### Option 2 – Operator-level passenger type
When a rider is picked up, the operator must manually select the passenger type.

To track alightings:
- Uncheck ‘Count on Tap’
- Select the passenger type
- Tap 'Off' at the time of drop-off

Configuration depends on agency needs. Use the following scenarios to guide setup:

---

## Type 1 – Pure On-Demand, Trip Count Only

1. Create a passenger type called **On Demand Rider**.
   - If the agency uses only on-demand or wants to combine fixed route and on-demand data, check the **Report** checkbox so it appears in reports.
2. Set the on-demand service's passenger type to **On Demand Rider**.

> ✅ No manual input needed by operators. Counts will automatically appear in Navigator.

---

## Type 2 – On-Demand + Accessibility Service

1. Create two passenger types:
   - One for general public (e.g., `General Public`, `Student`)
   - One for accessibility services (e.g., `ADA`, `Paratransit`)
2. Check **Report** for each based on reporting needs.
3. Assign the correct passenger type to each service.

> ✅ Counts auto-logged when riders are picked up or dropped off.

---

## Type 3 – Detailed Passenger Type Tracking Across Services

1. Create a passenger type called **On Demand Rider** and uncheck **Report**.
2. Assign this as the default for all on-demand services.
3. Create additional passenger types for each tracked group (e.g., `Student`, `Veteran`, `Elderly`).
   - Ensure **Device** is checked so the type appears on the MDT.
   - Check **Report** if you want it included in standard ridership reports.

### Operator Workflow
For boarding:
1. Tap `Passenger Type`
2. Select the appropriate rider type
3. Tap `On`

For alighting (optional):
1. Tap `Passenger Type`
2. Select the rider type again
3. Tap `Off`

> 💡 To simplify boarding only (no drop-offs), enable `Count on Tap` in passenger type settings.
  
---

[^1]: One or more services can be associated with an assignment. This is useful when running multiple rider services at one time. In the future, the autoschedule engine will use this for trip assignments.
[^2]: If you want control over when a specific assignment will start or when it will end, use these dates and the assignment will only be visible during those times. Most of the time, these can be left on their default values.
