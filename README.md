# TaskFlow — Task Manager

A full-stack task management application with calendar views, color-coded tags, and offline support via PWA.

---

## Screenshots

### Dashboard

![Dashboard](screenshoots/dashboard.png)

### Lighthouse Score

![Lighthouse Score](screenshoots/lighthouse%20score.png)

---

## Overview

| Part       | Stack                                           | Details                          |
| ---------- | ----------------------------------------------- | -------------------------------- |
| **Front-end** | React 19 · TypeScript · Tailwind CSS 4 · Vite 8 | SPA + PWA with offline caching  |
| **Back-end**  | Express 5 · TypeScript · Prisma 7 · PostgreSQL   | REST API with JWT authentication |

---

## Repository Structure

```
task-manager/
├── back-end/          # Express API server
│   ├── prisma/        #   Database schema & migrations
│   └── src/           #   Routes, controllers, middleware
├── front-end/         # React SPA (Vite)
│   ├── public/        #   Static / PWA assets
│   └── src/           #   Pages, components, hooks, context
└── README.md          # ← You are here
```

See the individual READMEs for detailed docs:
- [back-end/README.md](back-end/README.md)
- [front-end/README.md](front-end/README.md)

---

## Features

- **Task CRUD** — Create, view, update, and delete tasks with start / due dates.
- **Calendar View** — Visualize tasks on a month / week / day / agenda calendar (react-big-calendar).
- **Color-coded Tags** — Organize tasks with user-defined tags and colors.
- **JWT Authentication** — Secure register / login flow with token-based auth.
- **PWA & Offline** — Installable app with Workbox service worker; works offline with cached API data.
- **Code-splitting** — Lazy-loaded pages and components for fast initial load.
- **Responsive UI** — Mobile-first design with Tailwind CSS.

---

## Prerequisites

- **Node.js** ≥ 18
- **PostgreSQL** instance (local or hosted)

---

## Quick Start

### 1. Clone the repository

```bash
git clone <repo-url>
cd task-manager
```

### 2. Set up the back-end

```bash
cd back-end
npm install
```

Create a `.env` file:

```env
DATABASE_URL="postgresql://USER:PASSWORD@HOST:PORT/DATABASE"
JWT_SECRET="your-secret-key"
```

Run migrations and start the server:

```bash
npx prisma migrate deploy
npx prisma generate
npx prisma migrate dev --name init #to sync local db
npm run dev          # → http://localhost:5000
```

### 3. Set up the front-end

```bash
cd ../front-end
npm install
```

Create a `.env` file (or copy `.env.example`):

```env
VITE_API_URL=http://localhost:5000/api
```

Start the dev server:

```bash
npm run dev          # → http://localhost:5173
```

---

## Available Scripts

### Back-end (`back-end/`)

| Command       | Description                          |
| ------------- | ------------------------------------ |
| `npm run dev` | Start with hot-reload (ts-node-dev)  |

### Front-end (`front-end/`)

| Command           | Description                              |
| ----------------- | ---------------------------------------- |
| `npm run dev`     | Start Vite dev server with HMR           |
| `npm run build`   | Type-check + production build            |
| `npm run preview` | Serve the production build locally       |


---

## API Endpoints

All routes are prefixed with `/api`. Protected routes require a `Bearer <token>` header.

| Method | Endpoint          | Auth | Description           |
| ------ | ----------------- | ---- | --------------------- |
| POST   | `/api/register`   | —    | Create account        |
| POST   | `/api/login`      | —    | Login & get JWT       |
| POST   | `/api/tasks`      | ✔    | Create task           |
| GET    | `/api/tasks`      | ✔    | List user tasks       |
| PUT    | `/api/tasks/:id`  | ✔    | Update task           |
| DELETE | `/api/tasks/:id`  | ✔    | Delete task           |
| POST   | `/api/tags`       | ✔    | Create tag            |
| GET    | `/api/tags`       | ✔    | List user tags        |
| DELETE | `/api/tags/:id`   | ✔    | Delete tag            |

