#  **Architectural Overview**

The Tic-Tac-Toe application follows a **layered architecture based on the Model-View-Controller (MVC) pattern**, with a dedicated **Service Layer** and **Data Layer** to ensure clear separation of concerns, modularity, and maintainability.

The system is organized into four primary layers:

## **1. View Layer (Presentation Layer)**

**Components:**
- `ConsoleView`
- `BoardView`

**Description:**  
The View Layer is responsible for all user interactions. It handles input and output operations through the console interface. This includes displaying menus, rendering the Tic-Tac-Toe board, and capturing user inputs such as navigation and move selection.
## **2. Controller Layer**

**Components:**
- `AuthController`
- `MainController`
- `GameController`
- `HistoryController`

**Description:**  
The Controller Layer manages the overall application flow and user navigation. It acts as an intermediary between the View and Service layers. Controllers interpret user actions, invoke appropriate services, and determine the next steps in the application workflow (e.g., starting a game, viewing history, replaying a game).

---

## **3. Service Layer (Business Logic Layer)**

**Components:**
- `AuthService`
- `GameService`
- `BotService`
- `ReplayService`

**Description:**  
The Service Layer encapsulates the core business logic of the application. It is responsible for:
- User authentication and validation
- Game logic (move validation, win/draw detection)
- AI decision-making for different difficulty levels
- Replay simulation using stored move sequences

This layer ensures that all core computations and rules are isolated from UI and control flow.
## **4. Data Layer (Persistence Layer)**

**Components:**
- File Storage (Users, Games, Scores)

**Description:**  
The Data Layer is responsible for storing and retrieving persistent data. It manages user information, game history, and scores using file-based storage. Data is read and written through structured formats, enabling persistence across application sessions.


# **System Components**

---

## **Authentication Component**

The authentication component is responsible for handling user registration and login. When a user enters their credentials, the request is processed by the controller and validated through the service layer. The system ensures that usernames are unique and that only valid users are allowed to access the application. This component interacts with the data layer to store and retrieve user information.

---

## **Game Management Component**

The game management component forms the core of the application. It is responsible for creating a new game, managing turns between players, validating moves, and determining the outcome of the game. It controls the overall game lifecycle, from initialization to completion. This component also coordinates with other parts of the system, such as the AI module for bot moves and the data layer for saving game results.

---

## **AI (Bot) Component**

The AI component is responsible for generating moves when the user plays against the computer. Based on the selected difficulty level, it decides how the move is generated. In easier modes, the moves are less strategic, while in harder modes, the system makes more optimal decisions. The component takes the current board state as input and returns a valid move.

---

## **Score Management Component**

The score management component keeps track of user performance across games. It updates the score when a game is completed and ensures that no points are awarded if the game is abandoned. The scores are stored persistently so that they remain available across sessions.

---

## **History and Replay Component**

This component manages previously played games. It allows users to view their game history and select a game for replay. The replay functionality is implemented by reconstructing the game step-by-step using the sequence of stored moves, allowing the user to review how the game progressed.

---

## **User Interface Component**

The user interface component handles all interactions between the user and the system. It is responsible for displaying menus, rendering the game board, and capturing user input. The interface is console-based and supports keyboard navigation for both menu selection and gameplay.

---

## **Data Persistence Component**

The data persistence component is responsible for storing and retrieving all application data, including user details, game history, and scores. Data is stored locally using files, and all read/write operations are handled through the service layer.



# **Decision-Making Strategy (Minimax Algorithm)**

The core decision-making logic of the Tic-Tac-Toe system is based on the Minimax algorithm, a recursive strategy used in two-player games to determine the optimal move. The algorithm assumes that both players play optimally and evaluates all possible future game states before selecting a move.


## **Working Principle**

At each turn, the algorithm explores all possible moves from the current board state and constructs a decision tree of future game outcomes. Each terminal state is assigned a score:
- A win for the computer is assigned a positive score
- A win for the opponent is assigned a negative score
- A draw is assigned a neutral score
    

The algorithm alternates between two roles:
- **Maximizing player (Computer):** Attempts to maximize the score
- **Minimizing player (Human):** Attempts to minimize the score
    

By recursively evaluating all possible outcomes, the algorithm selects the move that leads to the most favorable result for the computer.

## **Application in Game Modes**

### **Easy Mode**

In Easy mode, the system uses a simple and non-strategic approach. It checks for an immediate winning move and selects it if available; otherwise, it chooses a move randomly from the available positions. The system does not attempt to block the opponent or evaluate future outcomes, making it easy for the player to win.


### **Medium Mode**

In Medium mode, the system aims to provide a balanced level of difficulty. This is achieved by combining optimal decision-making with controlled randomness.

For each move, the system decides whether to use the Minimax algorithm or a random move. With approximately 50% probability, the system selects the best possible move using Minimax. In the remaining cases, it chooses a random move.

This hybrid approach ensures that the computer sometimes plays optimally and sometimes makes mistakes, creating a more natural and unpredictable gameplay experience. It prevents the game from being too easy or too difficult, giving both the player and the system a fair chance of winning.

---

### **Hard Mode**

In Hard mode, the system fully utilizes the Minimax algorithm to make optimal decisions. It evaluates all possible future game states and selects the move that maximizes its chances of winning while minimizing the opponent’s chances.

As a result, the computer will always play the best possible move assuming the player also plays optimally. This guarantees that the system will either win or force a draw, making it extremely challenging for the player to win.
