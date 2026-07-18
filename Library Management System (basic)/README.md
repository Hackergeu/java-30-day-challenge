# Day 9: Library Management System (Basic)

## 📌 Overview
A console-based library system that lets a user view a catalog of books, borrow a book, and return a book. This is the first OOP-based project in the challenge — books are modeled as objects of a `Book` class rather than primitive arrays/variables.

## 🎯 Concepts Covered
- **Classes** – `Book` models a real-world entity with its own properties and behavior
- **Objects** – multiple independent `Book` instances created from the same class, each holding its own data
- **Constructors** – initializing a new `Book` object's data at the moment it's created
- **Instance variables vs `static`** – understanding why `title`, `author`, and `isAvailable` need to belong to each individual object, not be shared across the whole class
- **The `this` keyword** – disambiguating between a constructor parameter and the object's own field when they share the same name
- **Instance methods** – `displayInfo()` operates on *that specific* book's data

## 🧠 What I Learned

- **Why `static` wouldn't work here:** In earlier projects (like the ATM Simulation), `static` variables made sense because there was only ever *one* balance being shared across methods. A library, though, has *multiple* books — each with a different title, author, and availability. If `title` were `static`, there could only ever be one title for the entire class, which breaks the moment a second book is created. This is exactly why **instance variables** exist — each `new Book(...)` call creates a completely independent copy of `title`, `author`, and `isAvailable` in memory.

- **The `this` keyword:** Inside the constructor, `this.title = title;` looks confusing at first because both sides have the same name. `this.title` refers to the *object's own field*, while the plain `title` on the right refers to the *constructor's parameter*. `this` is what lets Java tell the two apart.

- **Constructors run automatically:** Writing `new Book("Java Basics", "James Gosling")` automatically triggers the constructor — there's no need to manually call a separate "setup" method afterward.

- **Objects as array elements:** Just like primitives can be stored in an array (`int[]`), objects can too (`Book[]`) — each element (`library[0]`, `library[1]`, etc.) is a reference to its own independent `Book` object.

## 🕹️ How to Run
Since this project uses two files, compile both together:
```bash
javac LibraryManagementSystem.java Book.java
java LibraryManagementSystem
```

## 🚀 Possible Improvements (Future Scope)
- Replace the fixed-size `Book[]` array with an `ArrayList<Book>` to support adding new books dynamically
- Add a `Member` class to track who borrowed which book
- Add due dates and a simple fine calculation for late returns
- Add a search feature (by title or author)

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
