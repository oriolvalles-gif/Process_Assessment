# Sequence Diagram

*-Sequence diagram depicting the communication between the tasks*

The sequence diagram illustrates the interaction between the User, "GettingAccesstotheHall", and "UsingtheElevator". The user presents a card, prompting "GettingAccesstotheHall" to validate access and notify "UsingtheElevator". 

After the user presses the elevator button, "UsingtheElevator" checks the door status with "GettingAccesstotheHall" and updates the elevator's status accordingly. 

Finally, the user is informed of their arrival at floor 0, completing the process.

```plantuml
@startuml SEQUENCE1

actor User

User -> GettingAccesstotheHall : Present card to enter
GettingAccesstotheHall -> GVL : Write CardStatus "Valid"
GettingAccesstotheHall -> UsingtheElevator : Notify UsingtheElevator (Access granted)

alt Access Granted
    UsingtheElevator -> GVL : Read CardStatus
    UsingtheElevator -> User : Elevator button enabled

    User -> UsingtheElevator : Press button to go to floor 0
    UsingtheElevator -> GVL : Write ElevatorStatus "Moving"
    UsingtheElevator -> GettingAccesstotheHall : Request current status

    GettingAccesstotheHall -> GVL : Read DoorStatus "Closed"
    GettingAccesstotheHall -> UsingtheElevator : Send DoorStatus "Closed"

    UsingtheElevator -> GVL : Write ElevatorStatus "Arrived at floor 0"
    UsingtheElevator -> User : Notify arrival at floor 0
    User -> UsingtheElevator : Exit elevator

else Access Denied
    GettingAccesstotheHall -> GVL : Write CardStatus "Invalid"
    UsingtheElevator -> User : Elevator button disabled
end

@enduml

```

---

*-Sequence diagram showing the calling of the function by the task*

In this sequence diagram, the User presents a card to "GettingAccesstotheHall", which calls the ValidateCard function to process the card information. 
Depending on the validation outcome, "GettingAccesstotheHall" updates the Global Variable List (GVL) with either "Valid" or "Invalid" status and notifies "UsingtheElevator" accordingly. 

This diagram highlights the modular design of the system, demonstrating how a specific function handles critical validation logic.

```plantuml
@startuml SEQUENCE2

actor User

User -> GettingAccesstotheHall : Present card to enter
GettingAccesstotheHall -> GettingAccesstotheHall : Call ValidateCard
GettingAccesstotheHall -> GVL : Read CardData
GettingAccesstotheHall -> GettingAccesstotheHall : Process validation logic

alt Card Valid
    GettingAccesstotheHall -> GVL : Write CardStatus "Valid"
    GettingAccesstotheHall -> UsingtheElevator : Notify UsingtheElevator (Access granted)
else Card Invalid
    GettingAccesstotheHall -> GVL : Write CardStatus "Invalid"
    GettingAccesstotheHall -> UsingtheElevator : Notify UsingtheElevator (Access denied)
end

@enduml
```