# Day 22: File-Based Notes App

## 📌 Overview
A console-based notes app that persists notes to a text file (`notes.txt`), so notes survive between program runs — unlike every previous project, where all data was lost the moment the program closed.

## 🎯 Concepts Covered
- **`FileWriter`** – writing text data to a file, with an append mode to avoid overwriting existing notes
- **`BufferedReader` + `FileReader`** – reading a file line by line
- **`IOException`** – Java's checked exception for file operations, which must be handled with `try-catch` or the code won't compile
- **`try-with-resources`** – automatically closing file streams once the block finishes, even if an error occurs
- **Persistence** – data surviving beyond a single program run, by storing it outside of memory

## 🧠 What I Learned

- **Why every previous project's data disappeared on exit:** Everything in earlier projects (`ArrayList`, `HashMap`, arrays) only exists in RAM while the program is running. The moment `main()` finishes, that memory is released and the data is gone. Writing to a file stores the data on disk instead, so it's still there the next time the program runs.

- **Append mode (`true` in `new FileWriter(FILE_NAME, true)`):** Without this flag, every call to `addNote()` would completely overwrite `notes.txt`, leaving only the most recent note. `true` tells `FileWriter` to add new content to the *end* of the file instead, preserving everything written before.

- **`readLine()` returning `null` as the "end of file" signal:** `BufferedReader.readLine()` returns one line at a time, and returns `null` once there's nothing left to read. The pattern `while ((line = reader.readLine()) != null)` reads a line, immediately checks if it was the last one, and loops until the file is fully read — a very common Java idiom for reading files line by line.

- **Why `IOException` had to be handled here but wasn't optional:** Unlike a custom exception (Day 18) that's used at the developer's discretion, `IOException` is a *checked* exception built into Java — file operations can fail in ways outside the program's control (missing file, permission issues), so the compiler forces a `try-catch` around any code that might throw it.

- **`try-with-resources`:** Writing `try (FileWriter writer = new FileWriter(...)) { ... }` automatically closes the file resource once the block ends — even if an exception is thrown partway through — removing the need to manually call `.close()` in every possible exit path.

- **Handling a file that doesn't exist yet:** The first time `viewAllNotes()` runs (before any note has ever been added), `notes.txt` doesn't exist, and trying to open it for reading throws an `IOException`. Rather than crashing, the `catch` block treats this case as "no notes yet" — a friendly message instead of an error.

## 🕹️ How to Run
```bash
javac NotesApp.java
java NotesApp
```
Notes are saved in a `notes.txt` file created in the same directory as the program.

## 🚀 Possible Improvements (Future Scope)
- Add timestamps to each note when it's saved
- Add a "Delete Note" feature (would require rewriting the whole file, since individual lines can't be removed directly)
- Store notes in a structured format (e.g., CSV) instead of plain text
- Add note categories or tags

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
