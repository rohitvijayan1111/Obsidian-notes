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

### Assumptions

- Board size is **fixed at 3×3**
- Logged-in user starts first
- Default symbols: Player = X, Opponent = O
- Rules will be available as an **optional help feature**