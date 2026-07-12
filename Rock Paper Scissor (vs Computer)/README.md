# Day 3: Rock Paper Scissor (vs Computer)

## 📌 Overview
A console-based Rock Paper Scissor game where the user plays against the computer. The computer's move is chosen randomly, the winner is decided using classic Rock-Paper-Scissor rules, and both round-wise and overall scores are tracked across multiple rounds until the user chooses to stop.

## 🎯 Concepts Covered
- **`enum`** – representing a fixed set of values (`ROCK`, `PAPER`, `SCISSOR`) as a proper type instead of raw numbers or strings
- **`Random` class** – generating the computer's move
- **`do-while` loop** – running the game for multiple rounds based on user choice
- **Methods** – separating winner-decision logic (`decideWinner`) from the main game loop for readability
- **Score tracking** – maintaining running totals across rounds

## 🧠 What I Learned

- **Why `enum` over plain numbers/strings:** Using `enum Move { ROCK, PAPER, SCISSOR }` makes the code type-safe (no invalid value like `4` or `"rockk"` can sneak in) and far more readable than comparing raw integers everywhere.

- **`Move.values()`** – every enum automatically gets a `.values()` method that returns an array of all its constants in declared order (`[ROCK, PAPER, SCISSOR]`). This made it easy to:
  - Convert the user's numeric choice into an enum: `Move.values()[choice - 1]`
  - Pick a random enum value for the computer: `Move.values()[random.nextInt(3)]`

- **`ordinal()` and the winner-decision formula:** Instead of writing all 9 combinations of Rock/Paper/Scissor as separate `if` conditions, I used each enum constant's position (`ordinal()` — ROCK=0, PAPER=1, SCISSOR=2) to detect a win with one formula:
  ```java
  int diff = (user.ordinal() - computer.ordinal() + 3) % 3;
  // diff == 1  →  user wins
  ```
  This works because Rock → Paper → Scissor → Rock forms a circular pattern, where each move only beats the move exactly one position "behind" it. The `+3` before the modulo avoids Java producing a negative remainder when the first ordinal is smaller than the second.

- **Trade-off — cleverness vs. readability:** This formula is compact, but it's noticeably harder to read at a glance compared to writing out all 9 explicit `if` cases. It's a good example of how "shorter" code isn't always "better" code — readability matters just as much, especially while still learning.

## 🕹️ How to Run
```bash
javac RockPaperScissor.java
java RockPaperScissor
```

## 🚀 Possible Improvements (Future Scope)
- Add `try-catch` around input reading to gracefully handle non-numeric input instead of crashing
- Let the user play "best of N" rounds instead of open-ended play
- Add a `TIE` streak counter or round history

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
