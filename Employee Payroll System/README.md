# Day 20: Employee Payroll System (TreeMap, Comparator)

## 📌 Overview
A console-based payroll system using `TreeMap` to store employee names mapped to salaries, automatically sorted alphabetically by name. Also supports viewing the payroll sorted by salary (highest-first or lowest-first) using a custom `Comparator`.

## 🎯 Concepts Covered
- **`TreeMap<String, Double>`** – a map that automatically keeps its keys in sorted order, unlike `HashMap` (Day 16–17) which gives no order guarantee
- **`Comparator`** – defining custom sorting logic, needed because `TreeMap` only sorts by key, not by value
- **Converting a map to a sortable list** – copying `entrySet()` into an `ArrayList` since a `TreeMap` itself can't be re-sorted by value
- **`Double.compare(a, b)`** – a helper method that returns negative/zero/positive depending on whether `a` is less than, equal to, or greater than `b`
- **Anonymous classes** – implementing the `Comparator` interface inline, without creating a separate named class

## 🧠 What I Learned

- **`TreeMap` vs `HashMap`:** In Day 16–17, `HashMap` gave no guarantee about the order entries would appear in. `TreeMap` solves this automatically for keys — `viewSortedByName()` needed zero extra sorting code, since iterating a `TreeMap`'s `entrySet()` already returns entries in sorted key order.

- **Why sorting by salary needed extra steps:** `TreeMap` only sorts by *key* (name), never by *value* (salary) — there's no built-in way to ask it "sort yourself by value instead." To sort by salary, the entries first had to be copied into a `List` (`new ArrayList<>(payroll.entrySet())`), which *can* be sorted with a custom `Comparator`.

- **How `compare()` decides order:** A `Comparator`'s `compare(obj1, obj2)` method returns a negative number if `obj1` should come first, positive if `obj2` should come first, and zero if they're equal. Sorting algorithms call this repeatedly to decide the final order.

- **The ascending vs descending trick — swapping arguments:** `Double.compare(e1.getValue(), e2.getValue())` produces ascending order (smaller salary first) because it returns negative when `e1`'s salary is smaller. Simply swapping the arguments to `Double.compare(e2.getValue(), e1.getValue())` reverses the entire ordering to descending (larger salary first) — no other logic needs to change, just the order the two values are compared in.

- **Anonymous class syntax:** `new Comparator<Map.Entry<String, Double>>() { @Override public int compare(...) {...} }` creates a one-off implementation of the `Comparator` interface directly at the point of use, without needing to define a separate named class file for it — useful when the custom logic is only needed in one place.

## 🕹️ How to Run
```bash
javac EmployeePayrollSystem.java
java EmployeePayrollSystem
```

## 🚀 Possible Improvements (Future Scope)
- Replace the anonymous `Comparator` classes with lambda expressions (e.g., `(e1, e2) -> Double.compare(e2.getValue(), e1.getValue())`) for more concise code
- Use `Comparator.comparing()` and `.reversed()` from `java.util.function` for a more modern approach
- Add employee IDs to handle duplicate names properly (currently, adding the same name twice overwrites the previous salary)
- Add department-wise grouping and subtotal calculations

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
