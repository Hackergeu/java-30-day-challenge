# Day 29: Chat Application (Console, Multi-Client)

## 📌 Overview
A console-based multi-client chat application. A `ChatServer` listens for incoming connections and broadcasts every message it receives to all connected clients. Multiple `ChatClient` instances can connect at once, each able to send and receive messages simultaneously — like a basic group chat.

## 🎯 Concepts Covered
- **`ServerSocket`** – listens on a port and accepts incoming client connections
- **`Socket`** – the actual connection endpoint used to send/receive data, on both the server and client side
- **`accept()`** – a blocking call that waits until a client connects
- **Streams over a socket** – wrapping `socket.getInputStream()`/`getOutputStream()` in `BufferedReader`/`PrintWriter`, the same pattern as file I/O but over a network connection instead of a file
- **One thread per client** – the server spawns a new thread for every connected client, so handling one client never blocks the others
- **Two threads per client (listener + sender)** – the client needs to send and receive at the same time, which a single thread can't do
- **Shared broadcast list + `synchronized`** – the server keeps a list of all connected clients' writers, protected with `synchronized` since multiple client threads read/write it concurrently (same idea as Day 27/28)

## 🧠 What I Learned
- **Why the server needs a thread per client**: `in.readLine()` is a blocking call — it waits until the client sends something. If the server only had one thread, it would get stuck waiting on one client and would never be able to accept new connections or read from anyone else. Spawning a thread per client means each client's blocking read only blocks *that* client's thread.
- **Why the client needs two threads**: reading console input (`console.readLine()`) is *also* blocking. If a single thread were both reading console input and reading incoming server messages, it could only do one at a time — meaning a message from another user couldn't be shown until the user pressed Enter on their own input. Splitting into a listener thread (receiving) and the main thread (sending) lets both happen independently and at the same time.
- **Sockets are just streams underneath**: once connected, a `Socket` behaves a lot like the file streams from Day 22 — you wrap its `InputStream`/`OutputStream` in the same `BufferedReader`/`PrintWriter` classes. The networking part is really just *getting* the stream; reading/writing from it is familiar.
- **Why the shared client list needs `synchronized`**: multiple client threads can be adding themselves to `clientWriters` (on connect), removing themselves (on disconnect), or iterating over it (during `broadcast()`) all at the same time. Without synchronizing access, this is the exact same kind of race condition as Day 27 — except this time it's on a `List` instead of an `int`, and could throw a `ConcurrentModificationException` instead of just losing an update.
- **`accept()` vs a client's `readLine()`**: both block, but for different reasons — `accept()` blocks *the server's main loop* waiting for a brand new connection, while a `ClientHandler`'s `readLine()` blocks *that client's dedicated thread* waiting for the next message from an already-connected client.

## 🕹️ How to Run
Compile both files:
```
javac ChatServer.java ChatClient.java
```

Start the server first (in one terminal):
```
java ChatServer
```

Then start one or more clients (in separate terminals):
```
java ChatClient
```

Each client will be asked for a username, then can type messages that get broadcast to everyone else connected. Open at least two client terminals to see the multi-client broadcast in action.

## 🚀 Possible Improvements (Future Scope)
- Add private/direct messaging (`/msg username hello`) instead of only broadcasting to everyone
- Handle duplicate usernames instead of allowing collisions
- Add a `/list` command to show currently connected users
- Move from raw sockets to a lightweight framework (or WebSockets) for a browser-based client
- Persist chat history to a file or database so it survives server restarts

---
Part of the [java-30-day-challenge](https://github.com/Hackergeu/java-30-day-challenge/blob/main) series — learning Java core concepts by building one project a day.
