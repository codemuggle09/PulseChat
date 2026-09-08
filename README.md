# PulseChat

Real-time chat application built with Next.js and Express, using Apache Kafka for asynchronous message processing, Redis for session management and caching, and PostgreSQL for persistent storage.

## Architecture

```text
                    ┌────────────────┐
                    │  Next.js Client│
                    └───────┬────────┘
                            │
                            ▼
                    ┌────────────────┐
                    │  Express API   │
                    └───────┬────────┘
                            │
              ┌─────────────┼─────────────┐
              │             │             │
              ▼             ▼             ▼
         ┌─────────┐   ┌─────────┐   ┌────────────┐
         │  Redis  │   │  Kafka  │   │ PostgreSQL │
         │ Sessions│   │ Messages│   │ Persistence│
         │  Cache  │   └────┬────┘   └────────────┘
         └─────────┘        │
                            ▼
                     ┌──────────────┐
                     │Kafka Consumer│
                     └──────┬───────┘
                            │
                            ▼
                     ┌────────────┐
                     │ PostgreSQL │
                     └────────────┘
```

## Features

- Google OAuth authentication
- Real-time messaging with Socket.IO
- Asynchronous message processing with Apache Kafka
- Redis-based session management and caching
- PostgreSQL persistence through Prisma
- Next.js frontend with TypeScript
- Express.js backend
- Tailwind CSS interface

## Tech Stack

### Frontend

- Next.js 14
- React
- TypeScript
- Tailwind CSS
- Socket.IO Client
- NextAuth
- Radix UI

### Backend

- Node.js
- Express.js
- Socket.IO
- Node-rdkafka
- Redis
- Prisma
- PostgreSQL

### Infrastructure

- Apache Kafka
- Redis
- Docker

## Project Structure

```text
PulseChat/
├── client/
│   ├── src/
│   │   ├── app/
│   │   ├── components/
│   │   ├── lib/
│   │   └── validations/
│   └── public/
│
├── server/
│   ├── src/
│   │   ├── config/
│   │   ├── controllers/
│   │   ├── middleware/
│   │   └── routes/
│   └── prisma/
│
└── docker/
```

## Setup

### Prerequisites

- Node.js 18+
- pnpm
- PostgreSQL
- Redis
- Apache Kafka

### Clone the Repository

```bash
git clone https://github.com/codemuggle09/PulseChat.git
cd PulseChat
```

### Install Dependencies

Install server dependencies:

```bash
cd server
pnpm install
```

Install client dependencies:

```bash
cd ../client
pnpm install
```

### Environment Variables

Create the following files:

```text
server/.env
client/.env.local
```

Configure the required database, Kafka, Redis, backend, and Google OAuth credentials according to your environment.

### Database Setup

```bash
cd server
npx prisma migrate dev
```

### Run the Application

Start the backend:

```bash
cd server
pnpm dev
```

In a separate terminal, start the frontend:

```bash
cd client
pnpm dev
```

The application will be available at:

```text
http://localhost:3000
```

## Message Flow

```text
Client
  │
  ▼
Next.js
  │
  ▼
Express API
  │
  ├──────────────► Redis
  │
  └──────────────► Kafka
                       │
                       ▼
                 Kafka Consumer
                       │
                       ▼
                  PostgreSQL
```

## License

MIT
