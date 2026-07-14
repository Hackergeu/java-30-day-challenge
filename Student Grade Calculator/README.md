# Day 5: Student Grade Calculator

## 📌 Overview
A console-based program that takes marks for multiple subjects from the user, calculates the total and percentage, and assigns a grade based on the percentage scored. Includes validation to ensure both the number of subjects and individual marks are within valid ranges.

## 🎯 Concepts Covered
- **Arrays** – storing marks for multiple subjects in a single `int[]` array
- **Nested loops** – an outer `for` loop iterating over subjects, with an inner `do-while` loop validating each individual mark entry
- **Type casting** – converting `int` division into accurate `double` division for percentage calculation
- **Methods** – separating grade-decision logic (`calculateGrade()`) from the main flow
- **`printf` formatted output** – displaying the percentage rounded to 2 decimal places

## 🧠 What I Learned

- **Type casting for correct percentage:** Since both `total` and `n` are `int`, writing `total / n` directly would perform **integer division**, silently dropping the decimal part (e.g., `171 / 2` would give `85`, not `85.5`). Casting with `(double) total / n` forces the division to happen in floating-point, giving the correct decimal result.

- **Nested loop flow:** The outer `for` loop controls which subject we're on (`i = 0` to `n-1`), while the inner `do-while` loop keeps re-asking for input **only when the entered marks are invalid** (outside 0–100). Once valid marks are entered, the `do-while` exits, and *then* — outside the `do-while` but still inside the `for` loop — the value is stored in the array (`marks[i] = subjectMarks`) and added to the running total.

- **Why `do-while` for validation:** A `do-while` loop guarantees the input is read at least once before checking the condition, which fits naturally with "ask for input, then check if it's valid, repeat if not."

- **Order matters in `if-else if` chains:** In `calculateGrade()`, conditions are checked from highest percentage to lowest (`>= 90` first, then `>= 80`, etc.). Since the chain returns immediately on the first matching condition, checking in the wrong order (e.g., checking `>= 40` first) would cause every higher percentage to also incorrectly match the lowest condition first.

- **`printf` formatting:** `%.2f` formats a `double` to exactly 2 decimal places, and `%%` is needed to print a literal `%` symbol (since a single `%` is a special format character).

## 🕹️ How to Run
```bash
javac StudentGradeCalculator.java
java StudentGradeCalculator
```

## 📊 Grading Scale
| Percentage | Grade |
|-----------|-------|
| 90% and above | A+ |
| 80% – 89% | A |
| 70% – 79% | B |
| 60% – 69% | C |
| 40% – 59% | D |
| Below 40% | Fail |

## 🚀 Possible Improvements (Future Scope)
- Store subject names alongside marks (would need a second array or a `Map`)
- Add a class-level average calculator for multiple students
- Export results to a file instead of just printing to console

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
