
# 🐞 Issue Tracker

A modern, full-stack issue tracking application built with **Next.js 14 App Router**, **Prisma**, **PostgreSQL**, and **NextAuth.js** (Google OAuth). Built for developers and teams to track bugs and tasks with ease, authentication secured by Google login.

---

## 🔧 Tech Stack

| Layer      | Tech                            |
| ---------- | ------------------------------- |
| Frontend   | Next.js 14 (App Router) + React |
| Backend    | App Router API Routes           |
| Auth       | NextAuth.js with Google OAuth   |
| ORM/DB     | Prisma + PostgreSQL (Supabase)  |
| Deployment | Vercel                          |

---

## ✨ Features

- ✅ Google OAuth login using NextAuth.js
- 🔐 Secured authentication with JWT sessions
- 📄 Issue creation, update, and listing _(if implemented)_
- 📦 Type-safe PostgreSQL integration using Prisma
- 🌐 Hosted on Vercel with optimized build

---

## ⚙️ Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/mangusingh01/Issue-Tracker.git
cd Issue-Tracker
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment Variables

```bash
DATABASE_URL=postgresql://USER:PASSWORD@HOST:PORT/DATABASE
GOOGLE_CLIENT_ID=your_google_oauth_client_id
GOOGLE_CLIENT_SECRET=your_google_oauth_client_secret
NEXTAUTH_SECRET=your_nextauth_secret
```

Generate a Secure `NEXTAUTH_SECRET`

```bash
openssl rand -base64 32
```

### 4. Useful Prisma commands

```bash
npx prisma generate
npx prisma db push
npx prisma migrate dev --name init
npx prisma studio

```

### 5. Local Dev

```bash
npm run dev
```
---
<p align="center">
<a href="https://github.com/mangusingh01"><img src="https://user-images.githubusercontent.com/58532023/171219272-a68dd897-a9c7-4826-b7e6-10ef84e6a0a8.png" alt="GitHub"/></a>
<a href="https://www.linkedin.com/in/mangu-singh/"><img src="https://user-images.githubusercontent.com/58532023/171219303-8839f911-21bf-453f-b517-9dd6ef9a873c.png" alt="LinkedIn"/></a>
</p>
