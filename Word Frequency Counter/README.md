# Day 21: Word Frequency Counter

## 📌 Overview
A console-based program that takes a sentence or paragraph from the user, cleans it up (removes punctuation, normalizes case), and counts how many times each word appears using a `HashMap`. Also identifies the single most frequent word.

## 🎯 Concepts Covered
- **String cleaning** – `.toLowerCase()` to normalize case, `.replaceAll()` with a regex to strip punctuation
- **`.split("\\s+")`** – splitting text into words using one-or-more whitespace characters as the delimiter
- **`HashMap<String, Integer>`** – mapping each unique word to its occurrence count
- **`.getOrDefault(key, default)`** – a concise way to handle "increment if exists, otherwise start at 1" logic
- **Regex basics** – using a character-class pattern (`[^a-z0-9\\s]`) to match and remove unwanted characters

## 🧠 What I Learned

- **Why cleaning the text matters before counting:** Without normalizing case, `"The"` and `"the"` would be counted as two different words. Without removing punctuation, `"sat."` and `"sat"` would also be treated as different words, even though they're really the same word. Cleaning the text *before* splitting and counting ensures accurate frequency counts.

- **The regex `[^a-z0-9\\s]`:** The `^` inside `[...]` means "NOT these characters." So this pattern matches any character that is *not* a lowercase letter, digit, or whitespace — essentially all punctuation — and `replaceAll()` replaces every match with an empty string, effectively deleting it.

- **`.split("\\s+")` vs `.split(" ")`:** Splitting on a single space (`" "`) would create empty "words" if there were multiple consecutive spaces in the input (e.g., double spaces between words). `"\\s+"` means "one or more whitespace characters," so any amount of spacing between words is treated as a single delimiter, avoiding empty strings in the result.

- **`getOrDefault()` simplifies the counting logic:** Without it, counting would need an explicit check:
  ```java
  if (frequency.containsKey(word)) {
      frequency.put(word, frequency.get(word) + 1);
  } else {
      frequency.put(word, 1);
  }
  ```
  `frequency.getOrDefault(word, 0) + 1` does the same thing in one line — if the word exists, its current count is returned; if not, `0` is returned as a fallback, and either way `+1` gives the correct new count to store.

- **Finding the most frequent word reuses the Day 17 "running maximum" pattern:** Just like finding the topper in the Student Result Portal, this loops through `entrySet()` while tracking the highest count seen so far and the word associated with it.

## 🕹️ How to Run
```bash
javac WordFrequencyCounter.java
java WordFrequencyCounter
```

## 🚀 Possible Improvements (Future Scope)
- Sort and display words by frequency (highest first), reusing the Day 20 `Comparator` + `List` pattern
- Read text from a file instead of manual console input (ties into Day 22's File I/O concepts)
- Exclude common "stop words" (the, is, at, on) from the frequency count
- Handle apostrophes properly (e.g., "don't" currently becomes "dont" after cleaning)

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
