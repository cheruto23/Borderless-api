# 🌐 Borderless‑API

Borderless‑API is a backend service for a mobile‑first social platform with user authentication, blog post CRUD operations, comments, and real‑time chat via WebSockets.  
Built with **Django**, **Django REST Framework**, and **Django Channels**, it provides both RESTful API endpoints and WebSocket integration for seamless communication.

---

## 📑 Table of Contents
- [✅ Setup Instructions](#-setup-instructions)
  - [📋 Requirements](#-requirements)
  - [🔧 Installation Steps](#-installation-steps)
  - [🗂 Folder Structure](#-folder-structure)
- [✅ How to Run the Project](#-how-to-run-the-project)
- [✅ Key Functions / Components](#-key-functions--components)
- [✅ Troubleshooting Tips](#-troubleshooting-tips)
- [✅ Contributing](#-contributing)
- [✅ License](#-license)

---

# ✅ Setup Instructions

## 📋 Requirements
- [Python](https://www.python.org/) 3.8+
- [pip](https://pip.pypa.io/) (comes with Python)
- [virtualenv](https://virtualenv.pypa.io/) (optional but recommended)
- A database: defaults to SQLite (can use PostgreSQL with proper config)
- Redis (for channel layers, if scaling WebSockets)

## 🔧 Installation Steps

### 1️⃣ Clone this repository
```bash
git clone https://github.com/cheruto23/Borderless-api.git
cd Borderless-api
2️⃣ Create and activate virtual environment
bash
Copy
Edit
python -m venv venv
source venv/bin/activate    # On Linux/Mac
venv\Scripts\activate       # On Windows
3️⃣ Install dependencies
bash
Copy
Edit
pip install -r requirements.txt
4️⃣ Configure environment variables
Copy .env.example to .env and set your secret keys, DB connection (if not using SQLite), and Redis URL if needed.

Example:

dotenv
Copy
Edit
DJANGO_SECRET_KEY=your_secret_key_here
DB_NAME=borderless
DB_USER=user
DB_PASS=password
DB_HOST=localhost
DB_PORT=5432
REDIS_URL=redis://127.0.0.1:6379
5️⃣ Apply migrations
bash
Copy
Edit
python manage.py migrate
6️⃣ Create a superuser (optional, for admin access)
bash
Copy
Edit
python manage.py createsuperuser
🗂 Folder Structure
plaintext
Copy
Edit
Borderless-api/
├── borderless/           # Django project folder
│   ├── asgi.py           # ASGI entry point (for WebSockets)
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── users/                # User auth app
├── posts/                # Blog posts & comments app
├── chat/                 # WebSocket chat app
├── requirements.txt
├── manage.py
└── README.md
✅ How to Run the Project
🔷 Run development server
bash
Copy
Edit
python manage.py runserver
✅ API available at: http://127.0.0.1:8000/api/
✅ Admin panel at: http://127.0.0.1:8000/admin/

🔷 Start Channels worker for WebSockets
For real‑time chat, also run:

bash
Copy
Edit
daphne borderless.asgi:application
🔷 Sample API output
json
Copy
Edit
{
  "token": "eyJ0eXAiOiJKV1QiLCJhbGci...",
  "user": {
    "id": 1,
    "username": "john_doe"
  }
}
✅ WebSocket endpoint:
ws://127.0.0.1:8000/ws/chat/<room_name>/

✅ Key Functions / Components
1️⃣ JWT Authentication Endpoint
File: users/views.py → TokenObtainPairView

Role: Issues JWT tokens to authenticated users.

Inputs: Request body (JSON):

json
Copy
Edit
{ "username": "john_doe", "password": "password123" }
Output: JWT access and refresh tokens + user info.

Edge cases:

Wrong credentials → HTTP 401 error

Inactive user → HTTP 403 error

2️⃣ Chat Consumer
File: chat/consumers.py → ChatConsumer

Role: Handles WebSocket connections for chat rooms.

Inputs: WebSocket events: connect, receive message, disconnect

Output: Broadcasts received messages to all users in the same room.

Edge cases:

User leaves → room is cleaned up

Message too large → connection closed

✅ Troubleshooting Tips
✅ Issue: django.core.exceptions.ImproperlyConfigured: SECRET_KEY not set
💡 Check your .env file and export it before running.

✅ Issue: WebSocket connections failing
💡 Ensure you’re running daphne or have proper ASGI server configured.

✅ Issue: Database errors (e.g. no such table)
💡 Run python manage.py migrate to create tables.

✅ Issue: Static files not loading in dev
💡 Run python manage.py collectstatic and check STATIC_URL.

✅ Helpful tip:
If using Redis, ensure it’s running on default port 6379 or update REDIS_URL.

✅ Contributing
Feel free to submit pull requests to improve documentation, add features, or fix bugs.

✅ License
MIT License — see LICENSE
