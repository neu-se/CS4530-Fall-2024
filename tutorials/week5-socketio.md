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
- [Using Socket.IO](#using-socketio)
  - [Set Up a New Project](#set-up-a-new-project)
  - [Emitting & Receiving Socket Events](#emitting-and-receiving-socket-events)
  - [Putting It All Together](#putting-it-all-together)
- [Useful Resources](#useful-resources)

# What is Socket.IO?

Socket.IO is a library that enables real-time, bidirectional, and persistent communication between client(s) and server(s). Bi-directional means that both the client and the server can send or receive messages. These features make it particularly useful for applications requiring continuous data sharing, such as live dashboards and chat apps.

## How Does It Work?

Socket.IO follows the ["observer pattern" or "listener pattern"](https://neu-se.github.io/CS4530-Fall-2024/modules/5-interaction-level-design-patterns) discussed in class. In this context:

- **Publisher** - A publisher can be identified where `.emit` is used. This _emits_ (sends) out data to the specified channel, making it available to any _subscriber_ to the channel.
- **Subscriber** - A subscriber can be identified where `.on` is used. This listens for updates emitted by a _publisher_ to the specified channel and executes a handler function (if applicable).

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

1. Chat Room - This is a simple use case outlined in the documentation (linked below). Users need to send and receive messages in real-time (instantly). With Socket.IO, the user can emit a message to the server, which then broadcasts it with the other connected users. If you were to use a REST API here, there would a lot of overhead and latency in sending/receiving messages from the need of constant requests to the API.

2. Multiplayer Games - Real-time game state sharing with low latency is essential for smooth multiplayer gameplay. By emitting socket events with the updated game state, you can make sure that all of the connected player clients have the same synchronized copy of the game state to display.

3. Collaborative Tools - For applications like collaborative text editors or whiteboards, sockets can help keep the state synchronized across the clients. When a user makes a change, the change will be emitted to the server, which may internally update the "source of truth" for the application. Then, the updated state would be emitted to all other connected clients, so that everyone sees the edits in real-time.

# Using Socket.IO

## Set Up a New Project

To get started with Socket.IO, you'll need to set up a Node.js project. Follow these steps:

1. **Initialize a Node.js Project**

   First, create a new directory for your project and navigate into it:

   ```
   mkdir socketio-tutorial
   cd socketio-tutorial
   ```

   Now initialize a new Node.js project by running the following command:

   ```
   npm init -y
   ```

   This will generate a package.json file with the default configuration.

2. **Install the Necessary Packages**

   To use Socket.IO, you'll need to install both `express` (for setting up a basic HTTP server) and `socket.io` itself. Also, you need to install `typescript`, the type definitions for both `express` and `socket.io` and some utilities to support TypeScript development.

   Run the following command to install everything that is needed for this project:

   ```
   npm install --save-dev typescript express @types/express socket.io @types/socket.io ts-node
   ```

   To configure TypeScript, you need to add a `tsconfig.json`. You can create this file manually or run:

   ```
   npx tsc --init
   ```

   This will generate a basic `tsconfig.json` with the default configuration.

3. **Set Up a Basic Server**

   Now, let's create the server. Inside your project directory, create a file called `server.ts`:

   ```
   touch server.ts
   ```

   Open `server.ts` and write the following code to create a basic HTTP server with Socket.IO:

   ```typescript
   import express, { Request, Response } from "express";
   import http from "http";
   import { Server, Socket } from "socket.io";
   import path from "path";

   const app = express();
   const server = http.createServer(app);
   const io = new Server(server);

   // Serve a simple HTML page (or use this for serving static files)
   app.get("/", (req: Request, res: Response) => {
     res.sendFile(path.join(__dirname, "index.html"));
   });

   // Set up a connection handler
   io.on("connection", (socket: Socket) => {
     console.log("A user connected");

     // Clean up when the client disconnects
     socket.on("disconnect", () => {
       console.log("A user disconnected");
     });
   });

   const PORT = 3000;
   server.listen(PORT, () => {
     console.log(`Server is running on http://localhost:${PORT}`);
   });
   ```

   This will setup a basic HTTP server that uses Socket.IO to establish connections. Now, let's create a simple client.

4. **Create a Client-Side HTML File**

   In your project directory, create a file called `index.html`:

   ```
   touch index.html
   ```

   Now, open `index.html` and add the following code:

   ```html
   <!DOCTYPE html>
   <html lang="en">
     <head>
       <meta charset="UTF-8" />
       <meta name="viewport" content="width=device-width, initial-scale=1.0" />
       <title>Socket.IO Tutorial</title>
       <script src="/socket.io/socket.io.js"></script>
     </head>
     <body>
       <h1>Hello Socket.IO!</h1>
       <script>
         const socket = io();

         // Listen for connection confirmation
         socket.on("connect", () => {
           console.log("Connected to the server");
         });

         // Listen for disconnection
         socket.on("disconnect", () => {
           console.log("Disconnected from the server");
         });
       </script>
     </body>
   </html>
   ```

   This HTML file sets up a basic client-side script that connects to the server using Socket.IO.

5. **Run Your Project**

   To start the server, run the following command:

   ```
   ts-node server.ts
   ```

   Then, open a browser and go to `http://localhost:3000`. You should see "Hello Socket.IO!" on the page, and in the browser's developer console, you'll see a message confirming the connection.

## Emitting and Receiving Socket Events

Now that you've set up a basic project, let's dive into how you can emit and receive Socket.IO events to communicate between the client and server.

1. **Creating a Socket Object on Client and Server**

   Client-Side:
   When the browser loads the HTML page, it creates a `socket` object that connects to the server.
   We've already initialized the socket object in the script section of `index.html`:

   ```typescript
   const socket = io(); // Automatically connects to the server
   ```

   Server-Side:
   On the server, Socket.IO will create a `socket` object for each client that connects. You can listen for new connections with the `io.on('connection')` event:

   ```typescript
   io.on("connection", (socket: Socket) => {
     console.log("A user connected");
   });
   ```

2. **Setting Up a Connection**

   Once the socket object is created, both the client and server can start emitting and receiving events.

   Example: Handling Connections and Disconnections

   We can already see basic connection handling:

   ```typescript
   // Server-side
   io.on("connection", (socket: Socket) => {
     console.log("A user connected");

     socket.on("disconnect", () => {
       console.log("A user disconnected");
     });
   });
   ```

   On the client-side, you can also listen for the `connect` and `disconnect` events:

   ```typescript
   // Client-side
   socket.on("connect", () => {
     console.log("Connected to the server");
   });

   socket.on("disconnect", () => {
     console.log("Disconnected from the server");
   });
   ```

3. **Emitting an Update + Object with the Update**

   To send data from the client to the server or vice versa, you use the `.emit()` method.

   Example: Emitting a Custom Event

   Let's say we want to send a chat message from the client to the server. You can emit a custom event like this:

   ```typescript
   // Client-side
   socket.emit("chat message", { user: "John", message: "Hello, World!" });
   ```

   On the server-side, you can listen for this event and handle the received data:

   ```typescript
   // Server-side
   socket.on("chat message", (data: { user: string; message: string }) => {
     console.log(`${data.user}: ${data.message}`);
   });
   ```

   You can also send data back to all connected clients:

   ```typescript
   // Server-side
   io.emit("chat message", { user: "Server", message: "Welcome to the chat!" });
   ```

4. **Subscribing a Listener to an Update + Handler Function for Emitted Object**

   On the client-side, you need to subscribe to the event to receive the emitted messages:

   ```typescript
   // Client-side
   socket.on("chat message", (data: { user: string; message: string }) => {
     console.log(`${data.user}: ${data.message}`);
   });
   ```

   This will allow the client to receive and handle chat messages sent from the server (or other clients).

## Putting It All Together

Here's an example of the sockets in a simple chat app:

Server-Side (`server.ts`):

```typescript
io.on("connection", (socket) => {
  console.log("A user connected");

  socket.on("chat message", (data: { user: string; message: string }) => {
    console.log(`${data.user}: ${data.message}`);
    // Broadcast the message to all clients
    io.emit("chat message", data);
  });

  socket.on("disconnect", () => {
    console.log("A user disconnected");
  });
});
```

Client-Side (`index.html`):

```html
<script>
  const socket = io();

  // Listen for chat messages
  socket.on("chat message", (data: { user: string, message: string }) => {
    console.log(`${data.user}: ${data.message}`);
  });

  // Example of emitting a message
  socket.emit("chat message", { user: "John", message: "Hello, World!" });
</script>
```

This example sets up a basic chat app where users can send and receive messages in real time.

# Useful Resources

- [Socket.IO Introduction (Documentation)](https://socket.io/docs/v4/tutorial/introduction)
- [Socket.IO Chat App Tutorial (Documentation)](https://socket.io/get-started/chat)
- [Learn Socket.io In 30 Minutes - Web Dev Simplified](https://www.youtube.com/watch?v=ZKEqqIO7n-k)
