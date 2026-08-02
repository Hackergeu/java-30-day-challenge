# Day 24: Snake Game (Java Swing)

## 📌 Overview
A classic Snake game built with Java Swing — the first GUI-based project in this challenge. The snake moves continuously in a grid, grows when it eats food, and the game ends if it hits a wall or its own body. Press Enter to restart after a game over.

## 🎯 Concepts Covered
- **`JFrame`** – the main application window
- **`JPanel`** – the drawing surface where the game is rendered
- **`Graphics`** – drawing shapes (`fillRect`, `fillOval`, `drawString`) onto the panel
- **`Timer` + `ActionListener`** – driving the game loop, ticking at a fixed interval
- **`KeyListener` (via `KeyAdapter`)** – capturing arrow key input to control the snake's direction
- **Event-driven programming** – code reacting to events (timer ticks, key presses) instead of running top-to-bottom once

## 🧠 What I Learned

- **Event-driven vs. procedural flow:** Every previous console project ran in a straight line — show a menu, read input, process it, repeat. A GUI game doesn't work that way: the program sets everything up once, then *waits* for events (a timer tick, a key press), and only runs specific code (`actionPerformed()`, `keyPressed()`) when those events happen. Control isn't linear anymore — it's reactive.

- **The game loop, powered by `Timer`:** `new Timer(DELAY, this)` fires `actionPerformed()` every `DELAY` milliseconds. Each tick does three things in order: move the snake, check for collisions, then call `repaint()` to redraw the screen — this repeating cycle *is* the game loop.

- **Representing the snake as two parallel arrays:** `snakeX[]` and `snakeY[]` store the x/y pixel position of every body segment, with index `0` always being the head. This mirrors the "parallel arrays" idea from the Day 8 To-Do List, just applied to coordinates instead of task data.

- **Why the movement loop runs backwards:** `move()` shifts every segment to the position of the one in front of it, looping from `snakeLength - 1` down to `1`. Looping forward instead would overwrite each segment's position with the next one's *before* that data was copied forward, corrupting the whole snake. Going backwards preserves each value just long enough to be copied.

- **Preventing instant U-turns:** The direction can't be reversed directly (e.g., pressing Down while already moving Up would make the snake collide with its own neck instantly). Each direction change checks the *opposite* direction first (`if (direction != 'D') direction = 'U';`) to block that.

- **`repaint()` vs `paintComponent()`:** `repaint()` is called manually to *request* a redraw, but Swing itself decides when to actually call `paintComponent()` in response — this is a Swing convention, not something the game loop controls directly.

## 🕹️ How to Run
```bash
javac SnakeGame.java
java SnakeGame
```
**Controls:** Arrow keys to move, Enter to restart after Game Over.

## 🚀 Possible Improvements (Future Scope)
- Add increasing speed as the score goes up (reduce `DELAY` dynamically)
- Add a high score that persists using File I/O (Day 22 concepts)
- Add a pause feature
- Add walls that wrap around instead of ending the game

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
