# Day 11: Employee Management System

## 📌 Overview
A console-based payroll system demonstrating inheritance and polymorphism. A base `Employee` class holds common properties, while `Manager`, `Developer`, and `Intern` subclasses each calculate salary differently. All employee types are stored and processed together through a single `Employee[]` array, showcasing runtime polymorphism.

## 🎯 Concepts Covered
- **Inheritance (`extends`)** – `Manager`, `Developer`, and `Intern` inherit common fields and behavior from `Employee` instead of duplicating them
- **`protected` access modifier** – fields accessible to subclasses but not to outside code
- **`super()`** – calling the parent class constructor from a subclass constructor
- **Method Overriding (`@Override`)** – each subclass provides its own version of `calculateSalary()` and `getRole()`
- **Runtime Polymorphism** – storing different subclass objects in a single `Employee[]` array, where the correct overridden method runs automatically based on the object's actual type

## 🧠 What I Learned

- **Why inheritance avoids duplication:** Without inheritance, `name`, `employeeId`, and `baseSalary` — along with the printing logic in `displayInfo()` — would have to be rewritten in every employee type class. With `extends Employee`, each subclass automatically gets all of this for free and only needs to add what's actually different about it.

- **`super(...)` delegates setup to the parent:** Inside `Manager`'s constructor, `super(name, employeeId, baseSalary)` calls `Employee`'s constructor to handle the common fields, so `Manager` only needs to set its own extra field (`bonus`).

- **The "IS-A" relationship:** Because `Manager extends Employee`, a `Manager` object **is an** `Employee` — which is why `Employee[] employees` can legally hold `Manager`, `Developer`, and `Intern` objects all in the same array, even though it's typed as `Employee[]`.

- **How polymorphism actually resolves at runtime:** `displayInfo()` is defined only once, in `Employee`, and is never overridden by any subclass. Yet it internally calls `calculateSalary()` and `getRole()` — and when the loop runs `emp.displayInfo()`, Java looks at what the object **actually is** (Manager, Developer, or Intern) at runtime and runs *that* object's overridden versions of those two methods, not `Employee`'s default ones. This is what "runtime polymorphism" means — the method that executes depends on the object's real type, not the variable's declared type.

- **Code reuse + customization together:** This is the real benefit of inheritance — shared logic (`displayInfo()`) is written once, while each subclass customizes only the specific behavior it needs (`calculateSalary()`), without touching or duplicating the shared logic.

## 🕹️ How to Run
```bash
javac EmployeeManagementSystem.java Employee.java Manager.java Developer.java Intern.java
java EmployeeManagementSystem
```

## 🚀 Possible Improvements (Future Scope)
- Convert `Employee` into an `abstract class` and make `calculateSalary()` an abstract method, forcing every subclass to implement it (ties into Day 12's abstraction concepts)
- Add a `raiseSalary()` method with role-specific raise percentages
- Read employee data from user input instead of hardcoding it
- Sort employees by salary using `Comparator`

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
