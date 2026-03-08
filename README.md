# 🎬 Movies API - Documentation

<div align="center">

![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi)
![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-black?style=for-the-badge&logo=JSON%20web%20tokens)
![Render](https://img.shields.io/badge/Render-46E3B7?style=for-the-badge&logo=render&logoColor=white)
![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

**A powerful REST API for movie management with JWT authentication and Supabase integration**

[Getting Started](#-getting-started) •
[Features](#-features) •
[API Endpoints](#-api-endpoints) •
[Testing Guide](#-testing-guide) •
[Troubleshooting](#-troubleshooting)

</div>

---

## 📖 Overview

This API provides a complete backend solution for movie catalog management. Built with **FastAPI** for high performance and **Supabase** for robust data persistence, it offers secure authentication and full CRUD operations.

### ✨ Features

- ✅ **Complete CRUD operations** for movies
- 🔐 **JWT authentication** via Supabase Auth
- 🚀 **High performance** with FastAPI
- 🗄️ **PostgreSQL database** managed by Supabase
- 📊 **Query filtering** and pagination
- 🧪 **Ready-to-use Postman collections**
- 🌐 **Hosted on Render** for easy access

---

## 🛠️ Technology Stack

| Layer | Technology | Purpose |
|-------|------------|---------|
| **Backend** | FastAPI (Python) | High-performance API framework |
| **Database** | Supabase (PostgreSQL) | Data persistence & real-time features |
| **Auth** | Supabase Auth | JWT authentication & user management |
| **Hosting** | Render | Cloud deployment & scaling |
| **Testing** | Postman | API testing & documentation |

---

## 📋 API Endpoints

### 🔍 Quick Reference

| Method | Endpoint | Description | Auth Required |
|:-------|:---------|:------------|:--------------|
| 🟢 GET | `/health` | Check API status | ❌ No |
| 🟢 GET | `/movies` | List all movies | ✅ Yes |
| 🟢 GET | `/movies/{id}` | Get movie by ID | ✅ Yes |
| 🟡 POST | `/movies` | Create new movie | ✅ Yes |
| 🟠 PUT | `/movies/{id}` | Update movie | ✅ Yes |
| 🔴 DELETE | `/movies/{id}` | Delete movie | ✅ Yes |

### 📊 Data Model

```json
{
  "id": "uuid",
  "title": "string (1-200 chars)",
  "description": "string",
  "release_year": "integer (1888-current)",
  "duration": "integer (minutes)",
  "genre": "string",
  "director": "string",
  "rating": "float (0-10)",
  "user_id": "uuid",
  "created_at": "timestamp",
  "updated_at": "timestamp"
}
```

---

## 🚀 Getting Started

### Prerequisites

- 📬 [Postman](https://www.postman.com/) installed
- 🔑 Supabase project with `anon_key`
- 🌐 Render deployment (or local development server)

### 📦 Required Files

Download these files to get started:
```
📁 Postman Collections/
├── 📄 [PRD] Movies API.postman_environment.json
├── 📄 User.postman_collection.json
└── 📄 Movies API.postman_collection.json
```

### ⚙️ Environment Setup

1. **Import files** into Postman
2. **Select environment** "[PRD] Movies API"
3. **Configure variables:**

| Variable | Example Value | Description |
|----------|---------------|-------------|
| `api_url` | `https://your-app.onrender.com` | Your deployed API URL |
| `supabase_url` | `https://xyz.supabase.co` | Your Supabase project URL |
| `api_key` | `eyJhbGciOiJIUzI1NiIs...` | Your SUPABASE_ANON_KEY |

---

## 🧪 Testing Guide

### 📝 Testing Flow Diagram

```
┌─────────────┐
│   Step 1    │
│    Setup    │
└──────┬──────┘
       ↓
┌─────────────┐
│   Step 2    │ ◄─────────────────┐
│  Sign Up/   │                    │
│    Login    │                    │
└──────┬──────┘                    │
       ↓ (get token & user_id)      │
┌─────────────┐                    │
│   Step 3    │                    │
│  Health     │                    │
│   Check     │                    │
└──────┬──────┘                    │
       ↓                            │
┌─────────────┐                    │
│   Step 4    │                    │
│   Create    │ ───┐ (get movie_id) │
│    Movie    │    │                │
└──────┬──────┘    │                │
       ↓           ↓                │
┌─────────────┐ ┌─────────────┐     │
│   Step 5    │ │   Step 6    │     │
│    Get      │ │   Update    │     │
│   Movie     │ │    Movie    │     │
└──────┬──────┘ └──────┬──────┘     │
       ↓               ↓             │
┌─────────────┐ ┌─────────────┐     │
│   Step 7    │ │   Step 8    │     │
│   Filter    │ │   Delete    │ ────┘
│   Movies    │ │    Movie    │
└─────────────┘ └─────────────┘
```

### Step-by-Step Testing

#### 🎯 Step 1: Health Check
```bash
GET {{api_url}}/health
```
✅ **Expected**: `{"status": "healthy"}`

#### 🔐 Step 2: Authentication

**Sign Up** (if needed):
```json
POST {{api_url}}/auth/signup
{
  "email": "user@example.com",
  "password": "SecurePass123"
}
```

**Login** (required):
```json
POST {{api_url}}/auth/login
{
  "email": "user@example.com",
  "password": "SecurePass123"
}
```
✅ **Success**: Automatically stores `access_token` and `user_id`

#### 🎬 Step 3: Create a Movie
```json
POST {{api_url}}/movies
{
  "title": "Inception",
  "description": "A thief who steals corporate secrets through dream-sharing technology",
  "release_year": 2010,
  "duration": 148,
  "genre": "Sci-Fi",
  "director": "Christopher Nolan",
  "rating": 8.8,
  "user_id": "{{user_id}}"
}
```
✅ **Success**: Returns movie object with `id` (auto-saved as `movie_id`)

#### 🔍 Step 4: Query with Filters

| Filter | Example | Description |
|--------|---------|-------------|
| Genre | `?genre=Sci-Fi` | Filter by genre |
| Rating | `?min_rating=8.5` | Minimum rating |
| Director | `?director=Nolan` | Filter by director |
| Pagination | `?limit=10&offset=20` | Paginate results |

**Example:**
```
GET {{api_url}}/movies?genre=Sci-Fi&min_rating=8.0&limit=5
```

---

## 📊 Postman Collection Details

### User Collection
```
📁 User
├── 📝 Create User (Optional)
└── 🔑 Login (Required)
```

### Movies API Collection
```
📁 Movies API
├── 🏥 Health Check
├── 📋 List Movies
├── 🔍 Get Movie by ID
├── ➕ Create Movie
├── 📝 Update Movie
├── 🗑️ Delete Movie
└── 🎯 Filter Movies
    ├── By Genre
    ├── By Director
    └── By Minimum Rating
```

---

## 🐛 Troubleshooting

### Common Issues & Solutions

| Issue | Error | Solution |
|-------|-------|----------|
| **Authentication** | `401 Unauthorized` | Run Login again - token expired |
| **Not Found** | `404 Not Found` | Check if `movie_id` is set correctly |
| **Invalid Data** | `400 Bad Request` | Verify field validations |
| **Timeout** | `504 Gateway Timeout` | Render might be sleeping - wait 30s |
| **Database** | `500 Internal Error` | Check Supabase connection |

### Quick Fixes

```bash
# 1. Always start with Login
POST {{api_url}}/auth/login

# 2. Verify your token is set
# Check Postman → Environment → access_token

# 3. Wake up Render (if asleep)
GET {{api_url}}/health
# Wait 30 seconds, then retry
```

---

## 📈 Best Practices

1. **Always run Login first** before any movie operations
2. **Use Health Check** to verify API availability
3. **Create a test movie** before testing updates/deletes
4. **Check environment variables** if requests fail
5. **Use filters** to test specific scenarios

---

## 🤝 Contributing

Contributions are welcome! Feel free to:
- 🐛 Report bugs
- 💡 Suggest features
- 🔧 Submit PRs
