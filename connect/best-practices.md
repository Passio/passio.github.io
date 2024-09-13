# Introduction

This document will highlight the best practices and usage for Passio Connect

## Important Links
Dispatch dashboard - https://dispatch.passioconnect.com  
Beta version - https://dispatch-beta.passioconnect.com  
[Product Roadmap](https://docs.google.com/spreadsheets/d/18iymPnGkeL0na0wA71oNjePomudTgxhVxNo4TivmnyI/edit?usp=sharing)

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
1. Edit Assignment (pencil icon)
2. Clear the Name field (if populated)
3. Set the Vehicle to "No Assignment" (very top of list)
4. Set the Driver to "No Assignment" (very top of list)
5. Slide the driver active to grey
6. Make sure any active assigned trips left in the list are reassigned

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

## Driver login on MDT
> [!IMPORTANT]
> These instructions are for version 39.21. [Update instructions here](#How-to-update-MDT-version)
1. Select Driver Name 
2. Click On Demand
3. The "Start Service" Screen will show
> [!TIP]
> If the Start service screen does not show  
> 1. Click Show Hidden
> 2. Find the Route for the driver that does not have information about another bus or another driver. The "blank" one will be theirs. Click that route and the manifest will show. If there are assigned trips, those will be shown in 30 seconds or so.
  
4. Tap on Start Service
5. See Trips to be performed or "Awaiting Trips" if none are assigned yet.



## How to update MDT version
> [!IMPORTANT]
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
