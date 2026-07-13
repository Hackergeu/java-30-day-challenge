# Day 4: ATM Simulation (Single Account)

## 📌 Overview
A console-based ATM simulation for a single account. The user must first enter a correct PIN to gain access, after which a menu-driven system lets them check their balance, deposit money, or withdraw money, until they choose to exit.

## 🎯 Concepts Covered
- **Methods** – separating each operation (`checkBalance()`, `deposit()`, `withdraw()`) into its own method for a clean, modular structure
- **`static` variables and methods** – sharing state (`balance`, `sc`) across multiple methods within the same class
- **`static final`** – marking the PIN as a constant that should never change
- **`do-while` loop** – running a repeating menu until the user selects "Exit"
- **`switch-case`** – routing the user's menu choice to the correct method
- **Basic validation** – preventing negative deposits/withdrawals and withdrawals exceeding the available balance

## 🧠 What I Learned

- **Why `Scanner` and `balance` had to be `static`:** Since operations like `deposit()` and `withdraw()` are separate methods (outside `main()`), a `Scanner` or `balance` variable declared *inside* `main()` would be out of scope for them — Java variables are only accessible within the block/method they're declared in. Declaring them at the **class level** with `static` makes them accessible to every method in the class.

- **Why `static` specifically (not just "class level"):** `main()` itself is a `static` method, and so are `deposit()`, `withdraw()`, etc. A `static` method can only directly access other `static` members — trying to access a non-static variable from a static method throws a compile error: *"non-static variable cannot be referenced from a static context."* So both `sc` and `balance` had to be `static` to match the methods using them.

- **`static final` for constants:** The PIN (`CORRECT_PIN`) is declared as `static final` because it's a fixed value that should never be reassigned during the program's execution — `final` enforces that at compile time.

- **Early return for access control:** If the entered PIN is wrong, the program calls `return;` immediately inside `main()`, which exits the program right away instead of letting it proceed to the menu.

## 🕹️ How to Run
```bash
javac ATMSimulation.java
java ATMSimulation
```
**Default PIN:** `1234` | **Starting Balance:** Rs. 5000.0

## 🚀 Possible Improvements (Future Scope)
- Move away from `static` shared state by using an actual `Account` class with instance variables (this becomes relevant once OOP concepts like classes and objects are covered)
- Support multiple accounts instead of a single hardcoded account
- Add a transaction history log
- Limit PIN attempts (e.g., lock after 3 wrong tries) instead of exiting after a single wrong attempt

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
