# State Diagram


*-First State Diagram of Getting Access to the Hall*

The system begins in an idle state, awaiting card presentation. Once the card is presented, it transitions to card validation. 
If the card is valid, access is granted, the door opens, and the person enters. If the card is invalid, access is denied, and the system resets to idle. 

```plantuml
@startuml CARD

START -> [Idle] : Leaving the room

[Idle] --> [CardPresented] : Card presented
[CardPresented] --> [CardValidated] : Validate card
[CardValidated] --> [AccessGranted] : Card valid
[CardValidated] --> [AccessDenied] : Card invalid

[AccessGranted] --> [DoorOpened] : Open door
[DoorOpened] --> [Entering] : Acces to the hall
[Entering] --> [Idle] : Reset system

[AccessDenied] --> [Idle] : Reset system

@enduml
```
---

*-Second State Diagram of Using the Elevator*

This state diagram models the process of a person using an elevator to travel to floor 0. 
Upon pressing the button, there’s a chance that the elevator is already on the same floor, allowing immediate entry. 
Otherwise, there’s a chance that the elevator is on a different floor, requiring the person to wait for its arrival. Once inside, the person selects floor 0, and the elevator moves to the destination. 

The process concludes when the elevator reaches floor 0 and the person exits.

```plantuml

@startuml ELEVATOR

START -> [WaitingForElevator] : Start

[WaitingForElevator] --> [PressButton] : Press button to call elevator
[PressButton] --> [ElevatorOnSameFloor] : Elevator is already on the same floor
[PressButton] --> [ElevatorNotOnSameFloor] : Elevator is on a different floor

[ElevatorOnSameFloor] --> [EnteringElevator] : Enter elevator
[ElevatorNotOnSameFloor] --> [WaitingForArrival] : Wait for elevator to arrive
[WaitingForArrival] --> [ElevatorArrives] : Elevator arrives
[ElevatorArrives] --> [EnteringElevator] : Enter elevator

[EnteringElevator] --> [InsideElevator] : Inside elevator
[InsideElevator] --> [SelectingFloor] : Select floor 0

[SelectingFloor] --> [MovingToFloor] : Elevator moves to floor 0
[MovingToFloor] --> [ArrivedAtFloor] : Arrive at floor 0

[ArrivedAtFloor] --> [ExitingElevator] : Exit elevator

@enduml
```