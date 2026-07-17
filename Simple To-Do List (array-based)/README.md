# Day 8: Simple To-Do List (Array-Based)

## 📌 Overview
A console-based menu-driven To-Do List that lets the user view, add, complete, and delete tasks, backed entirely by fixed-size arrays (no `ArrayList` used — intentionally, to first understand array limitations before learning collections).

## 🎯 Concepts Covered
- **Arrays** – storing tasks (`String[]`) and their completion status (`boolean[]`) using two parallel arrays
- **CRUD operations** – Create (add), Read (view), Update (mark complete), Delete — all implemented manually using array logic
- **Array limitations** – experiencing firsthand why a fixed-size array becomes a problem once it's full, and why deleting from the middle requires manually shifting elements
- **Menu-driven structure** – reused the `do-while` + `switch-case` pattern from the ATM Simulation project

## 🧠 What I Learned

- **Parallel arrays:** Instead of one complex structure, two same-length arrays (`tasks[]` and `isDone[]`) are used together — the same index in both arrays always refers to the same task. This works, but it's also a good preview of *why* a single object (a `Task` class with `description` and `done` fields) would be a cleaner design — something to look forward to once OOP concepts are covered.

- **Why `MAX_TASKS` is a hard limit:** Since a Java array's size is fixed at creation (`new String[MAX_TASKS]`), the list simply cannot hold more than 10 tasks no matter what — `addTask()` explicitly checks `taskCount >= MAX_TASKS` and refuses to add further. This is a genuine limitation of arrays that a dynamic structure like `ArrayList` (coming up on Day 16) solves automatically.

- **Deleting from the middle of an array — the shifting trick:** Arrays don't have a built-in way to "remove a gap." To delete task at index `index`, every task *after* it has to be shifted one position to the left:
  ```java
  for (int i = index; i < taskCount - 1; i++) {
      tasks[i] = tasks[i + 1];
  }
  ```
  After shifting, the last slot still holds a duplicate of the second-to-last value, so it's manually cleared (`tasks[taskCount - 1] = null`) and `taskCount` is decremented.

- **`sc.nextLine()` after `sc.nextInt()`:** After reading a menu choice with `nextInt()`, the newline character from pressing Enter is left behind in the input buffer. Calling `sc.nextLine()` right after consumes that leftover newline — without it, the next `sc.nextLine()` call (used to read the task description) would immediately return an empty string instead of waiting for real input.

## 🕹️ How to Run
```bash
javac ToDoList.java
java ToDoList
```

## 🚀 Possible Improvements (Future Scope)
- Replace the two parallel arrays with a single `Task` class once OOP is covered
- Replace the fixed-size array with an `ArrayList` to remove the 10-task limit
- Add task priorities or due dates
- Persist tasks to a file so they survive between program runs

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
