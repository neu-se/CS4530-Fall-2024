---
layout: page
title: Socket.IO Tutorial
permalink: /tutorials/week5-socketio-basics
parent: Tutorials
nav_order: 7
---

This tutorial covers the basic concepts of Socket.IO. By the end of the tutorial, you'll have an introduction to the concept of sockets for client-server communication, understand in what situations they are useful, and learn how to emit and listen for events for real-time updates.

Contents:

- [What is Socket.IO](#what-is-socketio)
  - [How Does It Work?](#how-does-it-work)
  - [Socket.IO vs. REST APIs](#socketio-vs-rest-apis)
  - [Example Uses](#example-uses)
- [Set Up a New Project](#set-up-a-new-project)
- [Emitting & Receiving Socket Events](#emitting-and-receiving-socket-events)
- [Useful Resources](#useful-resources)

# What is Socket.IO?

Socket.IO is a library that enables real-time, bidirectional, and persistent communication between client(s) and server(s). Bi-directional means that both the client and the server can send or receive messages. These features make it particularly useful for applications requiring continuous data sharing, such as live dashboards and chat apps.

## How Does It Work?

Socket.IO follows the ["observer pattern" or "listener pattern"](https://neu-se.github.io/CS4530-Fall-2024/modules/5-interaction-level-design-patterns) discussed in class. In this context:

- **Publisher** - A publisher can be identified where `.emit` is used. This _emits_ (sends) out data to the specified channel, making it available to any _subscriber_ to the channel.
- **Subscriber** - A subscriber can be identified where `.on` is used. This listens for updates emitted by a _publisher_ to the specified channel and executes the handler function (if applicable).

The code implementations below explore this in more depth.

Internally, Socket.IO establishes WebSocket connections where possible to send data. You can read more about the protocols in the [documentation](https://socket.io/docs/v4/how-it-works/).

## Socket.IO vs. REST APIs

A brief comparison between communication with Socket.IO and REST APIs:

| Feature            | Socket.IO                               | REST API                              |
| ------------------ | --------------------------------------- | ------------------------------------- |
| **Design Pattern** | Bidirectional, Publisher-Subscriber     | Server -> Client Response, Data-pull  |
| **Connection**     | Persistent (WebSocket or fallback)      | Temporary (HTTP request)              |
| **Use Cases**      | Real-time, low-latency data sharing     | CRUD operations, static data          |
| **Data Flow**      | Server and client can send data anytime | Client-initiated requests (on-demand) |
| **Statefulness**   | Stateful                                | Stateless                             |

## Example Uses:

Socket.IO is great for any use case where real-time updates are essential, or when the client and server need continuous communication. A few examples are:

1. Chat Room - This is a simple use case outlined in the documentation (linked below). Users need to send and receive messages in real-time (instantly). With Socket.IO, the user can emit a message to the server, which then broadcasts it with the other connected users. If you were to use a REST API here, there would a lot of overhead and latency in sending/receiving messages due to the constant need of sending requests to the API.

2. Multiplayer Games - Real-time game state sharing with low latency is essential for smooth mutliplayer gameplay. By emitting socket events with the updated game state, you can make sure that all of the connected player clients have the same, synchronized copy of the game state to display.

3. Collaborative Tools - For applications like collaborative text editors or whiteboards, sockets can help keep the state synchronized across the clients. When a user makes a change, the change will be emitted to the server, which may internall update the "source of truth" for the application. Then, the updated state would be emitted to all other connected clients, so that everyone sees the edits in real-time.

# Set Up a New Project

# Emitting and Receiving Socket Events

Notes to include here:

- Creating a socket object on client/server
- Setting up a connection
- Emitting an update + object with the update
- Subscribing a listener to an update + handler function for emitted object

# Useful Resources

- [Socket.IO Introduction (Documentation)](https://socket.io/docs/v4/tutorial/introduction)
- [Socket.IO Chat App Tutorial (Documentation)](https://socket.io/get-started/chat)
- [Learn Socket.io In 30 Minutes - Web Dev Simplified](https://www.youtube.com/watch?v=ZKEqqIO7n-k)
