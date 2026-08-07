# Day 28: Producer-Consumer Problem

## 📌 Overview
A classic multithreading demonstration where a `Producer` thread continuously adds items to a shared buffer, and a `Consumer` thread continuously removes them. The buffer has a fixed capacity — the Producer waits when it's full, and the Consumer waits when it's empty, using Java's built-in `wait()`/`notify()` mechanism for thread coordination.

## 🎯 Concepts Covered
- **`synchronized` methods** – ensuring only one thread can execute a method on a shared object at a time, preventing race conditions
- **`wait()`** – pausing a thread and releasing its lock until another thread calls `notify()`
- **`notify()`** – waking up a thread that's waiting on the same object's lock
- **`Runnable` interface** – defining the code a thread should run, separate from the `Thread` class itself
- **`Thread.sleep()`** – simulating time delay to make the producer/consumer timing visible in the output

## 🧠 What I Learned

- **Why `synchronized` is essential here:** Both `produce()` and `consume()` read and modify the same shared `queue`. Without `synchronized`, both threads could check and change the queue's state at the exact same moment, corrupting it (e.g., both thinking there's room to add an item when there isn't). `synchronized` ensures only one thread is inside `produce()` or `consume()` at any given time.

- **`while` instead of `if` around the wait condition:** After `wait()` returns (because some thread called `notify()`), the woken thread does *not* automatically know the condition is now actually true — it just knows it was told to check again. Using `while (queue.size() == capacity)` instead of `if` means the condition is re-checked after waking up, which matters especially if multiple threads could be waiting and only one gets to proceed.

- **What `wait()` actually does:** Unlike `Thread.sleep()` (which just pauses for a fixed time regardless of anything else), `wait()` releases the object's lock and pauses the thread *specifically* until another thread calls `notify()` on the same object — allowing other threads to get in and change the shared state in the meantime.

- **`Runnable` vs extending `Thread`:** `Producer` and `Consumer` implement `Runnable` (defining a `run()` method) rather than extending `Thread` directly. This is generally preferred because a class can only extend one parent (recall the "extends vs implements" lesson from Day 14) — implementing `Runnable` keeps the class free to extend something else if ever needed, and separates "what the thread does" from "the thread itself."

- **Different sleep durations create realistic buffering behavior:** The Producer sleeps 300ms between items while the Consumer sleeps 500ms — since the Consumer is slower, the buffer naturally fills up over time, which is what actually triggers the "Buffer full! Producer waiting..." messages during a run.

## 🕹️ How to Run
```bash
javac ProducerConsumerProblem.java
java ProducerConsumerProblem
```
The program runs indefinitely (Producer and Consumer loop forever) — stop it manually (Ctrl+C) to end.

## 🚀 Possible Improvements (Future Scope)
- Replace `wait()`/`notify()` with Java's higher-level `BlockingQueue` (from `java.util.concurrent`), which handles this coordination internally
- Add multiple producers and/or consumers sharing the same buffer
- Add a graceful shutdown mechanism instead of requiring a forced stop
- Log timestamps alongside each produce/consume event

---
*Part of the [java-30-day-challenge](../) series — learning Java core concepts by building one project a day.*
