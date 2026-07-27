# Day 18: Custom Exception Handling – Withdrawal System

## 📌 Overview
A console-based withdrawal system demonstrating custom exception handling. Two custom exceptions — `InsufficientBalanceException` and `InvalidAmountException` — are defined and thrown based on specific business rules, then caught and handled gracefully using `try-catch-finally`.

## 🎯 Concepts Covered
- **Custom Exceptions** – creating exception classes (`extends Exception`) tailored to specific business rules, rather than relying only on Java's built-in exceptions
- **`throw`** – manually triggering an exception when an invalid condition is detected
- **`throws`** – declaring in a method's signature that it may throw a checked exception, requiring the caller to handle it
- **`try-catch-finally`** – wrapping risky code, handling specific failure types separately, and running cleanup code unconditionally
- **Multiple catch blocks** – handling different exception types from the same `try` block with separate, targeted responses

## 🧠 What I Learned

- **Why custom exceptions instead of just built-in ones:** Java doesn't have a built-in exception specifically for "insufficient balance" or "invalid withdrawal amount" — those are rules specific to this application's logic. Creating `InsufficientBalanceException` and `InvalidAmountException` (both `extends Exception`) lets the code express *exactly* what went wrong in domain-specific terms, rather than using a generic exception that doesn't clearly communicate the actual problem.

- **`throw` vs `throws` — easy to confuse, different jobs:** `throw` is a statement that actually creates and fires an exception object at a specific point in the code (`throw new InvalidAmountException("...")`). `throws`, written in a method's signature (`public void withdraw(double amount) throws InsufficientBalanceException, InvalidAmountException`), is a declaration telling any code that calls this method: "you must be prepared to handle these exceptions."

- **Multiple catch blocks run independently:** A single `try` block can be followed by several `catch` blocks, each targeting a different exception type. Java checks them top to bottom and runs only the one whose type matches what was actually thrown — the others are simply skipped.

- **`finally` always runs:** Regardless of whether the `try` block succeeds, or which `catch` block (if any) handles the failure, the `finally` block executes every single time. This is useful for guaranteed cleanup or logging — in this project, it prints a "transaction attempt completed" message no matter the outcome.

- **Custom exceptions reuse the built-in mechanism:** `super(message)` inside each custom exception's constructor passes the message up to the built-in `Exception` class, which is what makes `e.getMessage()` work correctly when the exception is caught later.

## 🕹️ How to Run
```bash
javac WithdrawalSystem.java Account.java InsufficientBalanceException.java InvalidAmountException.java
java WithdrawalSystem
```

## 🚀 Possible Improvements (Future Scope)
- Explore checked vs. unchecked exceptions in more depth (why `RuntimeException` subclasses don't require a `throws` declaration)
- Add exception chaining (wrapping one exception as the "cause" of another)
- Add a minimum balance requirement (separate from simply "not enough funds")
- Log failed transaction attempts to a file (ties into Day 22's File I/O concepts)

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
