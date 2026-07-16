# Day 7: Tic-Tac-Toe (2-Player, Console)

## 📌 Overview
A console-based 2-player Tic-Tac-Toe game. Players take turns entering a position (1–9, mapped like a phone keypad) to place their mark (`X` or `O`) on a 3x3 board. The game detects a win across all rows, columns, and diagonals, or declares a draw if the board fills up with no winner.

## 🎯 Concepts Covered
- **2D Arrays (`char[3][3]`)** – representing the 3x3 game board
- **Nested loops** – printing the board and checking rows/columns for a win
- **Game state management** – tracking whose turn it is, how many moves have been played, and whether the game has ended
- **Win-condition logic** – checking all possible winning combinations (3 rows, 3 columns, 2 diagonals)
- **Input mapping** – converting a single number (1–9) into 2D grid coordinates

## 🧠 What I Learned

- **Numbered board trick:** Initializing the board with `'1'` through `'9'` instead of blank spaces lets the player see exactly which number corresponds to which cell, making input simpler — the user just enters one number instead of a row and column separately.

- **Position → row/col conversion:** The formula `row = (position - 1) / 3` and `col = (position - 1) % 3` converts a 1D number (1–9) into 2D grid coordinates:
  - Integer division (`/3`) determines which row the position falls into (since each row has 3 cells)
  - Modulo (`%3`) determines which column within that row
  
  For example, position `5` → `row = (5-1)/3 = 1`, `col = (5-1)%3 = 1` → the center cell `board[1][1]`.

- **Checking all 8 winning combinations:** A win can happen in 8 possible ways — 3 rows, 3 columns, and 2 diagonals. Rather than writing one giant condition, each type of check is handled with its own small loop or direct comparison, making `checkWin()` easy to read and verify.

- **Occupied-cell validation:** Before placing a mark, the code checks if the target cell already contains `'X'` or `'O'` (rather than a number), preventing a player from overwriting an existing move.

- **Draw detection:** The game tracks `movesPlayed` — if it reaches 9 (the whole board is full) without `checkWin()` returning true, the game is declared a draw.

## 🕹️ How to Run
```bash
javac TicTacToe.java
java TicTacToe
```

## 🚀 Possible Improvements (Future Scope)
- Add a single-player mode against a computer opponent (simple random-move AI to start)
- Highlight the winning line when a player wins
- Refactor the board into an `ArrayList` or use `Scanner` validation with `try-catch` for non-numeric input

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
