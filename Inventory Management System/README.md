# Day 16: Inventory Management System

## 📌 Overview
A console-based inventory system using a `HashMap` to store products as key-value pairs (product name → quantity). Supports adding, viewing, updating, removing, and searching products, all through fast key-based lookups instead of looping through a list.

## 🎯 Concepts Covered
- **`HashMap<String, Integer>`** – storing data as key-value pairs instead of an indexed list
- **Key-based lookups** – accessing a value directly by its key, without looping through every element
- **Core `HashMap` methods** – `.put()`, `.get()`, `.containsKey()`, `.remove()`, `.keySet()`
- **Iterating a `HashMap`** – using `.keySet()` in a `for-each` loop to visit every entry

## 🧠 What I Learned

- **`HashMap` vs `ArrayList` — why keys instead of indexes:** In the Day 15 Contact Book (`ArrayList<Contact>`), finding a specific contact by name meant looping through the whole list and comparing names one by one. A `HashMap` skips that entirely — `inventory.get("Laptop")` jumps straight to the value tied to the key `"Laptop"`, without checking every other entry first.

- **`.put()` on an existing key overwrites, it doesn't add:** This distinction shaped two different methods. `updateStock()` uses `.put(name, newQty)` to completely **replace** the old quantity — appropriate for "set the stock to this exact number." `addProduct()`, on the other hand, checks `.containsKey(name)` first, and if the product already exists, it manually adds the new quantity to the existing one (`inventory.get(name) + quantity`) before calling `.put()` — appropriate for "more stock just arrived."

- **`.containsKey()` before `.get()`:** Calling `.get()` on a key that doesn't exist returns `null` rather than throwing an error, which can cause confusing bugs later (like a `NullPointerException` if the returned `null` is used in a calculation). Checking `.containsKey()` first avoids that entirely.

- **No custom class needed this time:** Unlike Day 9–14 projects (which each defined their own class like `Book` or `Account`), this project didn't need one — `HashMap<String, Integer>` already models "product name maps to a quantity" well enough on its own, keeping everything in a single file.

- **`HashMap` doesn't guarantee order:** Unlike an `ArrayList` (which preserves insertion order), a `HashMap`'s `.keySet()` can return entries in a different order than they were added. If insertion order needs to be preserved, Java's `LinkedHashMap` is the alternative — worth knowing about even if not used here.

## 🕹️ How to Run
```bash
javac InventoryManagementSystem.java
java InventoryManagementSystem
```

## 🚀 Possible Improvements (Future Scope)
- Create a `Product` class (name, quantity, price, category) instead of just tracking quantity
- Use `LinkedHashMap` to preserve the order products were added in
- Add low-stock alerts (warn when quantity falls below a threshold)
- Sort and display products by quantity using a `TreeMap` (Day 20 preview)

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
