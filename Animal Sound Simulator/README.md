# Day 13: Animal Sound Simulator (Interfaces)

## 📌 Overview
A console-based simulator where different animals (Dog, Cat, Cow, Bird) each make their own sound, all through a shared `Animal` interface. Also demonstrates a class implementing multiple interfaces at once (`Dog` implements both `Animal` and `Pet`).

## 🎯 Concepts Covered
- **`interface`** – defining a pure contract with no implementation, only method signatures
- **`implements` keyword** – how a class agrees to fulfill an interface's contract
- **Multiple interface implementation** – a single class implementing more than one interface, something not possible with class inheritance (`extends`)
- **Polymorphism via interface type** – storing different classes in an `Animal[]` array, since they all share the same interface

## 🧠 What I Learned

- **Interface vs Abstract Class:** In the Day 12 Shape project, `Shape` (an abstract class) had both abstract *and* fully implemented methods, plus instance fields. An `interface` is different — by default, every method in it is implicitly `public` and `abstract` (no body at all), and interfaces can't hold instance fields the way a class can. Interfaces are used purely to define **what** a class must do, not to share any common implementation.

- **`implements` vs `extends`:** Classes use `extends` for inheriting from another class, but `implements` for fulfilling an interface's contract. The keyword difference reflects a real distinction: extending shares code, implementing only promises behavior.

- **A class can implement multiple interfaces:** `Dog implements Animal, Pet` — separating interface names with a comma lets one class fulfill multiple contracts simultaneously. This is a genuine advantage over class inheritance, where Java only allows extending **one** parent class. This is how Java works around not supporting "multiple inheritance" through classes.

- **Why this fits animals well:** Every animal makes a sound, but the actual sound has zero shared logic between species — there's nothing common to put in a base class. A `interface` (pure contract, no shared code) is a better fit here than an `abstract class`, which would be more appropriate if there *were* common logic to share (like `Shape`'s `displayArea()` in Day 12).

## 🕹️ How to Run
```bash
javac AnimalSoundSimulator.java Animal.java Pet.java Dog.java Cat.java Cow.java Bird.java
java AnimalSoundSimulator
```

## 🚀 Possible Improvements (Future Scope)
- Add a `Movement` interface (`walk()`, `fly()`, `swim()`) and mix-and-match it across animals (e.g., `Bird implements Animal, Movement`)
- Explore Java 8 `default` methods in interfaces (methods with a body, but overridable)
- Add an `Animal` factory that creates random animals for a bigger simulation

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
