# Day 2: Simple Calculator (CLI)

## 📌 Overview
A console-based calculator that takes two numbers and an operator from the user, performs the corresponding arithmetic operation, and displays the result. The program keeps running in a loop, allowing the user to perform multiple calculations until they choose to exit.

## 🎯 Concepts Covered
- **`switch-case` statement** – choosing the correct operation based on the operator entered
- **`char` data type** – storing and comparing single-character input (operator, continue/exit choice)
- **`do-while` loop** – ensures the calculator runs at least once, and repeats based on user choice
- **Variable scope** – understanding why a variable used both inside and outside a block needs to be declared at the right level
- **Edge case handling** – preventing divide-by-zero and modulus-by-zero errors

## 🧠 What I Learned

- **`sc.next().charAt(0)`** – Java's `Scanner` has no direct method to read a single `char`, so the trick is to read a `String` token with `next()` and pick its first character with `.charAt(0)`.

- **Bug 1 — Variable Scope Error:** Initially, the `key` variable (used to ask "continue or not?") was declared *inside* the `do{}` block but checked in the `while()` condition *outside* the block. Since Java variables only exist within the `{ }` block they're declared in, this caused a "cannot find symbol" compile error. Fixed by declaring `key` *before* the `do{}` block and only assigning its value inside.

- **Bug 2 — Repeating the same calculation:** Originally, the numbers and operator were being read only once, *outside* the loop. This meant that even after choosing to continue, the calculator would repeat the exact same calculation instead of asking for new input. Fixed by moving the input-reading code *inside* the `do{}` block.

- **`double` division by zero:** Unlike `int` division (which throws an `ArithmeticException`), dividing a `double` by zero doesn't crash the program — it returns `Infinity`. Since that's not user-friendly, an explicit check (`if (num2 == 0)`) was added before performing division and modulus.

## 🕹️ How to Run
```bash
javac Calculator.java
java Calculator
```

## 🚀 Possible Improvements (Future Scope)
- Add input validation for invalid operator entries before hitting the `switch`
- Support for more operations (power, square root)
- Wrap operations in separate methods for better modularity (e.g., `add()`, `subtract()`)

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
