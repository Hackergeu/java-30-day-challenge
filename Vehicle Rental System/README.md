# Day 14: Vehicle Rental System (Interfaces + Inheritance Combined)

## 📌 Overview
A console-based vehicle rental system combining an abstract class and an interface. `Vehicle` (abstract class) holds shared properties and rent-calculation logic, while `Rentable` (interface) defines the rent/return contract. `Car`, `Bike`, and `Truck` all extend `Vehicle` and implement `Rentable` together.

## 🎯 Concepts Covered
- **Abstract class + Interface together** – `Vehicle extends` provides shared state and partial behavior, while `Rentable implements` provides a pure behavioral contract
- **`extends` before `implements`** – the fixed order Java requires when a class does both
- **Abstract method overriding** – each vehicle type customizes `calculateRent()` differently
- **Interface method implementation** – `rentVehicle()`/`returnVehicle()` implemented identically across `Car`, `Bike`, `Truck`, but declared once in `Rentable`
- **Casting to an interface type** – accessing interface-only methods through a variable typed as the parent class

## 🧠 What I Learned

- **Why both an abstract class AND an interface were needed here:** `Vehicle` needed to hold actual shared state (`model`, `rentPerDay`, `isRented`) and a shared method (`displayInfo()`) — something only a class (not an interface) can do. But renting/returning behavior (`rentVehicle()`, `returnVehicle()`) is a separate *capability* that doesn't need to be tied to the vehicle hierarchy specifically — using an interface for it means other unrelated things (e.g., a `RentableEquipment` class in a totally different hierarchy) could reuse the same contract without needing to extend `Vehicle`.

- **`extends` before `implements`:** Java enforces a specific order in the class declaration — `class Car extends Vehicle implements Rentable`. A class can only extend one parent class, but can implement multiple interfaces (comma-separated) — Java requires the single class parent to be named first.

- **Truck's custom rent calculation:** Because `calculateRent()` is abstract in `Vehicle`, each subclass is *forced* to define its own version. `Truck` uses this to add a flat `HEAVY_VEHICLE_SURCHARGE` on top of the regular per-day rent — showing that overriding isn't just about giving *a* value, but genuinely different formulas per type.

- **Why casting was needed in the main class:** The `vehicles` array is typed as `Vehicle[]`, and `Vehicle` itself has no knowledge of `rentVehicle()`/`returnVehicle()` — those only exist on the `Rentable` interface. So before calling them, the object had to be explicitly cast: `Rentable rentable = (Rentable) vehicles[index];`. This is necessary because the compiler only allows calling methods that exist on the variable's *declared* type, even if the actual object supports more.

## 🕹️ How to Run
```bash
javac VehicleRentalSystem.java Vehicle.java Rentable.java Car.java Bike.java Truck.java
java VehicleRentalSystem
```

## 🚀 Possible Improvements (Future Scope)
- Since `rentVehicle()`/`returnVehicle()` are implemented identically in `Car`, `Bike`, and `Truck`, this duplication could be moved into `Vehicle` itself (making `Vehicle implements Rentable` at the abstract class level instead of repeating it in every subclass)
- Add a `Rentable` object list instead of casting from `Vehicle[]`
- Track total rental income across all vehicles
- Add a minimum rental period per vehicle type

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
