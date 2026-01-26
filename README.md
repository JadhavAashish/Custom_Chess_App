# ♟️ Custom Real-Time Chess Game

A real-time multiplayer chess application built with **Node.js**, **Express**, **Socket.io**, and **chess.js**. 
The app supports **two players (White & Black)** and **spectators**, with live board synchronization and drag-and-drop moves.

---

## 🚀 Features

* Real-time multiplayer chess using WebSockets
* Automatic role assignment (White / Black / Spectator)
* Drag-and-drop piece movement
* Legal move validation via chess.js
* Board flip for Black player
* Live board updates for all connected clients
* Spectator mode with real-time view

---

## 🛠 Tech Stack

### Backend

* Node.js
* Express
* Socket.io
* chess.js
* EJS (templating engine)

### Frontend

* HTML, CSS, JavaScript
* Tailwind CSS
* Socket.io client
* chess.js

---

## 📂 Project Structure

```
chess-app/
│
├── server.js
├── package.json
├── public/
│   ├── js/
│   │   └── chessgame.js
│   └── css/
│
├── views/
│   └── index.ejs
│
└── README.md
```

---

## ⚙️ Backend Setup

### Server Initialization

* Import required modules:

  * `express`
  * `http`
  * `socket.io`
  * `chess.js`
* Create an Express app instance
* Initialize an HTTP server using Express
* Attach Socket.io to the HTTP server
* Create a Chess instance to manage the game state

### Game State Management

* Maintain a `players` object to track:

  * Socket IDs
  * Player roles (white / black)
* Track the current player's turn
* Use **FEN notation** to sync board state

### Express Configuration

* Use **EJS** as the templating engine
* Serve static files from the `public` directory
* Define root route (`/`) and render `index.ejs`
* Pass page title: **"Custom Chess Game"**

### Socket.io Logic

* Handle client connections
* Assign roles dynamically:

  * First player → White
  * Second player → Black
  * Additional clients → Spectators
* Emit events:

  * `playerRole`
  * `spectatorRole`
* Send initial board state on connection

### Move Handling

* Listen for `"move"` events from clients
* Validate:

  * Correct player turn
  * Legal moves using chess.js
* Update game state if valid
* Broadcast:

  * Move event
  * Updated board state to all clients
* Handle client disconnections and free player slots

---

## 🎨 Frontend Setup

### Drag and Drop

* Enable drag & drop for chess pieces
* Allow dragging only if:

  * Player owns the piece
  * It is the player’s turn
* Use event listeners:

  * `dragstart`
  * `dragend`
  * `dragover`
  * `drop`

### Rendering the Board

* Dynamically generate an 8×8 grid
* Alternate light and dark squares
* Render pieces using Unicode chess symbols
* Flip the board for Black player’s view

### Handling Moves

* Capture source and target squares
* Convert positions to algebraic notation
* Emit `"move"` event to the server

### Socket.io Event Handlers

* Listen for:

  * Player role assignment
  * Spectator role assignment
  * Board state updates
  * Opponent moves
* Update local game state and re-render the board

### Initial Rendering

* Render the board immediately on page load

---

## 📌 Future Improvements

* Move highlighting
* Check / checkmate indicators
* Game timers
* Player names and chat
* Game history (PGN export)
* Mobile responsiveness

---

### ✅ Suggested Commit Message

```
Initial commit: real-time chess app using Socket.io and chess.js
```
