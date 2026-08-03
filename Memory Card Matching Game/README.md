# Day 25: Memory Card Matching Game (Swing, 2D Grid)

## 📌 Overview
A classic memory card matching game built with Java Swing. A 4x4 grid of hidden cards (8 pairs of numbers) is displayed as buttons — clicking two cards reveals their values, and matching pairs stay visible while mismatches flip back after a short delay.

## 🎯 Concepts Covered
- **`JButton` grid with `GridLayout`** – arranging 16 buttons into a 4x4 visual grid
- **`ActionListener` (lambda form)** – handling clicks on each button individually
- **`Collections.shuffle()`** – randomly rearranging a list of card values
- **Game state tracking** – tracking which cards are picked, matched, or mid-comparison using parallel arrays and index variables
- **`Timer` with `setRepeats(false)`** – a one-time delayed action (used here to briefly show a mismatched pair before hiding it again)

## 🧠 What I Learned

- **Shuffling with `Collections.shuffle()`:** Building the card values as `1,1,2,2,3,3...8,8` in a `List<Integer>` and calling `Collections.shuffle(values)` randomly reorders them in place — much simpler than manually writing a shuffling algorithm.

- **Tracking "first pick" and "second pick" with index variables:** Rather than storing full card objects, `firstPick` and `secondPick` just store the *array index* of the clicked buttons. `-1` is used as a sentinel value meaning "no card picked yet" — the same sentinel-value pattern used for the "invalid index" cases in earlier console projects.

- **Why clicks need to be blocked while `waiting` is true:** After a mismatch, both cards are shown briefly before flipping back. Without the `waiting` flag, a player could keep clicking other cards during that delay, corrupting `firstPick`/`secondPick` before the mismatch animation even finishes. Checking `if (waiting || ...) return;` at the top of `handleCardClick()` locks out further input until the delay is done.

- **`Timer` with `setRepeats(false)`:** In the Day 24 Snake Game, `Timer` fired repeatedly to drive the game loop. Here, it's used differently — `hideTimer.setRepeats(false)` makes it fire *exactly once* after 800 milliseconds, which is exactly what's needed for "wait briefly, then do one thing."

- **Lambda expressions instead of separate listener classes:** `button.addActionListener(e -> handleCardClick(index))` is a shorter way of writing an anonymous `ActionListener` class (compare this to the `Comparator` anonymous class from Day 20) — the lambda just needs one line to call the actual handler method.

- **Why `final int index` was needed inside the loop:** Java requires any local variable used inside a lambda to be "effectively final" (never reassigned after being set). Since the loop variable `i` changes on every iteration, it can't be used directly inside the lambda — copying its value into a new `final int index` each iteration works around this.

## 🕹️ How to Run
```bash
javac MemoryCardGame.java
java MemoryCardGame
```
**Controls:** Click any two cards to try to match them.

## 🚀 Possible Improvements (Future Scope)
- Track and display the number of moves/attempts taken
- Add a "Restart" button instead of requiring the program to be re-run
- Use images or symbols instead of numbers for the cards
- Add a timer/scoring system based on how quickly all pairs are matched

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
