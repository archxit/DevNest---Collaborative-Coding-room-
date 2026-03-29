# ⚡ DevNest Backend — Real-Time Collaborative Engine

> Multi-user code collaboration backend with live sync, role control, and persistent versioning.

---

## 🧠 What This Actually Does

DevNest backend is not just CRUD APIs — it’s a **state synchronization engine** for collaborative coding.

* Maintains shared code state across multiple clients
* Handles real-time updates via WebSockets
* Enforces access control (Owner / Editor / Viewer)
* Persists code + version history in MongoDB

---

## ⚙️ System Architecture

```id="l4t8xk"
Client (React + Monaco)
        ↓
REST API (Auth, Rooms, Versions)
        ↓
Socket.io Server (Real-time sync layer)
        ↓
MongoDB (Users, Rooms, Code Snapshots)
```

### Key Separation:

* **REST → persistence**
* **WebSocket → real-time updates**

---

## 🔥 Core Capabilities

### 🔐 Authentication

* JWT-based auth
* Middleware-protected routes
* Stateless session handling

---

### 🏠 Room System

* Create / Join rooms
* Role-based permissions:

  * Owner → full control
  * Editor → edit code
  * Viewer → read-only

---

### ⚡ Real-Time Sync (Socket.io)

```id="4f8lqv"
User types →
emit("code-change") →
server broadcasts →
all clients update instantly
```

* Room-based socket channels
* Low-latency broadcasting
* Handles multi-user editing

---

### 💾 Code Persistence

* Autosave via REST (`PATCH /code`)
* Version snapshots stored separately
* Time-based history tracking

---

### 🧠 Version History

* Snapshot-based system
* Restore previous states
* Tracks user + timestamp

---

## 📡 API Surface

### Auth

* `POST /api/auth/register`
* `POST /api/auth/login`

---

### Rooms

* `POST /api/rooms/create`
* `POST /api/rooms/join`
* `GET /api/rooms/my-rooms`
* `GET /api/rooms/:roomId`
* `PATCH /api/rooms/:roomId/code`

---

### Versions

* `POST /api/versions/save`
* `GET /api/versions/:roomId`

---

## 🔌 Socket Events (REAL CORE)

### Client → Server

```id="n8w8rx"
join-room        { roomId }
code-change      { roomId, code }
cursor-move      { roomId, position }
```

---

### Server → Client

```id="wq7pxz"
code-update      { code }
user-joined      { user }
cursor-update    { userId, position }
```

---

## 📂 Project Structure

```id="4jocqk"
devnest-backend/
├── server.js
├── config/db.js
├── models/
├── routes/
├── middleware/
```

---

## 🚀 Setup

```id="rkt3xf"
npm install
copy .env.example .env
npm run dev
```

---

## 🌍 Environment Variables

```id="j9u6h7"
PORT=5000
MONGO_URI=mongodb://127.0.0.1:27017/devnest
JWT_SECRET=your_secret
```

---

## 🧪 Health Check

```id="5pcr0y"
GET /api/health
```

---

## ⚠️ Design Trade-offs

* Uses **full document sync** (not OT/CRDT yet)
* Last-write-wins strategy
* No offline sync

---

## 🚀 What Makes This Strong

* Separates real-time + persistence layers cleanly
* Uses room-based socket architecture
* Demonstrates scalable system thinking
* Not just CRUD — actual collaborative system

---

## 🔮 Next Iteration

* Operational Transform / CRDT
* Differential updates instead of full state
* Rate limiting + throttling
* Horizontal scaling with Redis adapter

---

## 👨‍💻 Author

Nehal Verma
B.Tech CCE — Backend + Systems Engineering Focus

---
