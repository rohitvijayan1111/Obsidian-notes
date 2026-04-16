# Overview of the project

The objective of this project is to develop a Console-based Tic-Tac-Toe application that allows users to play the game in multiple modes, including against a computer with varying difficulty levels or in a manual mode. The application will include user authentication (login and sign-up), maintain player scores, and store game history with the ability to replay past games. 


# Objective of this document

This document is prepared to gather clarifications and confirm assumptions regarding the system requirements before finalizing the Software Requirements Specification (SRS).


# 2. Feature-wise Questions & Assumptions

### 2.1 Login / Signup
### Questions

1. What are the constraints for username and password? (length, special characters, etc.)
2. Should users be allowed to change their username or password after registration?
3. Is password reset (forgot password) required?
4. Should duplicate usernames be allowed?

### Assumptions

- Username must be **unique** - combination of letters and numbers.
- Password will follow **basic strength rules**  - ??????????
- Passwords will be **securely hashed and stored**


## 2.2 Game settings

### Questions

1. Should the Tic-Tac-Toe board always be **3×3**, or will it vary?
2. Should players be allowed to choose their symbol (X/O)?
3. Who starts the game?
    - Always the logged-in user?
    - Or the player who chooses X?
4. Should game rules be shown:
    - Before login?
    - Or as an optional help screen?
    - Or before every game?

### Assumptions

- Board size is **fixed at 3×3**
- The player who is logged in gets X.
- Rules will be available as an **optional help feature** in the main menu and could be should after signup.


## **2.4 Scoring System** - rephrase

### Questions

1. How should scores be maintained:
    - Per session head to head of the player?
    - The users score, across playing many matches?
    - Head-to-head of those players ?
2. What score should be given for a draw?

### Assumptions

- Winners would be allocated **100 point**
- When the match is draw both the players will be allocated **50 points**
- Scores are tracked **per user and persisted** and would be rendered


## **2.5 Quit Game**

### Questions

1. If a user quits mid-game should the game history be stored in history?
2. Should confirmation be shown before quitting? 

### Assumptions

- Quit games may be stored in history with status = “Abandoned”
- Confirmation prompt will be shown to the user, to prevent accidental quitting.

## **2.7 UI / Controls**

### Questions

1. What input method is preferred to choose the cell in the tic tac toe game:
    - Number keys (1–9)?
    - Arrow keys navigation?
2. Should menu navigation be:
    - Asking the user to enter the number of the option, based on the menu displayed.
    - Key-based (arrows + enter) to move across and choose the option?
3. Any preferred color themes or UI style?

### Assumptions

- Input via **number keys (1–9)**
- Menu selection via **number-based navigation**
- Basic UI without advanced theming
## **2.8 Error Handling**

### Questions

1. What should happen if a user enters an invalid move?
### Assumptions

- Invalid moves will: Show error message and Ask user to retry
## **2.9 Platform & Technology**

### Questions

1. Is a **console-based application** in C# acceptable?
2. Can external libraries (e.g., NuGet packages) be used?
### Assumptions
- Application will be **console-based**
- Use of standard libraries (NuGet) is allowed

---

## **2.10 Data Storage**

### Questions

1. Should data be stored In files or In a database?

### Assumptions

- Data will be stored locally using Files
