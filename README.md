# Chat App - NestJS and VueJS

## Overview

This mono repository contains the code for a real-time chat application built with NestJS for the backend and Vue.js for the frontend. The communication between the server and clients is facilitated through WebSockets using the Socket.IO library.

## Technologies Used

### Backend

- **NestJS:** A progressive Node.js framework for building efficient, scalable server-side applications.
- **WebSocket:** A communication protocol that provides full-duplex communication channels over a single TCP connection.
- **Socket.IO:** A library for real-time web applications. It enables real-time, bidirectional, and event-based communication.

### Frontend

- **Vue.js:** A progressive JavaScript framework for building user interfaces. It is designed from the ground up to be incrementally adaptable.
- **WebSocket:** Used on the client side to establish a connection with the server for real-time communication.
- **Socket.IO-client:** The Socket.IO client library used to connect to the Socket.IO server.

## Project Structure

```
/chat-mono-repo
|-- server      # NestJS backend code
|-- frontend     # Vue.js frontend code
|-- README.md    # Project documentation
```

## Getting Started

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/Giovani-f/chat-app-nestjs-vuejs.git
   ```

2. **Navigate to the Backend:**
   ```bash
   cd chat-mono-repo/server
   ```

3. **Install Dependencies:**
   ```bash
   npm install
   ```

4. **Start the Backend Server:**
   ```bash
   npm run start:dev
   ```

5. **Navigate to the Frontend:**
   ```bash
   cd ../frontend
   ```

6. **Install Dependencies:**
   ```bash
   npm install
   ```

7. **Start the Frontend Application:**
   ```bash
   npm run dev
   ```



## License

This project is licensed under the [MIT License](LICENSE).

---

Happy chatting! 🚀