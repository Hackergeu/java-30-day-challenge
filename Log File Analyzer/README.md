# Day 26: Log File Analyzer

## 📌 Overview
A console-based log file analyzer that reads a server/application-style log file, counts log entries by level (`INFO`, `WARNING`, `ERROR`), and filters + displays only the `ERROR` entries along with their extracted timestamps. If the log file doesn't already exist, the program generates a sample one automatically.

## 🎯 Concepts Covered
- **File I/O** – checking for file existence (`File.exists()`) and reading a file line-by-line (`Files.readAllLines()`)
- **`Pattern` and `Matcher`** – Java's regex engine, used to extract structured data (timestamps) from unstructured text
- **`Pattern.compile()`** – compiling a regex into a reusable object instead of re-parsing it on every call
- **`.find()` and `.group()`** – checking for a regex match and pulling out the matched text
- **`HashMap<String, Integer>`** – tracking counts per log level using `getOrDefault()`
- **`String.contains()`** – simple substring search, used where full regex power isn't needed

## 🧠 What I Learned
- **`.contains()` vs `Pattern`/`Matcher` — picking the right tool**: For finding a fixed keyword like `"ERROR"` anywhere in a line, `.contains()` is simpler, faster to read, and does the job. Regex earns its keep when you need to match a *structure* (like a timestamp's digit-hyphen-colon pattern) rather than a literal string, or when you need to know *which* of several alternatives matched.
- **Why timestamps need regex, not `.contains()`**: A timestamp like `2024-01-15 10:23:45` isn't a fixed string — it's a pattern (4 digits, hyphen, 2 digits, hyphen, 2 digits, space, 2 digits, colon, 2 digits, colon, 2 digits). `.contains()` has no way to express "any digit here," so extracting it required `Pattern.compile("\\d{4}-\\d{2}-\\d{2} \\d{2}:\\d{2}:\\d{2}")` and `matcher.find()` + `matcher.group()`.
- **`Pattern.compile()` is reusable on purpose**: Compiling the pattern once outside the loop (instead of inside it) avoids re-parsing the same regex for every line — the `Matcher` object is what gets recreated per line via `pattern.matcher(line)`, not the `Pattern` itself.
- **`getOrDefault()` for counting**: Same pattern as Day 21 — `levelCount.getOrDefault(level, 0) + 1` avoids null checks or manual "does this key exist yet" logic when building up counts in a `HashMap`.

## 🕹️ How to Run
```
javac LogFileAnalyzer.java
java LogFileAnalyzer
```
On first run (no `app.log` present), a 10-line sample log file is generated automatically in the project directory, then immediately parsed.

## 🚀 Possible Improvements (Future Scope)
- Extract full log entries into a `LogEntry` class (timestamp, level, message) instead of re-parsing raw lines each time
- Support filtering by a custom date/time range using the extracted timestamps
- Write filtered logs (e.g., all `ERROR` entries) out to a separate file
- Accept a log file path as a command-line argument instead of hardcoding `app.log`
- Add support for multi-line log entries (e.g., stack traces following an `ERROR` line)

---
Part of the [java-30-day-challenge](https://github.com/Hackergeu/java-30-day-challenge/blob/main) series — learning Java core concepts by building one project a day.
