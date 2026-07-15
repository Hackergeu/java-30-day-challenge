# Day 6: Pattern Printing Program

## 📌 Overview
A console-based menu program that prints four different star patterns — Square, Right Triangle, Pyramid, and Diamond — based on the number of rows specified by the user. The program keeps running until the user chooses to stop.

## 🎯 Concepts Covered
- **Nested loops** – an outer loop controlling rows, and inner loops controlling spaces/stars within each row
- **Loop control variables** – understanding what each loop counter represents (row number, star count, space count)
- **Pattern-to-logic translation** – converting a visual shape into loop bounds and conditions, a core problem-solving skill for interviews
- **Methods** – each pattern isolated into its own method, called via a `switch-case` menu

## 🧠 What I Learned

- **Right Triangle — the base case:** The outer loop variable `i` represents the current row. The inner loop runs from `1` to `i`, meaning row number *is* the star count — row 1 gets 1 star, row 3 gets 3 stars, and so on.

- **Pyramid — spaces before stars:** Each row needs two things before printing stars: leading spaces (to center-align it) and an odd number of stars. For `rows` total rows, at row `i`:
  - Spaces = `rows - i` (higher rows near the top need more spaces)
  - Stars = `2*i - 1` (odd progression: 1, 3, 5, 7...)
  
  This odd-number progression is what gives the pyramid its triangular symmetry — each row adds exactly 2 more stars than the previous one, one on each side.

- **Diamond — combining two patterns:** A diamond is essentially a pyramid stacked on top of an *inverted* pyramid. The top half loops `i` from `1` to `rows` (like a normal pyramid). The bottom half loops `i` from `rows - 1` down to `1` — starting at `rows - 1` (not `rows`) avoids printing the middle row twice, since the pyramid's last row and the inverted pyramid's first row would otherwise be identical.

- **Why spacing uses `"  "` (2 chars) instead of `" "` (1 char):** Since stars are printed as `"* "` (star + space, 2 characters wide), the leading spaces also need to be 2 characters wide per unit — otherwise the pattern doesn't align correctly and looks skewed.

## 🕹️ How to Run
```bash
javac PatternPrinting.java
java PatternPrinting
```

## 🚀 Possible Improvements (Future Scope)
- Add more patterns: hollow square, hollow diamond, number/character-based triangles (Pascal's triangle style)
- Let the user choose the character used (`*`, `#`, etc.) instead of hardcoding `*`
- Add input validation to prevent negative or zero row counts

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
