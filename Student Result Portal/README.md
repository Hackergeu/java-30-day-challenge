# Day 17: Student Result Portal

## 📌 Overview
A console-based result portal using a `HashMap<Integer, Double>` to map roll numbers to marks. Supports adding results, viewing all results with Pass/Fail status, searching by roll number, and calculating class statistics (average, topper, lowest scorer).

## 🎯 Concepts Covered
- **`HashMap<Integer, Double>`** – using a non-`String` type (`Integer`) as the key, showing that `HashMap` keys aren't limited to strings
- **Autoboxing** – Java automatically converting primitive `int`/`double` values into their wrapper classes (`Integer`/`Double`) when used with generic collections
- **`.values()`** – iterating just the values of a map when the key isn't needed
- **`Map.Entry` and `.entrySet()`** – iterating both the key and value together in a single loop, when both are needed at once

## 🧠 What I Learned

- **Why `HashMap<Integer, Double>` needs wrapper types, not primitives:** Java generics (the `<...>` part) only work with objects, not primitives — you can't write `HashMap<int, double>`. `Integer` and `Double` are the "wrapper class" versions of `int` and `double`, and Java automatically converts between them (autoboxing/unboxing) so the primitive values (like `rollNo` and `marks`) can still be used naturally in the code.

- **`.values()` vs `.entrySet()` — picking the right one:** `classAverage()` only needs the marks themselves (not who they belong to), so it loops with `results.values()` — simple and sufficient. But `findTopper()` and `findLowestScorer()` need to know *which roll number* had the extreme marks, and `.values()` alone can't provide that — it only hands over values, with no link back to their keys. Switching to `results.entrySet()` and looping with `Map.Entry<Integer, Double>` solves this: each `entry` carries both `.getKey()` (roll number) and `.getValue()` (marks) together, so both can be tracked in the same pass through the map.

- **Tracking a "running maximum/minimum" while looping:** Both `findTopper()` and `findLowestScorer()` use the same pattern — start with a value guaranteed to be beaten immediately (`highestMarks = -1` for topper since real marks can't be negative, `lowestMarks = 101` for lowest scorer since real marks can't exceed 100), then update it only when a more extreme value is found during the loop.

- **Overwriting on duplicate roll numbers:** Since `.put()` overwrites an existing key's value, adding a result for a roll number that's already in the map silently replaces the old marks — the code explicitly checks `.containsKey()` first just to inform the user this is happening, rather than letting it happen silently.

## 🕹️ How to Run
```bash
javac StudentResultPortal.java
java StudentResultPortal
```

## 🚀 Possible Improvements (Future Scope)
- Store student names alongside roll numbers (would need a `Student` class or a second map)
- Add grade classification (A+, A, B...) reusing the Day 5 grading logic
- Calculate the number of students who passed vs failed
- Sort and display results in roll-number order using `TreeMap` (Day 20 preview)

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
