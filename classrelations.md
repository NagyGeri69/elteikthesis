# Class Relations

## GameManager Dependencies
GameManager --> BoardManager : Creates / Uses
GameManager --> IPlayerController : Creates / Uses
GameManager --> HumanPlayer : Creates / Manages
GameManager --> NetworkPlayer : Uses
GameManager --> AIPlayer : Creates / Manages
GameManager --> OnlineLobby : Uses for online player data
GameManager --> RelayConnection : Uses for network setup
GameManager --> StoneManager : Subscribes to events

## BoardManager Dependencies
BoardManager --> IPlayerController : Manages players and turns
BoardManager --> StoneManager : Notifies of moves via events

## StoneManager Dependencies
StoneManager --> PitNumberDisplayManager : Updates pit displays
StoneManager --> BoardManager : Subscribes to OnGameCreated and OnMoveMade events

## PitActionTrigger Dependencies
PitActionTrigger --> GameManager : Checks game state
PitActionTrigger --> StoneManager : Checks stone movement state

## OnlineLobby Dependencies
OnlineLobby --> GameManager : Subscribes to OnGameStarted and OnGameOver
OnlineLobby --> RelayConnection : Subscribes to OnPlayersJoined
OnlineLobby --> IPlayerController : Uses for player management

## RelayConnection Dependencies
RelayConnection --> GameManager : Subscribes to OnGameOver
RelayConnection --> OnlineLobby : Subscribes to OnLeftLobby

## LobbyViewManager Dependencies
LobbyViewManager --> OnlineLobby : Uses for lobby operations

## PitNumberDisplayManager Dependencies
PitNumberDisplayManager --> GameManager : Subscribes to OnGameOver
PitNumberDisplayManager --> CameraManager : Uses for perspective checks

## HumanPlayer Dependencies
HumanPlayer --> PitActionTrigger : Subscribes to OnMoveSelectedByPit

## NetworkPlayer Dependencies
NetworkPlayer --> PitActionTrigger : Subscribes to OnMoveSelectedByPit

## AIPlayer Dependencies
AIPlayer --> BoardManager : Gets game state
AIPlayer --> StoneManager : Checks stone movement state

## Inheritance Relations
HumanPlayer --|> IPlayerController : Implements
NetworkPlayer --|> IPlayerController : Implements
AIPlayer --|> IPlayerController : Implements

## Event Relations
IPlayerController -- OnMoveSelected --> BoardManager : Triggers moves
BoardManager -- OnGameCreated --> StoneManager : Triggers stone spawning
BoardManager -- OnMoveMade --> StoneManager : Triggers stone movement
GameManager -- OnGameStarted --> OnlineLobby : Notifies game start
GameManager -- OnGameOver --> OnlineLobby : Notifies game end
RelayConnection -- OnPlayersJoined --> OnlineLobby : Notifies when players join
GameManager -- OnGameOver --> RelayConnection : Notifies game end
OnlineLobby -- OnLeftLobby --> RelayConnection : Notifies lobby exit
OnlineLobby -- OnLeftLobby --> LobbyViewManager : Notifies lobby exit
GameManager -- OnGameOver --> PitNumberDisplayManager : Notifies game end
PitActionTrigger -- OnMoveSelectedByPit --> HumanPlayer : Notifies of pit selection
PitActionTrigger -- OnMoveSelectedByPit --> NetworkPlayer : Notifies of pit selection
