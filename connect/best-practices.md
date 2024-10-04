# Introduction

This document will highlight the best practices and usage for Passio Connect

## Important Links
Dispatch dashboard - https://dispatch.passioconnect.com  
Beta version - https://dispatch-beta.passioconnect.com  
[Product Roadmap](https://docs.google.com/spreadsheets/d/18iymPnGkeL0na0wA71oNjePomudTgxhVxNo4TivmnyI/edit?usp=sharing)


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
2. Click On Demand
3. The "Start Service" Screen will show
> If the Start service screen does not show  
> 1. Click Show Hidden
> 2. Find the Route for the driver that does not have information about another bus or another driver. The "blank" one will be theirs. Click that route and the manifest will show. If there are assigned trips, those will be shown in 30 seconds or so.
  
4. Tap on Start Service
5. See Trips to be performed or "Awaiting Trips" if none are assigned yet.


## How to use the map on MDT

To access the map, the driver must be using version 40.03 or later. Then, they can tap the Map icon located under the "New Ladder" text.  
<img width="159" alt="Screenshot 2024-09-19 at 8 29 15 AM" src="https://github.com/user-attachments/assets/e483e9cc-0e72-4012-8ff8-0d05a6b3c891">

The map will automatically load based on the driver's current location. The manifest remains visible but appears in a smaller format, allowing the driver to view both the map and their stops.  
<img width="350" alt="Screenshot 2024-09-19 at 8 36 26 AM" src="https://github.com/user-attachments/assets/8a91f8e3-63c4-4ec8-8643-fe3dc7781acd">

To view trip details on the map, the driver can select a stop from the manifest and tap "Show on Map." The map will then zoom out to display both the pickup and drop-off locations for that trip. The driver can use the standard two-finger gesture to zoom or pan the map as needed.  
<img width="350" alt="Screenshot 2024-09-19 at 8 39 51 AM" src="https://github.com/user-attachments/assets/cfeb240c-8d61-4182-8b65-a7b957635c97">

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

  
---

[^1]: One or more services can be associated with an assignment. This is useful when running multiple rider services at one time. In the future, the autoschedule engine will use this for trip assignments.
[^2]: If you want control over when a specific assignment will start or when it will end, use these dates and the assignment will only be visible during those times. Most of the time, these can be left on their default values.
