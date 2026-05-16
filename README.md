# AquaMonitor

AquaMonitor is a full‑stack water monitoring platform for tracking groundwater and surface‑water stations. It provides an operational dashboard, interactive map, analytics, alerts, and reporting across a network of monitoring stations backed by a MySQL database and a secure REST API.

## ✨ Key Features

- **Operational dashboard** with KPIs for stations, alerts, and recharge estimates.
- **Interactive map (Leaflet + OpenStreetMap)** with station markers, status colors, and popups.
- **Water level analytics** with trends, seasonal comparisons, and recharge estimation.
- **Alerts management** with acknowledgements and severity levels.
- **Role‑based access** (admin/operator/viewer) using JWT authentication.
- **Report generation** for data summaries and export workflows.

## 🧱 Tech Stack

**Frontend**
- React 18 + TypeScript + Vite
- Tailwind CSS for UI
- Recharts for charts
- Leaflet / React‑Leaflet for maps
- Axios for API calls

**Backend**
- Node.js + Express
- MySQL (mysql2) with connection pooling
- JWT auth, bcrypt password hashing
- Joi validation, Helmet, CORS, rate limiting

## 📁 Project Structure

```
AquaMonitor/
├── backend/                 # Express API + MySQL integration
│   ├── config/              # DB connection
│   ├── routes/              # Auth, stations, readings, alerts, dashboard
│   ├── scripts/             # DB initialization
│   └── server.js            # API entrypoint
├── src/                     # React app
│   ├── pages/               # Dashboard, Map, Reports, etc.
│   ├── components/          # UI components
│   └── services/            # API client
├── MYSQL_SETUP.md           # Detailed MySQL setup guide
├── README_MYSQL_INTEGRATION.md
└── README.md
```

## ✅ Prerequisites

- **Node.js 18+** and npm
- **MySQL 8+** running locally or in Docker

## 🚀 Getting Started

### 1) Install Dependencies

```bash
npm run setup
```

This installs root dependencies and backend dependencies.

### 2) Configure Environment Variables

**Backend:**

```bash
cp backend/.env.example backend/.env
```

Update values in `backend/.env`:

- `DB_HOST`, `DB_PORT`, `DB_USER`, `DB_PASSWORD`, `DB_NAME`
- `JWT_SECRET`, `JWT_EXPIRES_IN`
- `PORT` (default `3001`)
- `FRONTEND_URL` (default `http://localhost:5173`)

**Frontend (optional):** create `.env` in the root:

```env
VITE_API_URL=http://localhost:3001/api
```

### 3) Initialize the Database

```bash
npm run backend:init-db
```

This creates the required tables and inserts sample data.

### 4) Run the App

**Run both frontend + backend together:**

```bash
npm run full:dev
```

**Or run separately:**

```bash
# Terminal 1
npm run backend:dev

# Terminal 2
npm run dev
```

### 5) Access the App

- Frontend: http://localhost:5173
- Backend API: http://localhost:3001
- Health Check: http://localhost:3001/api/health

## 🧪 Available Scripts

| Script | Description |
| --- | --- |
| `npm run dev` | Start frontend dev server |
| `npm run build` | Build frontend for production |
| `npm run lint` | Run ESLint |
| `npm run preview` | Preview production build |
| `npm run backend:dev` | Start backend with nodemon |
| `npm run backend:start` | Start backend (node) |
| `npm run backend:init-db` | Initialize MySQL tables + sample data |
| `npm run full:dev` | Run backend and frontend together |
| `npm run setup` | Install root + backend dependencies |

## 🔌 API Overview

**Authentication**
- `POST /api/auth/register`
- `POST /api/auth/login`
- `GET /api/auth/profile`

**Stations**
- `GET /api/stations`
- `GET /api/stations/:id`
- `POST /api/stations`
- `PUT /api/stations/:id`
- `DELETE /api/stations/:id`

**Readings**
- `GET /api/readings/station/:id`
- `GET /api/readings/latest`
- `POST /api/readings`
- `GET /api/readings/analytics/:id`

**Alerts**
- `GET /api/alerts`
- `POST /api/alerts`
- `PATCH /api/alerts/:id/acknowledge`
- `GET /api/alerts/stats`

**Dashboard**
- `GET /api/dashboard/stats`
- `GET /api/dashboard/trends`
- `GET /api/dashboard/alerts`
- `GET /api/dashboard/recharge`

Full details live in `MYSQL_SETUP.md`.

## 🗄️ Database Notes

The backend uses a MySQL schema with core tables for **users**, **stations**, **readings**, and **alerts**. Use the `backend/scripts/initDatabase.js` script via `npm run backend:init-db` to create tables and seed sample data.

## 🧰 Troubleshooting

- **Database connection fails**: verify MySQL is running and credentials in `backend/.env` are correct.
- **CORS issues**: ensure `FRONTEND_URL` in `backend/.env` matches your frontend URL.
- **Port in use**: change `PORT` in `backend/.env` or stop the running process.

## 📚 Additional Documentation

- `MYSQL_SETUP.md` — complete MySQL setup and troubleshooting
- `README_MYSQL_INTEGRATION.md` — integration overview
- `MAP_IMPLEMENTATION_SUCCESS.md` — map feature summary

## 🤝 Contributing

1. Create a feature branch
2. Make changes with clear commit messages
3. Open a pull request with a summary and testing notes

---

AquaMonitor helps teams track critical water resources with data‑driven insights and geospatial visibility.
