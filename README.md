# 🌐 Borderless‑API

Borderless‑API is a backend service for a mobile‑first social platform with user authentication, blog post CRUD operations, comments, and real‑time chat via WebSockets.  
Built with **Django**, **Django REST Framework**, and **Django Channels**, it provides both RESTful API endpoints and WebSocket integration for seamless communication.

---

# ✅ Setup Instructions

## 📋 Requirements
- [Python](https://www.python.org/) 3.8+
- [pip](https://pip.pypa.io/) (comes with Python)
- [virtualenv](https://virtualenv.pypa.io/) (optional but recommended)
- A database: defaults to SQLite (can use PostgreSQL with proper config)
- Redis (for channel layers, if scaling WebSockets)

## 🔧 Installation Steps

### 1. Clone this repository
```bash
git clone https://github.com/<your-username>/Borderless-api.git
cd Borderless-api

### 2. Create and activate virtual environment
