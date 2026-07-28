# Day 19: Movie Ticket Booking (Console)

## 📌 Overview
A console-based movie seat booking system using `HashSet` to naturally prevent double-booking. Supports booking a seat, viewing booked/available seats, and cancelling a booking.

## 🎯 Concepts Covered
- **`HashSet<Integer>`** – a collection that only stores unique values, making it a natural fit for tracking booked seats (no seat should ever be booked twice)
- **`.add()` return value** – using the `boolean` returned by `.add()` to detect whether a seat was newly booked or was already taken
- **`.contains()`** – checking whether a value exists in the set, used here to determine which seats are still available
- **`.remove()` return value** – using the `boolean` returned by `.remove()` to confirm whether a cancellation actually happened

## 🧠 What I Learned

- **How `HashSet` naturally prevents duplicates:** Calling `bookedSeats.add(seatNo)` on a seat number that's already in the set doesn't throw an error or add a duplicate — it just does nothing and returns `false`. This maps perfectly onto the real-world rule "a seat can only be booked once," without needing any manual duplicate-checking logic before calling `.add()`.

- **Finding available seats without storing them:** Since `HashSet` only tracks *booked* seats, available seats aren't stored anywhere directly. Instead, `viewAvailableSeats()` loops through every possible seat number (`1` to `TOTAL_SEATS`) and checks `!bookedSeats.contains(seat)` — any seat not found in the booked set is available.

- **Comparing collections so far:**
  - `ArrayList` (Day 15) — ordered, allows duplicates, accessed by index
  - `HashMap` (Day 16–17) — key-value pairs, unique keys, accessed by key
  - `HashSet` (today) — only unique values, no index, accessed only by checking membership (`.contains()`)
  
  Each collection fits a different kind of problem: a list of contacts (ArrayList), a lookup table (HashMap), and a "has this already happened" tracker (HashSet).

- **Printing a `HashSet` directly:** `System.out.println(bookedSeats)` automatically formats the set as `[3, 7, 12]` without needing a manual loop — the same convenience also works for `ArrayList` and `HashMap`.

## 🕹️ How to Run
```bash
javac MovieTicketBooking.java
java MovieTicketBooking
```

## 🚀 Possible Improvements (Future Scope)
- Add multiple show timings, each with its own separate `HashSet` of booked seats
- Add seat categories (Regular/Premium) with different pricing
- Sort and display booked/available seats in order (a `HashSet` doesn't guarantee this — a `TreeSet` would)
- Add a simple seating layout visualization instead of a plain number list

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
