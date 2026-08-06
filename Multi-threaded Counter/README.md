# Day 27: Multi-threaded Counter

## 📌 Overview
A console program that demonstrates race conditions and how to fix them. Four threads increment a shared counter 1000 times each — first **without** synchronization (showing the final value come out wrong and inconsistent), then **with** `synchronized` (showing the final value come out correct every single time).

## 🎯 Concepts Covered
- **`Thread`** – an independent execution path running alongside `main`
- **`Runnable` interface** – defining a thread's work by implementing `run()`, then wrapping it in a `Thread` object
- **`.start()` vs `.run()`** – `.start()` spins up a new thread and runs `run()` on it; calling `.run()` directly just runs the code on the current thread, like a normal method call
- **Race condition** – multiple threads reading and writing a shared variable at the same time, causing lost updates
- **`synchronized`** – ensuring only one thread can execute a critical section at a time
- **`join()`** – making one thread wait for another thread to finish before continuing

## 🧠 What I Learned
- **Why `counter++` isn't safe**: it looks like one operation but is actually three — read the value, add 1, write it back. If two threads interleave between these steps, one thread's increment can get silently overwritten by another's, and the final count ends up lower than expected.
- **Why the "wrong" answer changes every run**: race conditions depend on the exact timing of when threads get scheduled by the OS, which isn't fixed. That's what makes them dangerous — the bug doesn't show up consistently, so it's easy to miss in testing.
- **`synchronized` on a static method locks the class, not an instance**: since `increment()` is `static`, the lock is held on `MultiThreadedCounter.class` itself. Any thread trying to enter `increment()` while another thread is inside it has to wait its turn — no two threads can be inside that method for this class at the same time.
- **Why `join()` matters here**: without calling `join()` on each thread, `main` would move on to `System.out.println(unsafeCounter)` immediately after `.start()` — potentially before the threads have finished (or even started) incrementing. `join()` blocks `main` until that specific thread has completed, so the counter is only printed once all the work is actually done.

## 🕹️ How to Run
```
javac MultiThreadedCounter.java
java MultiThreadedCounter
```
Expected final value is `4000` (4 threads × 1000 increments) both times — but only the `synchronized` version will reliably print `4000`. Run the program a few times to see the unsynchronized version produce a different (and usually lower) number each time.

## 🚀 Possible Improvements (Future Scope)
- Replace manual `synchronized` with `java.util.concurrent.atomic.AtomicInteger` and compare performance/readability
- Use `ExecutorService` instead of manually creating and joining `Thread` objects
- Add timing (`System.nanoTime()`) to compare how much slower the synchronized version is
- Demonstrate `synchronized` on an object instance instead of a static method, using an actual `Counter` class

---
Part of the [java-30-day-challenge](https://github.com/Hackergeu/java-30-day-challenge/blob/main) series — learning Java core concepts by building one project a day.
