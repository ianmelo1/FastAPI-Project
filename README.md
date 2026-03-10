# FastAPI-Project

A RESTful API built with **FastAPI** for managing posts with image/video uploads, user authentication, and a social feed. Files are stored via **ImageKit** and data is persisted in an async SQL database.

---

## 🚀 Features

- **User Authentication** — Register, login, password reset, and email verification via `fastapi-users`
- **JWT Authentication** — Secure token-based auth for all protected routes
- **File Upload** — Upload images and videos, stored on ImageKit CDN
- **Post Feed** — Paginated feed of posts ordered by creation date
- **Post Deletion** — Delete posts by ID (authenticated users only)

---

## 🗂️ Project Structure

```
FastAPI-Project/
├── app/
│   ├── __init__.py
│   ├── app.py          # FastAPI app and route definitions
│   ├── db.py           # Database models and async session setup
│   ├── images.py       # ImageKit configuration
│   ├── schemas.py      # Pydantic schemas (Post, User)
│   └── users.py        # fastapi-users configuration and auth backend
├── main.py             # Entry point
├── pyproject.toml      # Project dependencies and metadata
└── uv.lock             # Lockfile (uv package manager)
```

---

## 📦 Tech Stack

| Tool | Purpose |
|---|---|
| [FastAPI](https://fastapi.tiangolo.com/) | Web framework |
| [fastapi-users](https://fastapi-users.github.io/) | User auth & management |
| [SQLAlchemy (async)](https://docs.sqlalchemy.org/) | ORM & database |
| [ImageKit](https://imagekit.io/) | CDN file storage |
| [uv](https://github.com/astral-sh/uv) | Package manager |

---

## ⚙️ Setup & Installation

### Prerequisites

- Python 3.11+
- [uv](https://github.com/astral-sh/uv) installed
- An [ImageKit](https://imagekit.io/) account

### 1. Clone the repository

```bash
git clone https://github.com/ianmelo1/FastAPI-Project.git
cd FastAPI-Project
```

### 2. Install dependencies

```bash
uv sync
```

### 3. Configure environment variables

Create a `.env` file in the project root:

```env
IMAGEKIT_PUBLIC_KEY=your_public_key
IMAGEKIT_PRIVATE_KEY=your_private_key
IMAGEKIT_URL_ENDPOINT=https://ik.imagekit.io/your_id
IMAGEKIT_URL=https://ik.imagekit.io/your_id

DATABASE_URL=sqlite+aiosqlite:///./dev.db   # or your async DB URL

SECRET=your_jwt_secret_key
```

### 4. Run the server

```bash
uv run uvicorn main:app --reload
```

The API will be available at `http://localhost:8000`.

---

## 📡 API Endpoints

### Auth

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/auth/register` | Register a new user |
| `POST` | `/auth/jwt/login` | Login and receive JWT token |
| `POST` | `/auth/forgot-password` | Request password reset |
| `POST` | `/auth/reset-password` | Reset password |
| `POST` | `/auth/request-verify-token` | Request email verification |
| `POST` | `/auth/verify` | Verify email |

### Users

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/users/me` | Get current user |
| `PATCH` | `/users/me` | Update current user |

### Posts

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/upload` | Upload an image or video (authenticated) |
| `GET` | `/feed` | Get all posts ordered by newest (authenticated) |
| `DELETE` | `/posts/{post_id}` | Delete a post by ID (authenticated) |

---

## 🔐 Authentication

All post routes require a valid JWT token. Include the token in the `Authorization` header:

```
Authorization: Bearer <your_token>
```

---

## 🖼️ Upload Example

```bash
curl -X POST http://localhost:8000/upload \
  -H "Authorization: Bearer <token>" \
  -F "file=@photo.jpg" \
  -F "caption=My first post"
```

---

## 📄 License

This project is open source. Feel free to use, modify, and distribute.