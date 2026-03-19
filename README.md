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

## How to Use

Once both the back-end and front-end servers are running, follow these steps to get started:

### Step 1 — Register a New Account

Open the app in your browser (`http://localhost:5173`). You will be redirected to the **Register** page. Fill in your name, email, and password, then click **Register** to create your account.

![Register](screenshoots/register.png)

### Step 2 — Log In

After registering, you will be taken to the **Login** page. Enter the email and password you just created and click **Login** to access the app.

![Login](screenshoots/login.png)

### Step 3 — Create Tags

Navigate to the **Tags** tab from the top navigation bar. Here you can create tags to categorize your tasks. Enter a tag name, pick a color, and click **Create**. Create as many tags as you need (e.g. *Work*, *Personal*, *Urgent*).

![Tags](screenshoots/tags.png)

### Step 4 — Create a Task

Go back to the **Dashboard** by clicking it in the navigation bar. Click the **Create Task** button to open the task creation form. Fill in the task details:

- **Title** — A short name for the task.
- **Description** — Optional details about the task.
- **Start Date** — When the task begins.
- **Due Date** — The deadline for the task.
- **Tag** — Select one of the tags you created in the previous step to assign it to the task.

Click **Create** to save the task. It will appear on your dashboard.

![Create Task](screenshoots/create%20task.png)

### Step 5 — View Tasks on the Dashboard

The **Dashboard** shows all your tasks as cards, each displaying the title, dates, and the assigned tag with its color. You can quickly see what needs to be done at a glance.

![Dashboard](screenshoots/dashboard.png)

### Step 6 — View Tasks on the Calendar

Switch to the **Calendar** view from the navigation bar. Your tasks will be displayed on the calendar based on their start and due dates. You can toggle between **Month**, **Week**, **Day**, and **Agenda** views to plan your schedule.

![Calendar](screenshoots/calendar.png)

### Step 7 — Delete a Task

To delete a task, click on the task card on the Dashboard to open its details. Click the **Delete** button and confirm the deletion in the confirmation dialog. The task will be removed from both the dashboard and the calendar.

---

## Installing the PWA

TaskFlow is a Progressive Web App and can be installed on your device for a native-like experience.

1. Open the app in **Google Chrome** (or any Chromium-based browser such as Edge).
2. Look for the **Install** button (amber-colored) in the top-right corner of the navigation bar.
3. Click **Install** — the browser will show a native install dialog.
4. Confirm the installation. TaskFlow will now appear as a standalone app on your desktop or home screen.

> **Note:** The Install button only appears when the browser's install criteria are met (served over HTTPS or localhost, valid manifest, and active service worker). If you don't see it, make sure you're running the production build or have `devOptions` enabled in the Vite PWA config.

---

## Testing Offline Access

The app caches API data and static assets via a Workbox service worker, so previously loaded content remains available without a network connection.

### How to test

1. **Load the app normally** — Open TaskFlow in your browser and navigate through the Dashboard, Calendar, and Tags pages so the service worker caches the API responses and assets.

2. **Go offline** — Use one of these methods:
   - **Browser DevTools:** Open DevTools → **Network** tab → check the **Offline** checkbox.
   - **System:** Disconnect from Wi-Fi or unplug Ethernet.

3. **Verify offline behavior:**
   - Refresh the page — the app shell should load instantly from cache.
   - The **Dashboard** and **Calendar** will display your previously loaded tasks and tags from cached API data.
   - An **offline banner** will appear at the top of the page indicating you are working without a connection.
   - Navigation between cached pages (Dashboard, Calendar, Tags) continues to work.

4. **Go back online** — Uncheck the Offline checkbox in DevTools (or reconnect your network). The offline banner will disappear, and the app will resume fetching fresh data from the server.

> **Limitations while offline:** Create, update, and delete operations require a network connection and will fail gracefully when offline. Only previously cached data is available for viewing.

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

