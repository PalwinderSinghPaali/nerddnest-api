# NerddNest API

Backend API for the **NerddNest social networking platform**, providing the server-side foundation for authentication, user profiles, social connections, posts, feeds, stories, groups, **real-time messaging, one-to-one chats, and group conversations**.

The API combines traditional REST APIs with **Socket.IO-powered real-time communication** to support both standard social-platform operations and interactive messaging experiences.

## 🚀 Overview

NerddNest is a social networking platform focused on connecting users through profiles, content, communities, social relationships, and real-time conversations.

The backend acts as the core application layer between the frontend, database, and real-time communication layer.

```text
                         NerddNest Platform
                                │
                 ┌──────────────┴──────────────┐
                 │                             │
                 ▼                             ▼
        Next.js / React Frontend         Real-Time Clients
                 │                             │
                 │ REST API                    │ Socket.IO
                 │                             │
                 ▼                             ▼
        ┌────────────────────────────────────────────┐
        │              NerddNest API                 │
        │                                             │
        │ Authentication                              │
        │ User Management                             │
        │ Social Features                             │
        │ Posts & Feeds                               │
        │ Stories & Groups                            │
        │ Chat & Messaging                            │
        │ Business Logic                              │
        │ Validation                                  │
        └───────────────────┬────────────────────────┘
                            │
                 ┌──────────┴──────────┐
                 │                     │
                 ▼                     ▼
             Database             Socket.IO
                                     │
                                     ▼
                              Connected Clients
```

## ✨ Core Features

### 👤 User & Authentication

* User registration and authentication
* Access-token based authentication
* Protected API resources
* User profiles
* User discovery
* User relationships

### 👥 Social Networking

* Friend/connection management
* Friend suggestions
* Social feeds
* Posts
* Stories
* Groups and communities
* Social interactions

### 💬 Real-Time Chat

A major part of the backend is the **real-time messaging system built with Socket.IO**.

The chat architecture supports:

* One-to-one conversations
* Group conversations
* Real-time message delivery
* Socket-based communication
* Message persistence
* Conversation management
* Multiple users connected to the same conversation
* Group chat communication

```text
User A
  │
  │ Socket.IO
  ▼
┌───────────────────┐
│   Socket.IO API   │
│                   │
│ Connection        │
│ Authentication    │
│ Events            │
│ Message Routing   │
└─────────┬─────────┘
          │
          ├──────────────► User B
          │
          ├──────────────► User C
          │
          └──────────────► Group Members
```

## 🔌 Socket.IO Architecture

REST APIs handle standard application operations, while Socket.IO handles events that need to be delivered in real time.

```text
                 Client
                   │
          ┌────────┴────────┐
          │                 │
       REST API          Socket.IO
          │                 │
          ▼                 ▼
    Request/Response    Real-Time Events
          │                 │
          └────────┬────────┘
                   ▼
              Backend Logic
                   │
                   ▼
                Database
```

This hybrid architecture allows the application to use the appropriate communication mechanism for each feature.

### Real-Time Event Flow

```text
Sender
  │
  ▼
Socket.IO Event
  │
  ▼
Backend
  │
  ├── Validate User
  ├── Validate Conversation
  ├── Process Message
  └── Persist Message
          │
          ▼
    Broadcast Event
          │
     ┌────┴────┐
     ▼         ▼
 Recipient   Group Members
```

## 💬 One-to-One Chat

The API supports direct conversations between users.

```text
┌──────────┐                     ┌──────────┐
│  User A  │                     │  User B  │
└────┬─────┘                     └────▲─────┘
     │                                │
     │         Socket.IO              │
     └─────────────┬──────────────────┘
                   │
                   ▼
             Chat Service
                   │
                   ▼
                Database
```

Messages can be transmitted through Socket.IO while being persisted on the backend for conversation history.

## 👨‍👩‍👧‍👦 Group Chat

The chat system also supports **group conversations**, allowing multiple users to participate in the same real-time conversation.

```text
                   Group Chat
                       │
            ┌──────────┼──────────┐
            │          │          │
            ▼          ▼          ▼
         User A      User B     User C
            │          │          │
            └──────────┼──────────┘
                       │
                       ▼
                  Socket.IO
                       │
                       ▼
                 Chat Service
                       │
                       ▼
                    Database
```

Group conversations require additional backend handling around:

* Group membership
* Conversation participants
* Message broadcasting
* Message persistence
* User authorization
* Conversation access

## 📨 Message Lifecycle

The messaging architecture follows a real-time event + persistence model:

```text
User Sends Message
        │
        ▼
   Socket.IO Event
        │
        ▼
   Authentication
        │
        ▼
 Authorization Check
        │
        ▼
 Message Validation
        │
        ▼
   Save Message
        │
        ▼
 Broadcast Event
        │
        ├──────────► Recipient
        │
        └──────────► Group Members
```

This approach provides both:

**Real-time delivery** for active users

and

**Persistent history** for users returning to the conversation later.

## 🟢 Real-Time Communication

Socket.IO provides the foundation for interactive communication between connected clients.

This architecture can support events such as:

* New messages
* Group messages
* Conversation updates
* User connection events
* Real-time UI updates
* Other social events

The socket layer is kept separate from standard REST request/response operations.

## 📝 Posts & Feed

The API provides the backend layer for social content and feed functionality.

```text
Create Post
    │
    ▼
API Request
    │
    ▼
Validation
    │
    ▼
Business Logic
    │
    ▼
Database
    │
    ▼
Feed Retrieval
    │
    ▼
Frontend
```

The server remains responsible for data validation, authorization, business rules, and persistence.

## 📸 Stories & Media

The platform supports story-based social content and media-related functionality.

The backend handles the server-side operations required to create, retrieve, and manage social media content.

```text
Media / Story
      │
      ▼
     API
      │
      ├── Authentication
      ├── Validation
      ├── Authorization
      └── Persistence
             │
             ▼
          Database
```

## 👨‍👩‍👧‍👦 Groups & Communities

Groups provide a community-oriented layer within the social platform.

The backend manages the relationships between users and groups and provides the foundation for group-based functionality.

Groups can also serve as the foundation for **group conversations and real-time group chat**.

```text
Group
 │
 ├── Members
 ├── Posts
 ├── Community Data
 └── Group Chat
        │
        ▼
    Socket.IO
```

## 🔐 Authentication & Authorization

Authentication is handled server-side and provides the foundation for protected API and socket functionality.

```text
Login / Registration
        │
        ▼
   Authentication
        │
        ▼
    Access Token
        │
        ├──────────────► REST API
        │
        └──────────────► Socket.IO
                              │
                              ▼
                         Authorized User
```

Authorization is particularly important for chat functionality because users must only be able to access conversations they are permitted to participate in.

## 🧠 Backend Architecture

The backend separates application responsibilities across different layers:

```text
Request / Socket Event
        │
        ▼
Controller / Socket Handler
        │
        ▼
Authentication
        │
        ▼
Validation
        │
        ▼
Business Logic
        │
        ▼
Service / Data Layer
        │
        ▼
Database
        │
        ▼
Response / Socket Event
```

This separation makes it easier to maintain both REST APIs and real-time communication as the platform grows.

## 🗄️ Database Layer

The database stores the persistent state required by the social platform.

Conceptually, the data model contains relationships such as:

```text
Users
 │
 ├── Connections
 │
 ├── Posts
 │
 ├── Stories
 │
 ├── Groups
 │
 └── Conversations
        │
        ├── Participants
        │
        └── Messages
```

The relationship between users, conversations, and messages provides the foundation for both direct messaging and group chats.

## 🛡️ API & Socket Security

Security is enforced on the backend rather than relying solely on frontend validation.

Important areas include:

* Authentication
* Authorization
* Request validation
* Socket authentication
* Conversation access control
* Group membership validation
* Input validation
* Protected resources
* Centralized error handling

This is particularly important for real-time systems where a connected client must not automatically be trusted to access arbitrary conversations or send messages on behalf of another user.

## ⚠️ Error Handling

The backend uses centralized error handling to provide consistent responses for API operations.

```text
Request / Socket Event
        │
        ▼
Application Logic
        │
   ┌────┴────┐
   │         │
Success     Error
   │         │
   ▼         ▼
Response   Error Handler
             │
             ▼
       Standardized Error
```

## 🛠️ Technology Stack

### Backend

* Node.js
* REST APIs
* JavaScript / TypeScript

### Real-Time

* **Socket.IO**
* WebSocket-based communication
* Real-time event handling

### Database

* Relational database
* ORM / database abstraction

### Application Architecture

* Authentication
* Authorization
* API validation
* Business logic
* Modular services
* Social graph management
* Conversation management
* Message persistence
* Group chat

## 🔗 Frontend Integration

The API works with the **NerddNest frontend** through two primary communication channels:

```text
              NerddNest Frontend
                     │
          ┌──────────┴──────────┐
          │                     │
          ▼                     ▼
       REST API             Socket.IO
          │                     │
          └──────────┬──────────┘
                     ▼
               NerddNest API
                     │
                     ▼
                  Database
```

REST is used for standard application operations, while Socket.IO provides real-time communication for chat and other interactive events.

## 🚀 Getting Started

### Prerequisites

Make sure you have the required Node.js runtime and database environment configured.

### Clone

```bash
git clone https://github.com/PalwinderSinghPaali/nerddnest-api.git

cd nerddnest-api
```

### Install Dependencies

```bash
npm install
```

### Environment Variables

Create a local environment configuration file with the required application and database settings.

Example:

```env
DATABASE_URL=your_database_url
JWT_SECRET=your_jwt_secret
PORT=5000
```

> Use the actual environment variables required by the application. Never commit secrets or production credentials to the repository.

### Start Development Server

```bash
npm run dev
```

## 📌 Project Status

NerddNest API represents the backend of a feature-rich social networking platform combining **REST APIs with real-time Socket.IO communication**.

The project demonstrates practical backend engineering across:

* REST API development
* Authentication & authorization
* User management
* Social connections
* Posts and feeds
* Stories
* Groups and communities
* One-to-one messaging
* Group chat
* Real-time communication
* Socket.IO event handling
* Conversation management
* Message persistence
* Database relationships
* Business logic
* Frontend/backend integration

This makes the project a strong example of building a **full-stack social platform with both traditional API architecture and real-time communication**.

---

**Built by [Palwinder Singh](https://github.com/PalwinderSinghPaali)**
