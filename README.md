# 📍 Where is My Faculty?

A university web application that lets students find faculty availability in real-time, discover campus clubs & events, and manage their academic schedule — all in one place.

**Built by:** Shansit Suman & Shreya Goyal

**Live App:** [where-is-my-faculty.netlify.app](https://where-is-my-faculty.netlify.app) *(update after deployment)*

---

## 🧩 What It Does

| Role | Capabilities |
|------|-------------|
| **Student** | Register/login, search faculty by name/slot, view cabin location, browse clubs & events |
| **Faculty** | Register/login (OTP verified + admin approved), set cabin number & free time slots, update availability |
| **Club** | Register/login (admin approved), post events with poster images and OD details |
| **Admin** | Approve/reject pending faculty and club registrations |

---

## 🏗️ Architecture

```mermaid
graph TD
    subgraph Frontend ["🌐 Frontend (Netlify — Static HTML)"]
        A[index.html] --> B[student-login / register]
        A --> C[faculty-login / register]
        A --> D[club-login / register]
        B --> E[student-dashboard.html]
        C --> F[faculty-dashboard.html]
        D --> G[club-dashboard.html]
        H[admin-dashboard.html]
        I[ffcs-dashboard.html]
        J[config.js — API_URL]
    end

    subgraph Backend ["⚙️ Backend (Render — Node/Express)"]
        K[Express Server :5000]
        K --> L[/api/student]
        K --> M[/api/faculty]
        K --> N[/api/club]
        K --> O[/api/admin]
        K --> P[/uploads — static images]
    end

    subgraph DB ["🗄️ Database (MongoDB Atlas)"]
        Q[(Students)]
        R[(Faculties)]
        S[(Clubs + Events)]
    end

    subgraph Auth ["🔐 Auth Middleware"]
        T[auth.js — Student JWT]
        U[facultyAuth.js — Faculty JWT]
        V[clubAuth.js — Club JWT]
    end

    Frontend -->|HTTP fetch via API_URL| Backend
    L --> Q
    M --> R
    N --> S
    O --> R
    O --> S
    M --> U
    N --> V
    L --> T
```

---

## 🗂️ Project Structure

```
Where-is-My-Faculty/
├── backend/
│   ├── config/
│   │   └── db.js                  # MongoDB Atlas connection
│   ├── controllers/
│   │   ├── adminController.js
│   │   ├── clubController.js
│   │   ├── facultyController.js
│   │   └── studentController.js
│   ├── middleware/
│   │   ├── auth.js                # Student JWT
│   │   ├── clubAuth.js            # Club JWT
│   │   └── facultyAuth.js        # Faculty JWT
│   ├── models/
│   │   ├── Admin.js
│   │   ├── Club.js                # includes embedded Event schema
│   │   ├── Event.js
│   │   ├── Faculty.js
│   │   └── Student.js
│   ├── routes/
│   │   ├── admin.js
│   │   ├── club.js
│   │   ├── faculty.js
│   │   └── student.js
│   ├── uploads/                   # uploaded club event posters
│   ├── index.js
│   ├── server.js
│   └── package.json
│
├── frontend/
│   ├── public/
│   │   ├── index.html             # landing / home page
│   │   ├── student-login.html
│   │   ├── student-register.html
│   │   ├── student-dashboard.html
│   │   ├── faculty-login.html
│   │   ├── faculty-register.html
│   │   ├── faculty-dashboard.html
│   │   ├── club-login.html
│   │   ├── club-register.html
│   │   ├── club-dashboard.html
│   │   ├── admin-dashboard.html
│   │   ├── ffcs-dashboard.html
│   │   ├── js/
│   │   │   ├── config.js          # ← API_URL lives here
│   │   │   └── script.js
│   │   └── img/                   # static images
│   ├── css/style.css
│   ├── src/input.css
│   ├── tailwind.config.js
│   └── package.json
│
├── render.yaml                    # Render backend deploy config
├── netlify.toml                   # Netlify frontend deploy config
├── DEPLOY.md                      # Full deployment guide
└── README.md
```

---

## 🔌 API Reference

### Student — `/api/student`
| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| POST | `/register` | — | Register new student |
| POST | `/login` | — | Login, returns JWT |

### Faculty — `/api/faculty`
| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| POST | `/register` | — | Register (requires admin approval) |
| POST | `/login` | — | Login, returns JWT |
| GET | `/` | — | Get all approved faculties |
| GET | `/me` | Faculty JWT | Get own profile & slots |
| POST | `/setup` | Faculty JWT | First-time dashboard setup |
| PUT | `/update` | Faculty JWT | Update cabin/slots/note |

### Club — `/api/club`
| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| POST | `/register` | — | Register club (requires admin approval) |
| POST | `/login` | — | Login, returns JWT |
| GET | `/all` | — | Get all approved clubs |
| GET | `/events/:id` | — | Get events for a club |
| GET | `/me` | Club JWT | Get own club profile |
| POST | `/event` | Club JWT | Post new event with poster |
| GET | `/pending` | Admin | Get pending club approvals |
| PUT | `/approve/:id` | Admin | Approve a club |

### Admin — `/api/admin`
| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| GET | `/pending` | — | Get all pending faculty & clubs |
| PUT | `/approve/faculty/:id` | — | Approve a faculty |
| PUT | `/approve/club/:clubName` | — | Approve a club |

---

## 🗃️ Data Models

**Faculty**
```
name, mobile, email, facultyID, password
otpVerified, approved, cabin, freeSlots[], note
```

**Student**
```
name, regNo, password
```

**Club**
```
clubName, email, presidentName, password
otpVerified, approved, events[]
  └── event: name, date, poster, odProvided
```

---

## 🚀 Running Locally

### Prerequisites
- Node.js v18+
- MongoDB Atlas account (or local MongoDB)

### Backend
```bash
cd backend
npm install
# create a .env file with:
# PORT=5000
# MONGO_URI=your_mongodb_connection_string
# JWT_SECRET=your_secret_key
node index.js
# ✅ Server running on port 5000
# ✅ MongoDB Connected
```

### Frontend
```bash
cd frontend
npm install
npm run dev
# Open http://localhost:5173
```

---

## ☁️ Deployment (Free)

| Service | Platform | URL |
|---------|----------|-----|
| Backend | Render.com | `https://where-is-my-faculty.onrender.com` |
| Frontend | Netlify | `https://where-is-my-faculty.netlify.app` |
| Database | MongoDB Atlas | Free M0 cluster |

See [DEPLOY.md](./DEPLOY.md) for full step-by-step instructions.

> **Note:** Render free tier sleeps after 15 min of inactivity. First request after idle takes ~30 seconds to wake up.

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | HTML, Tailwind CSS, Vanilla JS |
| Backend | Node.js, Express.js |
| Database | MongoDB Atlas + Mongoose |
| Auth | JWT (jsonwebtoken) + bcryptjs |
| File Upload | Multer |
| Email/OTP | Nodemailer |
| Deploy (BE) | Render |
| Deploy (FE) | Netlify |
