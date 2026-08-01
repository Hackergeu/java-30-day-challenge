# Day 23: CSV Parser (Basic)

## 📌 Overview
A console-based program that reads a CSV (Comma-Separated Values) file, parses each row into columns, and displays the data as a formatted table. If the CSV file doesn't already exist, the program creates a sample one automatically.

## 🎯 Concepts Covered
- **CSV format** – a plain-text tabular format where commas separate columns and newlines separate rows
- **Combining File I/O + String splitting** – reusing `BufferedReader` (Day 22) together with `.split(",")` (Day 21) to turn raw text into structured data
- **Header vs data row handling** – treating the first line of a CSV differently from the rest
- **Basic data validation** – detecting and skipping malformed rows instead of crashing
- **`File.exists()`** – checking whether a file is already present before creating a new one
- **`StringBuilder`** – efficiently building a formatted string piece by piece inside a loop

## 🧠 What I Learned

- **Parsing a CSV row is just splitting on commas:** `line.split(",")` turns `"Rahul,22,85"` into the array `["Rahul", "22", "85"]` — the same `.split()` method from Day 21's Word Frequency Counter, just with a comma delimiter instead of whitespace.

- **The "first line is different" pattern:** A `boolean isFirstLine` flag, checked at the top of the loop, lets the header row be handled separately (stored and printed as column titles) before switching to normal per-row processing for the rest of the file — a reusable pattern for any file with a header line.

- **Guarding against malformed rows:** If a row has fewer or more commas than expected (e.g., `"Rahul,22"` missing the marks column), trying to access `columns[2]` directly would throw an `ArrayIndexOutOfBoundsException` and crash the program. Comparing `columns.length` to the expected `headers.length` *before* accessing any specific index catches this safely and skips just that row instead of crashing the whole parse.

- **`File.exists()` for one-time setup:** Rather than always overwriting the CSV with hardcoded sample data, checking `file.exists()` first means the sample file is only created once — if the user manually edits `students.csv` later, those changes won't be wiped out on the next run.

- **`StringBuilder` for building formatted output:** Instead of repeatedly concatenating strings with `+` inside a loop (which creates a new `String` object every time, wasting memory), `StringBuilder.append()` modifies a single growing buffer, then `.toString()` converts it to a final string once — a more efficient approach when building text piece by piece.

## 🕹️ How to Run
```bash
javac CSVParser.java
java CSVParser
```
On the first run, this creates `students.csv` in the same directory with sample data if it doesn't already exist.

## 🚀 Possible Improvements (Future Scope)
- Handle commas *inside* quoted values properly (e.g., `"Delhi, India"` as a single field) — real CSV parsing needs to account for this
- Store parsed rows into `Student` objects instead of just printing them
- Allow the user to specify which CSV file to load
- Write parsed/modified data back out to a new CSV file

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
