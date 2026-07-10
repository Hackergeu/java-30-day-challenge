# Day 1: Number Guessing Game

## 📌 Overview
A console-based game where the computer randomly picks a number between 1 and 100, and the user has to guess it. After every guess, the program tells the user whether their guess was too high or too low, and finally reports the total number of attempts taken.

## 🎯 Concepts Covered
- **`Random` class** – generating a random number within a specific range
- **`Scanner` class** – taking user input from the console
- **`while` loop** – repeating logic until the correct guess is made
- **Conditionals (`if-else`)** – comparing guess to target and giving feedback
- **Variables & counters** – tracking number of attempts

## 🧠 What I Learned
- How `random.nextInt(bound)` works — it generates a number from `0` to `bound-1`, so to get a custom range like `1-100`, the formula is:
  ```
  random.nextInt(range) + start
  ```
  where `range = end - start + 1`

- **Bug 1 — Infinite Loop:** Initially I forgot to read a new guess inside the `while` loop, which caused the loop to run forever since the condition never changed. Fixed by reading input again at the end of each loop iteration.

- **Bug 2 — Off-by-one in attempts count:** Since the first guess is taken *before* the loop starts, initializing `attempts = 0` undercounted the total tries (e.g., a correct first guess showed 0 attempts instead of 1). Fixed by initializing `attempts = 1` instead.

## 🕹️ How to Run
```bash
javac NumberGuessingGame.java
java NumberGuessingGame
```

## 🚀 Possible Improvements (Future Scope)
- Add input validation for guesses outside the 1-100 range
- Add a limited number of attempts (e.g., max 7 chances)
- Add difficulty levels (easy/medium/hard) with different ranges

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
