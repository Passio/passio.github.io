# Introduction

This document will highlight the best practices and usage for Passio Connect

Dispatch dashboard - https://dispatch.passioconnect.com  
Beta version - https://dispatch-beta.passioconnect.com

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
1. Select name
2. Click On Demand
3. If the manifest is not shown:
    1. Click Show Hidden
    2. Find the Route for the driver that does not have information about another bus or another driver. The "blank" one will be theirs. Click that route and the manifest will show. If there are assigned trips, those will be shown in 30 seconds or so.

[^1]: One or more services can be associated with an assignment. This is useful when running multiple rider services at one time. In the future, the autoschedule engine will use this for trip assignments.
[^2]: If you want control over when a specific assignment will start or when it will end, use these dates and the assignment will only be visible during those times. Most of the time, these can be left on their default values.
