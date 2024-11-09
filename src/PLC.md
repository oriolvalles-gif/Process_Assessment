# PLC

In this project, we’ve developed two tasks that work in tandem to control access to a secure area and manage elevator usage based on granted access. 

Task 1 is responsible for verifying access permissions, ensuring that only authorized users can initiate entry. By validating an access card, Task 1 sets a limited window during which access is granted. 

Task 2 then builds on this by coordinating elevator movement: once access is approved and an elevator request is made, Task 2 ensures that the elevator arrives at the designated floor, completing a controlled, secure entry process.

*-Explanation of Task 1*

Task 1 handles access control for entry. It checks if a valid access card is scanned by reading the bCardScanned and bCardValid variables from the GVL. 
If both conditions are true, it sets bAccessGranted to TRUE in the GVL, indicating authorized entry, and starts a timer (tmrAccess). 
When this timer finishes, bAccessGranted is reset to FALSE, closing access after a specified time.

*-Explanation of Task 2*

Task 2 manages elevator access and movement. It checks if access has been granted and if an elevator request (bElevatorRequest) is active. 
If both conditions are met, a timer (tmrElevatorMove) is started for the elevator to reach floor 0. 
Once the timer finishes, bElevatorArrived in the GVL is set to TRUE, signaling the elevator’s arrival at floor 0, and resets when no access or request is active.