# Building a React Chat App with Socket.IO

This tutorial will guide you through creating a simple chat application using React for the frontend and a mock server using Socket.IO.

## Table of Contents
1. [Setting Up the Mock Server](#setting-up-the-mock-server)
2. [Creating the React Client](#creating-the-react-client)
3. [Running the Application](#running-the-application)

## Setting Up the Mock Server

### 1. Create a new directory for your server
```bash
mkdir chat-server
cd chat-server
```

### 2. Initialize a new Node.js project
```bash
npm init -y
```

### 3. Install necessary dependencies
```bash
npm install express socket.io @types/express @types/socket.io typescript ts-node
```

### 4. Create a new file called `server.ts` with the following content:

```typescript
import express from 'express';
import http from 'http';
import { Server } from 'socket.io';

const app = express();
const server = http.createServer(app);
const io = new Server(server, {
  cors: {
    origin: "http://localhost:3000",
    methods: ["GET", "POST"]
  }
});

interface Message {
  id: string;
  user: string;
  text: string;
  timestamp: number;
}

// Mock data store
let messages: Message[] = [];

io.on('connection', (socket) => {
  console.log('A user connected');

  // Send existing messages to the new client
  socket.emit('initial messages', messages);

  // Handle new message
  socket.on('new message', (message: Omit<Message, 'id' | 'timestamp'>) => {
    const newMessage: Message = {
      id: Date.now().toString(),
      user: message.user,
      text: message.text,
      timestamp: Date.now()
    };

    messages.push(newMessage);

    // Broadcast the message to all connected clients
    io.emit('new message', newMessage);
  });

  // Handle disconnect
  socket.on('disconnect', () => {
    console.log('A user disconnected');
  });
});

const PORT = process.env.PORT || 3001;

server.listen(PORT, () => {
  console.log(`Mock server running on port ${PORT}`);
});
```

### 5. Add a script to your `package.json` to run the server:
```json
"scripts": {
  "start": "ts-node server.ts"
}
```

## Creating the React Client

### 1. Create a new React app
```bash
npx create-react-app chat-client --template typescript
cd chat-client
```

### 2. Install Socket.IO client
```bash
npm install socket.io-client @types/socket.io-client
```

### 3. Replace the contents of `src/App.tsx` with the following:

```tsx
import React, { useState, useEffect } from 'react';
import { io, Socket } from 'socket.io-client';

interface Message {
  id: string;
  user: string;
  text: string;
  timestamp: number;
}

const socket: Socket = io('http://localhost:3001');

function App() {
  const [messages, setMessages] = useState<Message[]>([]);
  const [inputMessage, setInputMessage] = useState('');

  useEffect(() => {
    socket.on('initial messages', (initialMessages: Message[]) => {
      setMessages(initialMessages);
    });

    socket.on('new message', (message: Message) => {
      setMessages(prevMessages => [...prevMessages, message]);
    });

    return () => {
      socket.off('initial messages');
      socket.off('new message');
    };
  }, []);

  const sendMessage = (e: React.FormEvent) => {
    e.preventDefault();
    if (inputMessage.trim()) {
      socket.emit('new message', { user: 'User', text: inputMessage });
      setInputMessage('');
    }
  };

  return (
    <div>
      <h1>Chat App</h1>
      <div style={{ height: '300px', overflowY: 'scroll', border: '1px solid black' }}>
        {messages.map(message => (
          <div key={message.id}>
            <strong>{message.user}:</strong> {message.text}
          </div>
        ))}
      </div>
      <form onSubmit={sendMessage}>
        <input
          type="text"
          value={inputMessage}
          onChange={(e) => setInputMessage(e.target.value)}
        />
        <button type="submit">Send</button>
      </form>
    </div>
  );
}

export default App;
```

## Running the Application

### 1. Start the server
In the `chat-server` directory:
```bash
npm start
```
You should see a message saying "Mock server running on port 3001".

### 2. Start the React app
In the `chat-client` directory:
```bash
npm start
```

### 3. Testing the application
- Make sure both the server (running on port 3001) and the client (running on port 3000) are started.
- Open your browser and go to `http://localhost:3000`. You should see the chat interface.
- Try sending a message. You should see it appear in the chat window.
- Open another browser window or tab to `http://localhost:3000`. You now have two clients connected to your chat.
- Send messages from both windows. You should see the messages appear in real-time in both windows.

This setup creates a basic, functioning chat application with a mock server. The server stores messages in memory and broadcasts them to all connected clients, while the React frontend displays messages and allows users to send new ones.

Remember, this is a simplified setup for development and testing. In a production environment, you'd want to use a real backend with a database, implement proper error handling, add authentication, and follow security best practices.
