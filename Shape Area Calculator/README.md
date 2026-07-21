# Day 12: Shape Area Calculator (Abstraction)

## 📌 Overview
A console-based program that calculates the area of different shapes — Circle, Rectangle, and Triangle — using an `abstract` base class. Each shape provides its own area formula, and all shapes are processed together through a single `Shape[]` array.

## 🎯 Concepts Covered
- **Abstraction** – defining *what* every shape must do (`calculateArea()`) without specifying *how*, since a generic "shape" has no sensible default area
- **`abstract class`** – a class that cannot be instantiated directly and exists purely as a base for other classes
- **`abstract method`** – a method with no body in the parent class, forcing every subclass to provide its own implementation
- **Concrete (non-abstract) methods inside an abstract class** – `displayArea()` is fully implemented in `Shape` and shared by all subclasses, while `calculateArea()` is left abstract
- **Polymorphism** – storing `Circle`, `Rectangle`, and `Triangle` objects together in a single `Shape[]` array

## 🧠 What I Learned

- **Why `Shape` needed to be `abstract`:** In the Day 11 Employee project, `Employee.calculateSalary()` had a sensible default (just return `baseSalary`). But there's no sensible "default area" for a generic shape — the concept is incomplete without knowing the specific shape. Making `calculateArea()` `abstract` forces every subclass to supply its own formula; there's no fallback that could silently produce a wrong or meaningless value.

- **`abstract class` vs regular class:** Unlike `Employee` (Day 11), `Shape` **cannot** be instantiated directly — `new Shape("test")` is a compile error. Only concrete subclasses like `Circle`, `Rectangle`, and `Triangle` (which have implemented `calculateArea()`) can actually be created with `new`.

- **Mixing abstract and concrete methods in one class:** `Shape` has both an abstract method (`calculateArea()` — no body) and a regular method (`displayArea()` — fully implemented). `displayArea()` internally calls `calculateArea()`, and thanks to polymorphism, it automatically calls whichever subclass's version is appropriate — this is the same principle from Day 11, just now enforced by the compiler rather than being optional.

- **Compiler enforcement:** If a subclass of `Shape` forgets to implement `calculateArea()`, Java refuses to compile it with an error like *"X is not abstract and does not override abstract method calculateArea()."* This is the core benefit of abstraction — it's not just a design suggestion, it's a compile-time guarantee that every shape will know how to calculate its own area.

## 🕹️ How to Run
```bash
javac ShapeAreaCalculator.java Shape.java Circle.java Rectangle.java Triangle.java
java ShapeAreaCalculator
```

## 🚀 Possible Improvements (Future Scope)
- Add more shapes (Square, Trapezoid, Parallelogram)
- Add a `calculatePerimeter()` abstract method alongside `calculateArea()`
- Read shape dimensions from user input instead of hardcoding them
- Explore the difference between `abstract class` and `interface` (coming up on Day 13)

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
