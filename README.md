 Project Name: TaskFlow – Real-Time Task Management App (PERN Stack)

 Overview

TaskFlow is a real-time task management application built using the **PERN stack**:

* **PostgreSQL** for database
* **Express.js** for backend API
* **React** (with Vite) for the frontend
* **Node.js** as the runtime
* Plus **BullMQ + Redis** for background job queues
* **Mailhog** for mock email notifications
* **Docker Compose** for running all services in one go

The app lets users:

* Create tasks with different priorities
* Attach and preview image uploads
* Automatically process tasks in the background
* Get notified via email when statuses change
* View real-time updates on task progress

---

### 🛠️ Tech Stack

| Layer      | Tools Used                   |
| ---------- | ---------------------------- |
| Frontend   | React 18, Vite, Tailwind CSS |
| Backend    | Node.js, Express.js          |
| Database   | PostgreSQL 14                |
| Queues     | BullMQ + Redis 7             |
| Emails     | Nodemailer + Mailhog         |
| DevOps     | Docker Compose               |
| Image Proc | Multer + Sharp (thumbnails)  |

---

### 📂 Project Structure

```
.
├── docker-compose.yml
├── server/                 # Express API, queues, DB
│   ├── routes/             # API routes
│   ├── workers/            # BullMQ processors
│   ├── utils/              # Mailer, storage utils
│   └── index.js            # App entry
├── client/                 # React frontend
│   └── src/
│       ├── pages/
│       ├── components/
│       └── App.jsx
├── .env                    # Secrets
└── README.md

### 🔧 How It Works (Simple Terms)

1. **Create Task** via the React UI.
2. Task is saved to **PostgreSQL**, and 3 jobs are queued:

   * Task Processor
   * Image Uploader
   * Email Dispatcher
3. **Workers** pick up the jobs and:

   * Simulate a 5–10 second task
   * Resize the image
   * Send notification email
4. **React frontend** listens for updates via Socket.IO or polling and updates in real time.

### 🧬 Architecture Diagram

#### Visual (for README)

```
Frontend (React)
   │
   ▼
Express API (Node.js)
   │       ┌────────────┐
   ├──────▶│ PostgreSQL │
   │       └────────────┘
   │
   ├────▶ BullMQ Queue ───────────────┐
   │                                  ▼
   │         ┌────────────┐   ┌─────────────────┐
   ├────────▶│ imageUpload│ → │ Sharp (Resize)  │
   │         ├────────────┤   └─────────────────┘
   │         │ taskWorker │ → Update Status
   │         ├────────────┤
   │         │ emailQueue │ → Nodemailer → Mailhog
   │         └────────────┘
```

---

### 📬 API Examples (Curl)

```bash
# Create a new task
curl -X POST http://localhost:3000/api/tasks \
  -H "Content-Type: application/json" \
  -d '{ "title": "Design Homepage", "priority": "High" }'

# Get all tasks
curl http://localhost:3000/api/tasks

# Update task status manually
curl -X PATCH http://localhost:3000/api/tasks/<TASK_ID>/status \
  -H "Content-Type: application/json" \
  -d '{ "status": "Completed" }'
```

---

### 🐳 Docker-Compose

This project includes a `docker-compose.yml` that runs:

* The Express API
* React frontend
* Redis server
* PostgreSQL DB
* Mailhog (email UI)

Just run:

```bash
docker-compose up --build

You're ready to hit send! 📬
