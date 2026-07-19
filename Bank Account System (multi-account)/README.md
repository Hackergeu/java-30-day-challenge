# Day 10: Bank Account System (Multi-Account)

## 📌 Overview
A console-based banking system supporting multiple accounts. Users can create new accounts, deposit, withdraw, check balance, and view all accounts — each account's data is protected using encapsulation, accessible only through controlled methods.

## 🎯 Concepts Covered
- **Encapsulation** – making fields `private` and exposing controlled access through getters and validated methods
- **Data protection** – preventing invalid states (like a negative balance) by keeping `balance` inaccessible from outside the class
- **Multiple objects management** – storing and searching through an array of `Account` objects
- **Boolean return values** – `deposit()`/`withdraw()` return `true`/`false` so calling code knows whether the operation actually succeeded
- **Auto-generated identifiers** – generating a simple unique account number for each new account

## 🧠 What I Learned

- **Why `private` matters:** In the Day 9 Library project, `Book` fields were public — anything outside the class could directly do `book.title = "..."` with no checks. Here, `balance` is `private`, so the *only* way to change it is through `deposit()`/`withdraw()` — methods that contain validation logic (rejecting negative amounts, rejecting withdrawals beyond the balance). This is the core idea of encapsulation: **the object controls its own data**, rather than trusting outside code to modify it correctly.

- **Getters vs direct field access:** `getBalance()` only *reads* the balance — it can't be used to change it. This is intentional: some fields should be readable but never writable from outside (or only writable through specific validated methods).

- **Why `deposit()`/`withdraw()` return `boolean`:** Returning `true`/`false` lets the calling code know whether the operation actually happened. Without this, if a withdrawal silently failed due to insufficient balance, the calling code would have no way to know — it would just assume success.

- **Searching for an account:** Since `Account[] accounts` is just an array, finding a specific account means looping through it and comparing account numbers (`findAccountByNumber()`). This linear search works fine for a small number of accounts, but it's a preview of why `HashMap` (Day 17) is more efficient for lookups by a unique key.

- **`sc.nextLine()` after `sc.nextInt()`:** Just like in the To-Do List project, reading a number with `nextInt()` leaves a leftover newline in the buffer, so `sc.nextLine()` is called right after to clear it before reading the next line of text input.

## 🕹️ How to Run
```bash
javac BankAccountSystem.java Account.java
java BankAccountSystem
```

## 🚀 Possible Improvements (Future Scope)
- Replace the fixed-size `Account[]` array with a `HashMap<String, Account>` for faster lookups by account number
- Add a PIN/password per account for authentication
- Add a transaction history log per account
- Support fund transfers between two accounts

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
