# Day 15: Contact Book App (Encapsulation + ArrayList Basics)

## 📌 Overview
A console-based contact book that lets the user add, view, search, update, and delete contacts. Unlike the Day 8 To-Do List (which used fixed-size arrays), this project uses `ArrayList` — a dynamically-sized collection — to store `Contact` objects.

## 🎯 Concepts Covered
- **`ArrayList`** – a dynamically resizable list, unlike a fixed-size array
- **Generics (`ArrayList<Contact>`)** – restricting the list to only hold `Contact` objects, giving compile-time type safety
- **Encapsulation** – `Contact`'s fields are `private`, accessed only through getters/setters
- **Core `ArrayList` methods** – `.add()`, `.get()`, `.remove()`, `.size()`, `.isEmpty()`
- **`for-each` loop over a collection** – iterating an `ArrayList` directly without manual index management

## 🧠 What I Learned

- **`ArrayList` solves the Day 8 array-size problem:** The To-Do List project had a hard `MAX_TASKS` limit because arrays have a fixed size at creation. `ArrayList` has no such limit — `.add()` grows the list automatically as needed.

- **`.remove(index)` handles shifting internally:** In the Day 8 To-Do List, deleting a task required manually writing a loop to shift every subsequent element one position left. With `ArrayList`, `contacts.remove(index)` does all of that shifting internally — no manual loop needed.

- **Why the setter (`setPhoneNumber()`) initially had no use, and why that mattered:** A constructor only runs once, when an object is first created. A setter can be called anytime *after* creation to update a field's value. Initially, `setPhoneNumber()` was defined but never called anywhere — the app had no "Update Contact" feature, so the setter existed but was genuinely dead code. Adding an "Update Contact" menu option gave it a real purpose: modifying an *existing* `Contact` object's phone number without creating a new one.

- **`sc.nextLine()` after `sc.nextInt()`:** Same recurring pattern from earlier projects — reading a number with `nextInt()` leaves a leftover newline in the input buffer, so an extra `sc.nextLine()` call is needed before reading the next full line of text (like a name or phone number).

- **A known limitation (left as-is for now):** If the user enters something that isn't a valid list position — like an actual phone number instead of the S.No. shown in the list — the program throws an `InputMismatchException` and crashes. This can be fixed with `try-catch` around the input reading (planned as a future improvement, once exception handling is covered in more depth around Day 18).

## 🕹️ How to Run
```bash
javac ContactBook.java Contact.java
java ContactBook
```

## 🚀 Possible Improvements (Future Scope)
- Add `try-catch` around list-position input to prevent crashes on invalid entries (see Day 18: Custom Exception Handling)
- Prevent duplicate contacts (same name or phone number)
- Sort contacts alphabetically before displaying
- Persist contacts to a file so they aren't lost when the program closes

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
