# RBAC Manager — Access Control Demo

> **University Cybersecurity Project** — Role-Based Access Control (RBAC) system built with Next.js 14, Supabase, and TypeScript.

---

## Features

| Feature | Description |
|---|---|
| ✅ User Management CRUD | View all users, assign/remove roles, delete accounts |
| ✅ Role Creation | Create custom roles with descriptions |
| ✅ Visual Permission Matrix | Interactive checkbox grid per role × resource |
| ✅ Audit Trail | Searchable, filterable access log with status badges |
| ✅ Authentication | Email/password login via Supabase Auth |
| ✅ Route Protection | Middleware-based redirect for unauthenticated users |
| ✅ Row Level Security | RLS enabled on all Supabase tables |

---

## Tech Stack

- **Framework**: Next.js 14 (App Router, Server Actions)
- **Database & Auth**: Supabase (PostgreSQL + RLS)
- **Language**: TypeScript
- **Styling**: CSS Modules (glassmorphism design system)
- **Runtime**: Node.js
- **Deploy**: Vercel

---

## Project Structure

```
rbac-demo/
├── app/                    # Next.js App Router pages
│   ├── page.tsx            # Landing / Home
│   ├── login/              # Login page
│   ├── signup/             # Signup page
│   ├── dashboard/          # Stats overview
│   ├── users/              # User management CRUD
│   ├── roles/              # Role management
│   ├── permissions/        # Visual permission matrix
│   └── audit/              # Access log & audit trail
├── components/             # Reusable UI components
│   ├── Header.tsx
│   ├── Footer.tsx
│   ├── UserTable.tsx       # Paginated user table with edit/delete
│   ├── RoleCard.tsx        # Role cards with permission summary
│   ├── PermissionMatrix.tsx# Interactive checkbox matrix
│   ├── AuditLog.tsx        # Filterable log table
│   └── ui/                 # Badge, Card, Modal primitives
├── lib/
│   ├── types.ts            # TypeScript interfaces
│   ├── supabase/           # Client, server, middleware helpers
│   └── actions/            # Server Actions (auth, users, roles, audit)
└── data/
    └── schema.sql          # Full DB schema + seed data
```

---

## Setup Instructions

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/rbac-demo.git
cd rbac-demo
```

### 2. Install dependencies

```bash
npm install
```

### 3. Set up Supabase

1. Create a project at [supabase.com](https://supabase.com)
2. Go to **SQL Editor** and run the full contents of [`data/schema.sql`](./data/schema.sql)
3. Enable **Email/Password** authentication in Authentication → Providers

### 4. Configure environment variables

```bash
cp .env.local.example .env.local
```

Fill in your values from the Supabase project dashboard:

```env
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key
```

### 5. Run the development server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

---

## Database Schema

```
roles              → id, name, description
permissions        → id, name, resource, action, description
role_permissions   → role_id, permission_id (many-to-many)
user_profiles      → id (→ auth.users), full_name, email
user_roles         → user_id, role_id (many-to-many)
access_logs        → id, user_id, action, resource, status, details
```

RLS is enabled on all tables. The service-role key is used server-side for admin operations only.

---

## Deployment (Vercel)

1. Push your repo to GitHub
2. Import the project at [vercel.com/new](https://vercel.com/new)
3. Add the three environment variables in **Settings → Environment Variables**
4. Deploy — Vercel will auto-detect Next.js

---

## Screenshots

> _(Add screenshots here after deployment)_

| Page | Description |
|---|---|
| `/` | Landing page with feature overview |
| `/dashboard` | Stats cards + recent activity feed |
| `/users` | Searchable user table with role assignment |
| `/roles` | Role cards with permission counts |
| `/permissions` | Full permission matrix editor |
| `/audit` | Event log with status filters |
