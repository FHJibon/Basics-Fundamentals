# Next.js Fundamentals — Complete Guide (28 Notes)

> Source: [Ashraful-Momen/NextJS / MyNotes / 1. Fundamental](https://github.com/Ashraful-Momen/NextJS/tree/main/MyNotes/1.%20Fundamental). 


---

## Table of Contents

| \# | Topic | Source File |
| --- | --- | --- |
| 0 | Next.js Folder Structure | `0. Next Js Folder Structure.md` |
| 1 | Layout — Header + Body + Footer | `1. Layout - Header + Body(children - dynamic)+ footer.md` |
| 1.1 | Layout — Page-Wise Layout | `1.1. Layout - page ways layout.md` |
| 1.2 | Layout Page-Ways + Route Groups | `1.2. Layout page ways + Route Group.md` |
| 2 | Folder-Base Route & Page | `2. Folder Base Route and Page.md` |
| 3.0 | Route Params | `3.0. Route Params.md` |
| 3.1 | Route Params + Search Params | `3.1. Route Parame and Search Params.md` |
| 4 | ORM Complete Note | `4. ORM Complete Note.md` |
| 4.0 | ORM — DB Transactions (ACID) | `4.0. ORM - DB Transiction (ACID).md` |
| 4.1 | SSR + CSR with Prisma | `4.1. Complete Note - SSR + CSR with Prisma.md` |
| 5 | Middleware | `5. Middleware.md` |
| 5.1 | Complete Note — SSR+CSR+Middleware | `5.1. Complete Note -SSR+CSR+Middleware.md` |
| 6 | Form Validation & Submit | `6. Form Validation And Submit.md` |
| 6.1 | Form Submit with Zod | `6.1. Form Submit with Zod.md` |
| 7 | Zustand — State Management Complete | `7. Zustand - State Management Complete note.md` |
| 7.1 | Zustand Advanced | `7.1. Zustand Advance note.md` |
| 8 | Redux — Advanced State Management | `8. Redux - Advance State Mangement.md` |
| 8.1 | Redux Thunk | `8.1. Redux Thunk.md` |
| 9 | SWR & ISR | `9. SWR & ISR .md` |
| 9.1 | ISR + SWR Combined | `9.1. ISR and SWR combine.md` |
| 10 | Try / Catch / Finally + Error Logs | `10. Try - Catch - Final and Error Logs.md` |
| 11 | Caching (Redis) | `11. Caching .md` |
| 12 | Observer — DB Observer (Prisma Middleware) | `12. Observer - DB Observer.md` |
| 12.1 | Event-Driven / Pub-Sub with Emitter | `12.1. Event -Driven or Pub Sub with Emitter , Observer real code .md` |
| 13 | Event-Driven, Pub/Sub with EventEmitter | `13. Event Driven , Pub Sub with Emmit.md` |
| 14 | Jobs & Queue | `14. Jobs & Queue.md` |
| 15 | Advanced — Pub/Sub + Jobs + Redis + EventEmitter + BullMQ | `15. Advance - Pub Sub , Jobs and queue with redis + EventEmmit + BullMQ.md.md` |
| 16 | Testing — AAA Pattern | `16. Testing - AAA pattern.md` |

---

# 0. Next.js Folder Structure

## Basic Idea

> **Folders = Routes** → `page.js` **= What shows on that route**

## Example Structure

```bash
app/
├── page.js
├── about/
│   └── page.js
├── blog/
│   ├── page.js
│   └── post/
│       └── page.js
```

## URL → Folder Mapping

| Folder Path | URL Route | File Used |
| --- | --- | --- |
| `app/page.js` | `/` | Home page |
| `app/about/page.js` | `/about` | About page |
| `app/blog/page.js` | `/blog` | Blog list |
| `app/blog/post/page.js` | `/blog/post` | Blog post page |

## Rule

- Every folder inside `app/` becomes part of the URL.
- A route **only works if it has** `page.js` **inside**.
- Without `page.js` → no page will show.

## Dynamic Routes

```bash
app/blog/[slug]/page.js
```

URL:

```
/blog/hello-world
/blog/my-post
```

`[slug]` = dynamic value.

## Layout (Optional)

```bash
app/layout.js
```

Wraps all pages (navbar/footer shared across routes).

> **One-line summary:** Folder name = URL path; `page.js` = UI for that path.

## Recommended Full Structure

```bash
my-nextjs-app/
├── public/                     # Static assets
│   ├── images/
│   └── favicon.ico
│
├── src/                        # (optional but recommended)
│   ├── app/                    # App Router
│   │   ├── layout.js           # Root layout
│   │   ├── page.js             # Home (/)
│   │   ├── globals.css
│   │   │
│   │   ├── about/              # /about
│   │   ├── blog/               # /blog
│   │   │   └── [slug]/         # /blog/:slug
│   │   │
│   │   ├── api/                # API routes
│   │   │   └── hello/route.js
│   │   │
│   │   ├── loading.js
│   │   ├── error.js
│   │   └── not-found.js
│   │
│   ├── components/             # Reusable UI
│   │   ├── ui/
│   │   └── layout/
│   │
│   ├── lib/                    # Utilities, configs
│   ├── hooks/                  # Custom hooks
│   ├── services/               # API layer
│   ├── styles/
│   └── types/                  # TypeScript types
│
├── .env.local
├── next.config.js
├── package.json
└── tsconfig.json
```

> Notes: `app/` = new routing system (recommended); `pages/` = old router; `src/` keeps things cleaner in larger apps; API routes now use `route.js`.

---

# 1. Layout — Header + Body (children) + Footer

A clean, minimal Next.js layout setup using **global layout** + **page-level layouts**.

## Folder Structure

```bash
my-next-app/
├── app/
│   ├── layout.js          # Global layout
│   ├── page.js
│   │
│   ├── dashboard/
│   │   ├── layout.js
│   │   └── page.js
│   │
│   ├── blog/
│   │   ├── layout.js
│   │   ├── page.js
│   │   └── [slug]/page.js
│   │
│   └── components/
│       ├── Navbar.js
│       └── Footer.js
```

## Global Layout (`app/layout.js`)

```jsx
// app/layout.js
import './globals.css';
import Navbar from './components/Navbar';
import Footer from './components/Footer';

export const metadata = {
  title: 'My App',
  description: 'Simple Next.js App',
};

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>
        <Navbar />
        <main style={{ padding: '20px' }}>{children}</main>
        <Footer />
      </body>
    </html>
  );
}
```

**Explanation**

- `RootLayout` is the top-level layout. Next.js calls it for **every**route.
- It must return `<html>` and `<body>`.
- `children` is a special prop — it represents the current page or nested layout. Visiting `/` → `children = <HomePage />`.

## Home Page (`app/page.js`)

```jsx
export default function HomePage() {
  return <h1>Home Page</h1>;
}
```

## Page-Level Layout — Dashboard

```jsx
// app/dashboard/layout.js
export default function DashboardLayout({ children }) {
  return (
    <div style={{ display: 'flex' }}>
      <aside style={{ width: '200px', background: '#eee' }}>
        <p>Sidebar</p>
      </aside>
      <section style={{ flex: 1, padding: '20px' }}>{children}</section>
    </div>
  );
}
```

## Dashboard Page

```jsx
// app/dashboard/page.js
export default function DashboardPage() {
  return <h1>Dashboard</h1>;
}
```

## Blog Layout

```jsx
// app/blog/layout.js
export default function BlogLayout({ children }) {
  return (
    <div>
      <h2>Blog Layout Header</h2>
      {children}
    </div>
  );
}
```

## Navbar & Footer

```jsx
// app/components/Navbar.js
export default function Navbar() {
  return (
    <nav style={{ background: 'black', color: 'white', padding: '10px' }}>
      My Navbar
    </nav>
  );
}

// app/components/Footer.js
export default function Footer() {
  return (
    <footer style={{ background: '#ddd', padding: '10px' }}>
      My Footer
    </footer>
  );
}
```

## Key Concepts

- `app/layout.js` → global wrapper
- `app/section/layout.js` → scoped layout
- Layouts are **nested automatically**
- `children` → dynamically injected content
- No need for `_app.js` (App Router replaces it)

---

# 1.1. Layout — Page-Wise Layout

A walkthrough of creating **per-page custom layouts** with route groups.

## Folder Structure

```bash
my-next-app/
├── app/
│   ├── layout.js              # Global layout (base wrapper)
│   │
│   ├── (main)/                # Main site (default header/footer)
│   │   ├── layout.js
│   │   └── page.js
│   │
│   ├── (dashboard)/           # Dashboard (custom header/footer)
│   │   ├── layout.js
│   │   └── page.js
│   │
│   ├── (auth)/                # Auth (no header/footer)
│   │   ├── layout.js
│   │   └── login/page.js
│   │
│   └── components/
│       ├── MainHeader.js
│       ├── MainFooter.js
│       ├── DashboardHeader.js
│       └── DashboardFooter.js
```

## Global Layout (`app/layout.js`)

```jsx
export default function RootLayout({ children }) {
  return (
    <html>
      <body>{children}</body>
    </html>
  );
}
```

**Explanation:** only `<html>` and `<body>` — DO NOT hardcode header/footer here if you want flexibility.

## Main Layout — Default Header/Footer

```jsx
// app/(main)/layout.js
import MainHeader from '../components/MainHeader';
import MainFooter from '../components/MainFooter';

export default function MainLayout({ children }) {
  return (
    <>
      <MainHeader />
      <main>{children}</main>
      <MainFooter />
    </>
  );
}
```

## Dashboard Layout — Different Header/Footer

```jsx
// app/(dashboard)/layout.js
import DashboardHeader from '../components/DashboardHeader';
import DashboardFooter from '../components/DashboardFooter';

export default function DashboardLayout({ children }) {
  return (
    <div>
      <DashboardHeader />
      <div style={{ display: 'flex' }}>
        <aside>Sidebar</aside>
        <section>{children}</section>
      </div>
      <DashboardFooter />
    </div>
  );
}
```

## Auth Layout — No Header/Footer

```jsx
// app/(auth)/layout.js
export default function AuthLayout({ children }) {
  return (
    <div style={{ maxWidth: '400px', margin: 'auto' }}>
      {children}
    </div>
  );
}
```

## Core Insight

```text
RootLayout (HTML only)
   ↓
Route Group Layout (decides Header/Footer)
   ↓
Page
```

## ❌ Anti-Pattern: Conditional Rendering in Root

```jsx
import { usePathname } from 'next/navigation';

export default function RootLayout({ children }) {
  const pathname = usePathname();
  const isDashboard = pathname.startsWith('/dashboard');

  return (
    <html>
      <body>
        {isDashboard ? <DashboardHeader /> : <MainHeader />}
        {children}
        {isDashboard ? <DashboardFooter /> : <MainFooter />}
      </body>
    </html>
  );
}
```

⚠️ Issues: tight coupling, hard to scale, breaks separation of concerns.

## Mental Model

```text
Route Group decides layout

(main)       → MainHeader + Footer
(dashboard)  → DashboardHeader + Sidebar + Footer
(auth)       → No Header/Footer
```

---

# 1.2. Layout Page-Ways + Route Groups

> ✅ Global root layout (mandatory) · ✅ Completely different layouts per section · ✅ Separate Header/Footer per layout · ✅ Clean, scalable structure

## Folder Structure

```bash
my-next-app/
├── app/
│   ├── layout.tsx              # Root layout (only html/body)
│   │
│   ├── (main)/                 # Public pages
│   │   ├── layout.tsx          # Main Header/Footer
│   │   ├── page.tsx            # "/"
│   │   └── about/page.tsx      # "/about"
│   │
│   ├── (blog)/                 # Blog section (different layout)
│   │   ├── layout.tsx
│   │   ├── page.tsx            # "/blog"
│   │   └── [slug]/page.tsx     # "/blog/:slug"
│   │
│   ├── (auth)/                 # Auth (no chrome)
│   │   ├── layout.tsx
│   │   └── login/page.tsx      # "/login"
│   │
│   └── components/
│       ├── MainHeader.tsx
│       ├── MainFooter.tsx
│       ├── BlogHeader.tsx
│       └── BlogFooter.tsx
```

## Root Layout

```tsx
export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  );
}
```

## Main Layout

```tsx
import MainHeader from '../components/MainHeader';
import MainFooter from '../components/MainFooter';

export default function MainLayout({ children }: { children: React.ReactNode }) {
  return (
    <>
      <MainHeader />
      <main>{children}</main>
      <MainFooter />
    </>
  );
}
```

## Blog Layout (Different)

```tsx
import BlogHeader from '../components/BlogHeader';
import BlogFooter from '../components/BlogFooter';

export default function BlogLayout({ children }: { children: React.ReactNode }) {
  return (
    <>
      <BlogHeader />
      <section>{children}</section>
      <BlogFooter />
    </>
  );
}
```

## Auth Layout

```tsx
export default function AuthLayout({ children }: { children: React.ReactNode }) {
  return (
    <div style={{ maxWidth: '400px', margin: 'auto' }}>
      {children}
    </div>
  );
}
```

## Render Tree by Route

| URL | Layout chain |
| --- | --- |
| `/` | RootLayout → MainLayout → HomePage |
| `/blog` | RootLayout → BlogLayout → BlogPage |
| `/login` | RootLayout → AuthLayout → LoginPage |

> Layouts are **NOT** shared across route groups. Each group has its own independent layout tree. Only RootLayout is common.

---

# 2. Folder-Base Route & Page

## Tutorial — User Dashboard & User Details

```bash
app/
└─ dashboard/
   ├─ user/
   │  ├─ page.jsx       # User Dashboard
   │  └─ [id]/
   │      └─ page.jsx   # User Details
   └─ page.jsx          # Optional: dashboard main page
```

## User Dashboard

```tsx
// app/dashboard/user/page.jsx
import Link from 'next/link';

export default function UserDashboard() {
  return (
    <div>
      <h1>User Dashboard Page</h1>
      <ul>
        <li><Link href="/dashboard/user/1">User Details 1</Link></li>
        <li><Link href="/dashboard/user/2">User Details 2</Link></li>
        <li><Link href="/dashboard/user/3">User Details 3</Link></li>
      </ul>
    </div>
  );
}
```

## User Details

```tsx
// app/dashboard/user/[id]/page.jsx
export default async function UserDetails({ params }) {
  const { id } = await params;          // unwrap async params (Next 16+)

  return (
    <div>
      <h1>User Details Page</h1>
      <p>User ID: {id}</p>
      <Link href="/dashboard/user">Back to Dashboard</Link>
    </div>
  );
}
```

> Notes: `[id]` = dynamic route param. In Next.js 16+ server components, `params` is **async** — `await params`. No `'use client'` needed unless you want hooks/state. Use `<Link>` for client-side navigation.

---

# 3.0. Route Params

## Basic Routes

```jsx
// app/page.js
export default function HomePage() {
  return <h1>Home</h1>;
}

// app/about/page.js
export default function AboutPage() {
  return <h1>About</h1>;
}
```

## Dynamic Route — `[param]`

```jsx
// app/blog/[slug]/page.js
export default function BlogDetails({ params }) {
  return <h1>Slug: {params.slug}</h1>;
}
```

Visiting `/blog/hello-world` → `params = { slug: "hello-world" }`.

## Multiple Params

```jsx
// app/user/[id]/[postId]/page.js
export default function UserPost({ params }) {
  return (
    <div>
      <p>User ID: {params.id}</p>
      <p>Post ID: {params.postId}</p>
    </div>
  );
}
```

For `/user/10/55` → `params = { id: "10", postId: "55" }`.

## Navigation

```jsx
import Link from 'next/link';

export default function Home() {
  return (
    <div>
      <Link href="/about">Go to About</Link>
      <br />
      <Link href="/blog/nextjs-routing">Go to Blog Details</Link>
    </div>
  );
}
```

## Mental Model

```text
URL → Folder Structure → params injected → Component render

/product/25
→ app/product/[id]/page.js
→ params = { id: "25" }
```

---

# 3.1. Route Params + Search Params

## Query Params — `searchParams`

```jsx
// app/blog/page.js
export default function BlogPage({ searchParams }) {
  return (
    <div>
      <p>Category: {searchParams.category}</p>
      <p>Page: {searchParams.page}</p>
    </div>
  );
}
```

For `/blog?category=tech&page=2`:

```js
searchParams = { category: "tech", page: "2" }
```

| Param | Source |
| --- | --- |
| `params` | path values |
| `searchParams` | query string |

---

# 4. ORM Complete Note

> A production-ready daily reference for **Prisma ORM + Next.js + MySQL/Postgres**.

## Setup

```bash
npm install prisma @prisma/client
npx prisma init
npx prisma migrate dev --name init
npx prisma generate
npx prisma db push
npx prisma studio
```

## Prisma Client (`lib/prisma.ts`)

```typescript
import { PrismaClient } from "@prisma/client";

const globalForPrisma = global as unknown as {
  prisma: PrismaClient;
};

export const prisma =
  globalForPrisma.prisma ||
  new PrismaClient();

if (process.env.NODE_ENV !== "production") {
  globalForPrisma.prisma = prisma;
}
```

## Relationship Notation

| Notation | Meaning |
| --- | --- |
| `profile?` | Optional / nullable |
| `posts[]` | Array (one-to-many) |
| `user` | Required (mandatory relation) |

## One-to-One (1:1) — User ↔ Profile

```prisma
model User {
  id      Int      @id @default(autoincrement())
  email   String   @unique
  profile Profile?
}

model Profile {
  id     Int    @id @default(autoincrement())
  bio    String?
  userId Int    @unique
  user   User   @relation(fields: [userId], references: [id])
}
```

```typescript
await prisma.user.create({
  data: {
    email: "test@gmail.com",
    profile: { create: { bio: "Hello" } }
  }
});

await prisma.user.findUnique({
  where: { id: 1 },
  include: { profile: true }
});
```

> `@unique` on `userId` enforces one profile per user.

## One-to-Many (1:M) — User ↔ Posts

```prisma
model User {
  id    Int    @id @default(autoincrement())
  email String @unique
  posts Post[]
}

model Post {
  id     Int  @id @default(autoincrement())
  title  String
  userId Int
  user   User @relation(fields: [userId], references: [id])
}
```

```typescript
await prisma.post.create({
  data: { title: "My Post", user: { connect: { id: 1 } } }
});
```

## Many-to-Many (M:M) — Post ↔ Tags

```prisma
model Post {
  id    Int   @id @default(autoincrement())
  title String
  tags  Tag[] @relation("PostTags")
}

model Tag {
  id    Int   @id @default(autoincrement())
  name  String @unique
  posts Post[] @relation("PostTags")
}
```

```typescript
await prisma.post.create({
  data: {
    title: "Next.js Guide",
    tags: {
      connectOrCreate: [{
        where:  { name: "nextjs" },
        create: { name: "nextjs" }
      }]
    }
  }
});
```

## M:M with Custom Pivot Table

```prisma
model User {
  id      Int           @id @default(autoincrement())
  email   String        @unique
  courses UserCourse[]
}

model Course {
  id      Int           @id @default(autoincrement())
  title   String
  users   UserCourse[]
}

model UserCourse {
  userId   Int
  courseId Int
  progress Int    @default(0)
  status   String @default("pending")
  user     User   @relation(fields: [userId], references: [id])
  course   Course @relation(fields: [courseId], references: [id])

  @@id([userId, courseId])
}
```

> Automatic M:M can't store extra fields. Custom pivot allows progress, status, etc.

## CRUD

```typescript
// Read
await prisma.user.findUnique({ where: { id: 1 } });
await prisma.user.findFirst({ where: { status: "ACTIVE" } });
await prisma.user.findMany();
await prisma.user.findMany({ select: { id: true, name: true } });
await prisma.user.findMany({ include: { posts: true } });

// WHERE
where: { status: "ACTIVE" }
where: { status: { not: "ACTIVE" } }
where: { age:    { gt: 18 } }
where: { id:     { in: [1, 2, 3] } }
where: { deletedAt: null }
where: { OR:  [{ name: "John" }, { email: "john@gmail.com" }] }
where: { AND: [{ status: "ACTIVE" }, { age: { gte: 18 } }] }

// Search
where: { name:  { contains: "john", mode: "insensitive" } }
where: { name:  { startsWith: "Jo" } }
where: { email: { endsWith:   "@gmail.com" } }

// Sorting
orderBy: { id: "desc" }
orderBy: [{ status: "asc" }, { id: "desc" }]

// Pagination
const page = 2, limit = 10;
await prisma.user.findMany({
  skip: (page - 1) * limit,
  take: limit
});

// Create
await prisma.user.create({ data: { name: "John", email: "john@gmail.com" } });
await prisma.user.createMany({
  data: [{ name: "A" }, { name: "B" }]
});

// Update
await prisma.user.update({ where: { id: 1 }, data: { name: "Updated" } });
await prisma.user.updateMany({ where: { status: "PENDING" }, data: { status: "ACTIVE" } });
await prisma.user.update({
  where: { id: 1 },
  data: { loginCount: { increment: 1 } }
});

// Delete
await prisma.user.delete({ where: { id: 1 } });
await prisma.user.deleteMany({ where: { status: "BLOCKED" } });

// Soft delete
await prisma.user.update({
  where: { id: 1 },
  data:  { deletedAt: new Date() }
});

// Upsert
await prisma.user.upsert({
  where:  { email: "admin@gmail.com" },
  update: { name: "Updated" },
  create: { name: "Admin", email: "admin@gmail.com" }
});

// Transactions
await prisma.$transaction([
  prisma.user.create({ data: { name: "John" } }),
  prisma.profile.create({ data: { bio: "Hello" } })
]);

// Raw SQL
await prisma.$queryRaw`SELECT * FROM users`;
await prisma.$executeRaw`DELETE FROM users`;
```

## Most Used Pattern

```typescript
const users = await prisma.user.findMany({
  where: {
    deletedAt: null,
    OR: [
      { name:  { contains: search, mode: "insensitive" } },
      { email: { contains: search, mode: "insensitive" } }
    ]
  },
  include:  { role: true },
  orderBy:  { id: "desc" },
  skip:     (page - 1) * limit,
  take:     limit
});
```

## Recommended Project Structure

```bash
project/
├── prisma/
│   ├── schema.prisma
│   └── migrations/
│
├── src/
│   ├── app/
│   │   ├── api/{users,auth}/route.ts
│   │   ├── dashboard/
│   │   ├── login/
│   │   └── layout.tsx
│   │
│   ├── components/{ui,forms,tables}/
│   ├── lib/{prisma.ts,auth.ts,utils.ts}
│   ├── services/user.service.ts
│   ├── repositories/user.repository.ts
│   ├── validators/user.schema.ts
│   ├── types/
│   ├── hooks/
│   └── middleware.ts
│
├── .env
├── next.config.ts
└── tsconfig.json
```

## Production Best Practices

```prisma
createdAt DateTime @default(now())
updatedAt DateTime @updatedAt
@@index([email])
@@index([status])

enum Role { ADMIN USER }

@relation(fields: [userId], references: [id], onDelete: Cascade)
```

## Backend Flow

```text
Route
  ↓
Controller / Route Handler
  ↓
Service
  ↓
Repository
  ↓
Prisma ORM
  ↓
Database
```

---

# 4.0. ORM — DB Transactions (ACID)

> Transactions ensure: all queries succeed together, or all fail together. No partial data is saved.

## Two Transaction Types

```text
┌────────────────────────────────────────────────────────┐
│               PostgreSQL Transactions                  │
└────────────────────────────────────────────────────────┘
                           │
             ┌─────────────┴─────────────┐
             ▼                           ▼
   ┌────────────────────┐   ┌────────────────────┐
   │      Automatic     │   │       Manual       │
   │    (Prisma ORM)    │   │    (Raw Driver)    │
   └────────────────────┘   └────────────────────┘
             │                           │
     Auto-handles State          Explicit Management
     Commit on Success           BEGIN / COMMIT
     Rollback on Error           ROLLBACK on Error
```

## Automatic Transactions (Prisma)

```javascript
import { prisma } from "@/lib/prisma";

export async function updateStatus(id) {
  try {
    return await prisma.$transaction(async (tx) => {
      const user = await tx.user.update({
        where: { id },
        data: { status: "active" }
      });

      // add more queries using 'tx' here

      return { success: true, user };
      // <-- SUCCESS: Prisma auto COMMITS
    });
  } catch (error) {
    // <-- FAILURE: Prisma auto ROLLBACKS
    return { success: false, error: error.message };
  }
}
```

**Automatic Flow**

```text
Start $transaction Block
           │
           ▼
   Run Query 1 (tx)
           │
           ├── Any Error Found?
           │       ▼
           │   Auto ROLLBACK Database
           │
           └── All Queries Clean?
                   ▼
               Auto COMMIT Database
```

## Manual Transactions (Raw `pg` Driver)

```javascript
import { Pool } from "pg";

const pool = new Pool();

export async function updateStatusManual(id) {
  const client = await pool.connect();

  try {
    await client.query("BEGIN");

    const queryStr = "UPDATE users SET status = 'active' WHERE id = $1";
    await client.query(queryStr, [id]);

    await client.query("COMMIT");
    return { success: true };

  } catch (error) {
    await client.query("ROLLBACK");
    return { success: false, error: error.message };

  } finally {
    client.release();       // always free the connection
  }
}
```

## Method Comparison

| Feature | Prisma (Automatic) | pg Driver (Manual) |
| --- | --- | --- |
| Command Syntax | Safe JavaScript Objects | Raw SQL Strings ($1 variables) |
| Commit Trigger | Implicit at final `}` | Explicit `client.query('COMMIT')` |
| Rollback Trigger | Implicit on code throw | Explicit `client.query('ROLLBACK')` |
| Connection Closing | Automatic | Manual via `client.release()` |

## Forcing Manual Rollback in Prisma

```javascript
await prisma.$transaction(async (tx) => {
  const user = await tx.user.update({
    where: { id },
    data:  { status: "active" }
  });

  if (user.isBlocked) {
    throw new Error("Cannot activate a blocked user profile");
    // throws → triggers auto-ROLLBACK
  }
});
```

## Critical Rules

```javascript
// ❌ WRONG — runs outside transaction
await prisma.user.update(...);

// ✅ RIGHT — bound to transaction thread
await tx.user.update(...);
```

And always use `client.release()` inside `finally {}` when using the raw `pg` driver.

---

# 4.1. SSR + CSR with Prisma — Complete CRUD

## Full Architecture

```text
NEXT.JS FULL STACK
┌──────────────────────────────────────────────────────────────┐
│                       FRONTEND                               │
│   ┌──────────────────────────────────────────────────────┐   │
│   │          SERVER COMPONENT (SSR)                      │   │
│   │   - Fetch Database Data                              │   │
│   │   - SEO Friendly                                     │   │
│   │   - Fast First Load                                  │   │
│   └──────────────────────────────────────────────────────┘   │
│                           ▼                                  │
│   ┌──────────────────────────────────────────────────────┐   │
│   │          CLIENT COMPONENT (CSR)                      │   │
│   │   - Add/Edit/Delete Buttons · Form · useState        │   │
│   └──────────────────────────────────────────────────────┘   │
└──────────────────────────────────────────────────────────────┘
                            │
                  ┌─────────┴─────────┐
                  ▼                   ▼
            API Routes          Prisma ORM
                              MySQL/Postgres
```

## SSR vs CSR

| Feature | SSR | CSR |
| --- | --- | --- |
| Runs On | Server | Browser |
| Best For | Data fetching | Button clicks |
| SEO | Yes | No |
| Hooks | No | Yes |
| Default in Next.js | Yes | No |

## Project Structure

```bash
next-crud-app/
├── app/
│   ├── api/users/{route.js,[id]/route.js}
│   ├── page.jsx
│   └── layout.jsx
├── components/{AddButton,EditButton,DeleteButton,UserTable}.jsx
├── prisma/schema.prisma
├── lib/prisma.js
└── .env
```

## Prisma Setup

```bash
npm install prisma @prisma/client
npx prisma init
```

```prisma
// prisma/schema.prisma
generator client { provider = "prisma-client-js" }
datasource db    { provider = "mysql" url = env("DATABASE_URL") }

model User {
  id        Int      @id @default(autoincrement())
  name      String
  email     String   @unique
  createdAt DateTime @default(now())
}
```

```bash
npx prisma migrate dev --name init
npx prisma generate
```

## SSR Page

```jsx
// app/page.jsx
import { prisma } from "@/lib/prisma";
import UserTable from "@/components/UserTable";

export default async function HomePage() {
  const users = await prisma.user.findMany({ orderBy: { id: "desc" } });

  return (
    <div>
      <h1>User List (SSR)</h1>
      <UserTable users={users} />
    </div>
  );
}
```

## CSR — Add Button

```jsx
// components/AddButton.jsx
"use client";
import { useState } from "react";

export default function AddButton() {
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");

  async function addUser() {
    await fetch("/api/users", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ name, email }),
    });
    alert("User Added");
  }

  return (
    <div>
      <input placeholder="Name"    value={name}  onChange={(e) => setName(e.target.value)} />
      <input placeholder="Email"   value={email} onChange={(e) => setEmail(e.target.value)} />
      <button onClick={addUser}>Add User</button>
    </div>
  );
}
```

## CSR — Edit & Delete Buttons

```jsx
// components/EditButton.jsx
"use client";
export default function EditButton({ id }) {
  async function updateUser() {
    await fetch(`/api/users/${id}`, {
      method: "PUT",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ name: "Updated User" }),
    });
    alert("User Updated");
  }
  return <button onClick={updateUser}>Edit</button>;
}

// components/DeleteButton.jsx
"use client";
export default function DeleteButton({ id }) {
  async function deleteUser() {
    await fetch(`/api/users/${id}`, { method: "DELETE" });
    alert("User Deleted");
  }
  return <button onClick={deleteUser}>Delete</button>;
}
```

## User Table

```jsx
// components/UserTable.jsx
import AddButton    from "./AddButton";
import EditButton   from "./EditButton";
import DeleteButton from "./DeleteButton";

export default function UserTable({ users }) {
  return (
    <div>
      <AddButton />
      <hr />
      {users.map((user) => (
        <div key={user.id}>
          <h3>{user.name}</h3>
          <p>{user.email}</p>
          <EditButton   id={user.id} />
          <DeleteButton id={user.id} />
        </div>
      ))}
    </div>
  );
}
```

## API — GET / POST

```js
// app/api/users/route.js
import { prisma } from "@/lib/prisma";

export async function GET() {
  const users = await prisma.user.findMany();
  return Response.json(users);
}

export async function POST(req) {
  const body = await req.json();
  const user = await prisma.user.create({ data: { name: body.name, email: body.email } });
  return Response.json({ message: "User Created", data: user });
}
```

## API — PUT / DELETE

```js
// app/api/users/[id]/route.js
import { prisma } from "@/lib/prisma";

export async function PUT(req, { params }) {
  const body = await req.json();
  const user = await prisma.user.update({
    where: { id: Number(params.id) },
    data:   { name: body.name },
  });
  return Response.json({ message: "User Updated", data: user });
}

export async function DELETE(req, { params }) {
  await prisma.user.delete({ where: { id: Number(params.id) } });
  return Response.json({ message: "User Deleted" });
}
```

## Prisma CRUD Methods

| Method | Purpose |
| --- | --- |
| `prisma.user.findMany()` | Get all |
| `prisma.user.findUnique()` | Get one |
| `prisma.user.create()` | Insert |
| `prisma.user.update()` | Update |
| `prisma.user.delete()` | Delete |

## Important Next.js Rules

- Server Component = DEFAULT
- `"use client"` for useState / useEffect / onClick
- API Route = Backend
- Prisma = ORM layer

---

# 5. Middleware

> Middleware runs **before** the request reaches a page or API. It can check auth, role, redirect, block, rate-limit, modify requests, and protect routes.

## File Location

```text
project-root/
├── middleware.js
└── app/
```

The file **must** stay in the root.

## Basic Structure

```js
import { NextResponse } from "next/server";

export function middleware(req) {
  return NextResponse.next();
}
```

## Request Object

```text
req
 ├── req.nextUrl            # URL helpers
 ├── req.cookies
 ├── req.headers
 ├── req.method
 └── req.ip
```

```js
const path  = req.nextUrl.pathname;
const page  = req.nextUrl.searchParams.get("page");
const token = req.cookies.get("token")?.value;
const ua    = req.headers.get("user-agent");
const method = req.method;
```

## Response Methods

| Method | Purpose |
| --- | --- |
| `NextResponse.next()` | Continue request |
| `NextResponse.redirect()` | Redirect user |
| `NextResponse.rewrite()` | Rewrite URL |
| `NextResponse.json()` | Return JSON |

## Auth Middleware

```js
import { NextResponse } from "next/server";

export function middleware(req) {
  const token = req.cookies.get("token")?.value;
  const path  = req.nextUrl.pathname;

  const publicRoutes  = ["/login", "/register"];
  const privateRoutes = ["/dashboard", "/profile"];
  const isPublic  = publicRoutes.includes(path);
  const isPrivate = privateRoutes.includes(path);

  if (!token && isPrivate) {
    return NextResponse.redirect(new URL("/login", req.url));
  }

  if (token && isPublic) {
    return NextResponse.redirect(new URL("/dashboard", req.url));
  }

  return NextResponse.next();
}
```

## Role-Based Access

```js
const role = req.cookies.get("role")?.value;

if (path.startsWith("/admin") && role !== "admin") {
  return NextResponse.redirect(new URL("/403", req.url));
}
```

## Rate Limiting (in-memory)

```js
import { NextResponse } from "next/server";

const ipRequests = new Map();
const WINDOW_MS  = 60 * 1000;
const MAX_REQ    = 5;

export function middleware(req) {
  const ip  = req.ip || "unknown";
  const now = Date.now();
  const data = ipRequests.get(ip);

  if (!data) {
    ipRequests.set(ip, { count: 1, startTime: now });
    return NextResponse.next();
  }

  if (now - data.startTime > WINDOW_MS) {
    ipRequests.set(ip, { count: 1, startTime: now });
    return NextResponse.next();
  }

  data.count++;

  if (data.count > MAX_REQ) {
    return NextResponse.json(
      { message: "Too Many Requests" },
      { status: 429 }
    );
  }

  return NextResponse.next();
}
```

## Matcher — Limit Routes

```js
export const config = {
  matcher: [
    "/dashboard/:path*",
    "/admin/:path*",
    "/api/:path*"
  ],
};
```

| Matcher | Meaning |
| --- | --- |
| `/dashboard/:path*` | All dashboard routes |
| `/admin/:path*` | All admin routes |
| `/api/:path*` | All API routes |

## Express vs Next.js Middleware

| Framework | Signature |
| --- | --- |
| Express | `(req, res, next)` |
| Next.js | `(req)` + `NextResponse.next()` |

## Important Rules

- Middleware runs **before** page/API
- Use matcher to control routes
- Keep middleware **fast**
- Avoid heavy DB queries in middleware
- Best for auth, role, redirect, rate limit

---

# 5.1. Complete Note — SSR + CSR + Middleware

This combines SSR / CSR / Middleware / Prisma into one full-stack pattern.

## Project Structure

```bash
next-crud-app/
├── app/
│   ├── api/users/{route.js,[id]/route.js}
│   ├── dashboard/page.jsx
│   ├── login/page.jsx
│   ├── page.jsx
│   └── layout.jsx
├── components/{AddButton,EditButton,DeleteButton,UserTable}.jsx
├── prisma/schema.prisma
├── lib/prisma.js
├── middleware.js
└── .env
```

## Prisma Schema

```prisma
generator client { provider = "prisma-client-js" }
datasource db    { provider = "mysql" url = env("DATABASE_URL") }

model User {
  id        Int      @id @default(autoincrement())
  name      String
  email     String   @unique
  createdAt DateTime @default(now())
}
```

## SSR Page

```jsx
// app/page.jsx
import { prisma } from "@/lib/prisma";
import UserTable from "@/components/UserTable";

export default async function HomePage() {
  const users = await prisma.user.findMany({ orderBy: { id: "desc" } });
  return (
    <div>
      <h1>User List (SSR)</h1>
      <UserTable users={users} />
    </div>
  );
}
```

## CSR Add/Edit/Delete — see 4.1 for full code

```jsx
"use client";
import { useState } from "react";
// ... AddButton / EditButton / DeleteButton as shown in 4.1
```

## Auth Middleware

```js
// middleware.js
import { NextResponse } from "next/server";

export function middleware(req) {
  const path  = req.nextUrl.pathname;
  const token = req.cookies.get("token")?.value;
  const publicRoutes = ["/login", "/register"];
  const isPublic = publicRoutes.includes(path);

  if (!token && !isPublic) {
    return NextResponse.redirect(new URL("/login", req.url));
  }
  if (token && isPublic) {
    return NextResponse.redirect(new URL("/dashboard", req.url));
  }
  return NextResponse.next();
}

export const config = {
  matcher: [
    "/dashboard/:path*",
    "/profile/:path*",
    "/admin/:path*",
    "/login",
    "/register",
  ],
};
```

## Login / Logout API

```js
// app/api/login/route.js
import { NextResponse } from "next/server";

export async function POST(req) {
  const body = await req.json();

  if (body.email === "admin@gmail.com" && body.password === "123456") {
    const response = NextResponse.json({ message: "Login Success" });
    response.cookies.set("token", "abc123");
    return response;
  }
  return NextResponse.json({ message: "Invalid Credential" });
}

// app/api/logout/route.js
import { NextResponse } from "next/server";

export async function POST() {
  const response = NextResponse.json({ message: "Logout Success" });
  response.cookies.delete("token");
  return response;
}
```

## Full Real-World Flow

```text
USER OPEN PAGE
        ▼
MIDDLEWARE CHECK
        ├── INVALID TOKEN → REDIRECT LOGIN
        └── VALID TOKEN
                 ▼
          SSR FETCH DATA
                 ▼
            PRISMA ORM
                 ▼
              DATABASE
                 ▼
          RENDER HTML PAGE
                 ▼
         CSR BUTTON CLICK
                 ▼
          API CRUD REQUEST
                 ▼
              DATABASE
                 ▼
            UPDATE UI
```

---

# 6. Form Validation & Submit

> Validate BOTH client-side (UX) AND server-side (security).

## Why Validate?

- Empty input
- Wrong email
- Weak password
- Invalid data

## Why Server-Side?

```text
Frontend can be bypassed — server validation is the REAL security.
```

## Folder Structure

```bash
app/
├── register/page.jsx
├── api/register/route.js
components/
└── RegisterForm.jsx
```

## Client Form (Basic — `useState`)

```jsx
"use client";
import { useState } from "react";

export default function RegisterForm() {
  const [name, setName]         = useState("");
  const [email, setEmail]       = useState("");
  const [password, setPassword] = useState("");

  return (
    <div>
      <input placeholder="Name"     value={name}     onChange={(e) => setName(e.target.value)} />
      <input placeholder="Email"    value={email}    onChange={(e) => setEmail(e.target.value)} />
      <input placeholder="Password" value={password} onChange={(e) => setPassword(e.target.value)} />
      <button>Register</button>
    </div>
  );
}
```

## Full Validation Example

```jsx
"use client";
import { useState } from "react";

export default function RegisterForm() {
  const [name, setName]         = useState("");
  const [email, setEmail]       = useState("");
  const [password, setPassword] = useState("");
  const [errors, setErrors]     = useState({});
  const [loading, setLoading]   = useState(false);

  function validateForm() {
    const newErrors = {};
    if (!name)                              newErrors.name     = "Name is required";
    if (!email)                             newErrors.email    = "Email is required";
    else if (!email.includes("@"))          newErrors.email    = "Invalid email";
    if (!password)                          newErrors.password = "Password is required";
    else if (password.length < 6)           newErrors.password = "Minimum 6 characters";

    setErrors(newErrors);
    return Object.keys(newErrors).length === 0;
  }

  async function handleSubmit(e) {
    e.preventDefault();
    if (!validateForm()) return;

    setLoading(true);
    await fetch("/api/register", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ name, email, password }),
    });
    setLoading(false);
    alert("Register Success");
  }

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <input placeholder="Name" value={name} onChange={(e) => setName(e.target.value)} />
        {errors.name && <p>{errors.name}</p>}
      </div>
      <div>
        <input placeholder="Email" value={email} onChange={(e) => setEmail(e.target.value)} />
        {errors.email && <p>{errors.email}</p>}
      </div>
      <div>
        <input placeholder="Password" type="password" value={password} onChange={(e) => setPassword(e.target.value)} />
        {errors.password && <p>{errors.password}</p>}
      </div>
      <button type="submit" disabled={loading}>
        {loading ? "Loading..." : "Register"}
      </button>
    </form>
  );
}
```

## API Route (Server-Side Validation)

```js
// app/api/register/route.js
import { prisma } from "@/lib/prisma";

export async function POST(req) {
  const body = await req.json();

  if (!body.name)
    return Response.json({ message: "Name required" });
  if (!body.email)
    return Response.json({ message: "Email required" });
  if (body.password.length < 6)
    return Response.json({ message: "Weak password" });

  const user = await prisma.user.create({
    data: { name: body.name, email: body.email, password: body.password },
  });

  return Response.json({ message: "Success", data: user });
}
```

## Email Regex

```js
const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
if (!emailRegex.test(email)) newErrors.email = "Invalid email";
```

## Password Confirm

```jsx
if (password !== confirmPassword) {
  newErrors.confirmPassword = "Password not match";
}
```

## Form Best Practices

- Always validate on server
- Show error under each field
- Disable button while loading
- Never trust frontend validation
- Use controlled inputs

---

# 6.1. Form Submit with Zod (React Hook Form + Zod)

## Architecture

```text
NEXT.JS MODERN FORM FLOW
┌──────────────────────────────────────────────────────┐
│           CLIENT COMPONENT (CSR)                     │
│   ┌──────────────────────────────────────────────┐   │
│   │       React Hook Form + Zod                 │   │
│   │   - Input Register · Validation · Errors     │   │
│   │   - Submit Handling · Loading State          │   │
│   └──────────────────────────────────────────────┘   │
└──────────────────────────────────────────────────────┘
                        │
                        ▼
                 fetch("/api/register")
                        │
                        ▼
┌──────────────────────────────────────────────────────┐
│                    API ROUTE                         │
│   - Validate Again with Zod · Save DB · Return JSON │
└──────────────────────────────────────────────────────┘
                        │
                        ▼
                 Prisma ORM + Database
```

## Why React Hook Form + Zod?

- Without libraries, `useState × 4 + manual validation` becomes messy.
- Modern industry stack: **RHF + Zod + Prisma + Next.js API**

## Install

```bash
npm install react-hook-form zod @hookform/resolvers
```

## Zod Schema

```js
// schemas/registerSchema.js
import { z } from "zod";

export const registerSchema = z.object({
  name:     z.string().min(3, "Minimum 3 characters"),
  email:    z.email("Invalid email"),
  password: z.string().min(6, "Minimum 6 characters"),
});
```

## Register Form

```jsx
// components/RegisterForm.jsx
"use client";
import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { registerSchema } from "@/schemas/registerSchema";

export default function RegisterForm() {
  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting },
    reset,
  } = useForm({ resolver: zodResolver(registerSchema) });

  async function onSubmit(data) {
    const response = await fetch("/api/register", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(data),
    });
    const result = await response.json();
    alert(result.message);
    reset();
  }

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <div>
        <input type="text"     placeholder="Name"     {...register("name")} />
        {errors.name     && <p>{errors.name.message}</p>}
      </div>
      <div>
        <input type="email"    placeholder="Email"    {...register("email")} />
        {errors.email    && <p>{errors.email.message}</p>}
      </div>
      <div>
        <input type="password" placeholder="Password" {...register("password")} />
        {errors.password && <p>{errors.password.message}</p>}
      </div>
      <button type="submit" disabled={isSubmitting}>
        {isSubmitting ? "Loading..." : "Register"}
      </button>
    </form>
  );
}
```

## RHF Functions

| Function | Purpose |
| --- | --- |
| `register()` | Connect input |
| `handleSubmit()` | Handle submit |
| `errors` | Form errors |
| `reset()` | Reset form |
| `isSubmitting` | Loading state |

## API Route — `safeParse`

```js
// app/api/register/route.js
import { prisma } from "@/lib/prisma";
import { registerSchema } from "@/schemas/registerSchema";

export async function POST(req) {
  const body      = await req.json();
  const validated = registerSchema.safeParse(body);

  if (!validated.success) {
    return Response.json({
      message: "Validation Failed",
      errors:  validated.error.flatten(),
    });
  }

  const user = await prisma.user.create({ data: validated.data });
  return Response.json({ message: "Register Success", data: user });
}
```

> **Always validate AGAIN on the backend** — frontend can be bypassed via Postman, custom scripts, or direct API requests.

## Password Confirm with `.refine()`

```js
export const schema = z.object({
  password:        z.string(),
  confirmPassword: z.string(),
}).refine((data) => data.password === data.confirmPassword, {
  message: "Password not match",
  path:    ["confirmPassword"],
});
```

## Golden Rule

```text
React Hook Form = Form Management
Zod             = Validation
Prisma          = Database ORM
```

---

# 7. Zustand — State Management Complete

> A lightweight global state management library for React and Next.js.

## State Types

| Type | Scope |
| --- | --- |
| Local State | Single Component |
| Global State | Whole Application |

Local state becomes **prop drilling** when many components need the same data — Zustand solves this with a single global store.

## Install

```bash
npm install zustand
```

## Folder Structure

```bash
app/page.jsx
components/{Counter,UserProfile,ThemeToggle}.jsx
store/{counterStore,userStore,themeStore}.js
```

## Counter Store

```js
// store/counterStore.js
import { create } from "zustand";

export const useCounterStore = create((set) => ({
  count: 0,
  increment: () => set((state) => ({ count: state.count + 1 })),
  decrement: () => set((state) => ({ count: state.count - 1 })),
}));
```

## Counter Component

```jsx
// components/Counter.jsx
"use client";
import { useCounterStore } from "@/store/counterStore";

export default function Counter() {
  const { count, increment, decrement } = useCounterStore();
  return (
    <div>
      <h1>{count}</h1>
      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
    </div>
  );
}
```

> Zustand components MUST use `"use client"`.

## User Store

```js
// store/userStore.js
import { create } from "zustand";

export const useUserStore = create((set) => ({
  user: null,
  setUser: (userData) => set({ user: userData }),
  logout: () => set({ user: null }),
}));
```

## Theme Store

```js
// store/themeStore.js
import { create } from "zustand";

export const useThemeStore = create((set) => ({
  darkMode: false,
  toggleTheme: () => set((state) => ({ darkMode: !state.darkMode })),
}));
```

## Persist (LocalStorage)

```js
// store/authStore.js
import { create } from "zustand";
import { persist } from "zustand/middleware";

export const useAuthStore = create(
  persist(
    (set) => ({
      token: null,
      setToken: (newToken) => set({ token: newToken }),
      logout:    ()         => set({ token: null }),
    }),
    { name: "auth-storage" }
  )
);
```

## Selectors (Performance)

```js
// BAD — subscribes to entire store
const store = useCounterStore();

// GOOD — subscribes only to `count`
const count = useCounterStore((state) => state.count);
```

## Async Action

```js
import { create } from "zustand";

export const usePostStore = create((set) => ({
  posts: [],
  getPosts: async () => {
    const response = await fetch("/api/posts");
    const data     = await response.json();
    set({ posts: data });
  },
}));
```

## Zustand vs useState

| useState | Zustand |
| --- | --- |
| Local Component | Global State |
| One Component | Whole App |
| Prop Drilling | No Prop Drilling |

## Best Practices

- Zustand for **global** state only
- useState for local state
- Use selectors for performance
- Keep stores small
- Use `persist` for auth/token

---

# 7.1. Zustand Advanced

## Multi-Store Architecture

```text
Redux       =  One Store + Multiple Slices
Zustand     =  Multiple Small Stores  OR  Combined Slice Store
```

```bash
store/
├── authStore.js
├── cartStore.js
├── themeStore.js
├── userStore.js
├── productStore.js
├── notificationStore.js
└── modalStore.js
```

## Auth Store

```js
import { create } from "zustand";

export const useAuthStore = create((set) => ({
  user:  null,
  token: null,
  login:  (userData, token) => set({ user: userData, token }),
  logout: ()               => set({ user: null, token: null }),
}));
```

## Cart Store

```js
import { create } from "zustand";

export const useCartStore = create((set) => ({
  cartItems: [],
  addToCart: (product) => set((state) => ({
    cartItems: [...state.cartItems, product],
  })),
  clearCart: () => set({ cartItems: [] }),
}));
```

## Combining Stores in One Component

```jsx
"use client";
import { useAuthStore } from "@/store/authStore";
import { useCartStore } from "@/store/cartStore";

export default function Navbar() {
  const user       = useAuthStore((state) => state.user);
  const cartItems  = useCartStore((state) => state.cartItems);

  return (
    <div>
      <h1>{user?.name}</h1>
      <h2>Cart: {cartItems.length}</h2>
    </div>
  );
}
```

## Store Communication

```js
// authStore.js — clear cart on logout
import { useCartStore } from "./cartStore";

export const useAuthStore = create((set) => ({
  logout: () => {
    useCartStore.getState().clearCart();   // call another store's action
    set({ user: null });
  },
}));
```

## Slice Pattern (Advanced)

```js
// store/slices/authSlice.js
export const createAuthSlice = (set) => ({
  user: null,
  login: (user) => set({ user }),
  logout: () => set({ user: null }),
});

// store/slices/cartSlice.js
export const createCartSlice = (set) => ({
  cartItems: [],
  addToCart: (product) => set((state) => ({
    cartItems: [...state.cartItems, product],
  })),
});

// store/store.js
import { create } from "zustand";
import { createAuthSlice } from "./slices/authSlice";
import { createCartSlice } from "./slices/cartSlice";

export const useAppStore = create((...a) => ({
  ...createAuthSlice(...a),
  ...createCartSlice(...a),
}));
```

## Architecture Decision

```text
Feature → Separate Store

Auth    → authStore
Cart    → cartStore
Profile → userStore
```

> Most production apps use **separate feature stores** — simpler than slices, easier to maintain.

---

# 8. Redux — Advanced State Management

> Redux = global state management library. Solves **prop drilling**.

## Architecture

```text
COMPONENT ─ dispatch(action) ─▶ REDUCER ─▶ STORE ─▶ COMPONENTS re-render
```

| Concept | Purpose |
| --- | --- |
| Store | Global state container |
| Slice | Feature state |
| Reducer | Update logic |
| Action | Trigger update |
| `dispatch()` | Send action |
| `useSelector()` | Get state |

## Old Redux vs Redux Toolkit

| Old Redux | Redux Toolkit |
| --- | --- |
| Complex | Simpler |
| More setup | Easy setup |

## Install

```bash
npm install @reduxjs/toolkit react-redux
```

## Project Structure

```bash
app/{layout.jsx,page.jsx}
components/{Counter,UserProfile,Navbar}.jsx
redux/
├── store.js
└── features/{counterSlice,authSlice,cartSlice}.js
```

## Counter Slice

```js
// redux/features/counterSlice.js
import { createSlice } from "@reduxjs/toolkit";

const initialState = { count: 0 };

const counterSlice = createSlice({
  name: "counter",
  initialState,
  reducers: {
    increment: (state) => { state.count += 1; },
    decrement: (state) => { state.count -= 1; },
  },
});

export const { increment, decrement } = counterSlice.actions;
export default counterSlice.reducer;
```

## Store

```js
// redux/store.js
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "./features/counterSlice";
import authReducer    from "./features/authSlice";

export const store = configureStore({
  reducer: { counter: counterReducer, auth: authReducer },
});
```

## Provider

```jsx
// app/providers.jsx
"use client";
import { Provider } from "react-redux";
import { store } from "@/redux/store";

export default function Providers({ children }) {
  return <Provider store={store}>{children}</Provider>;
}

// app/layout.jsx
import Providers from "./providers";

export default function RootLayout({ children }) {
  return (
    <html>
      <body><Providers>{children}</Providers></body>
    </html>
  );
}
```

## Counter Component

```jsx
"use client";
import { useSelector, useDispatch } from "react-redux";
import { increment, decrement } from "@/redux/features/counterSlice";

export default function Counter() {
  const count    = useSelector((state) => state.counter.count);
  const dispatch = useDispatch();

  return (
    <div>
      <h1>{count}</h1>
      <button onClick={() => dispatch(increment())}>+</button>
      <button onClick={() => dispatch(decrement())}>-</button>
    </div>
  );
}
```

## Auth Slice

```js
import { createSlice } from "@reduxjs/toolkit";

const initialState = { user: null, token: null };

const authSlice = createSlice({
  name: "auth",
  initialState,
  reducers: {
    login:  (state, action) => {
      state.user  = action.payload.user;
      state.token = action.payload.token;
    },
    logout: (state) => {
      state.user  = null;
      state.token = null;
    },
  },
});

export const { login, logout } = authSlice.actions;
export default authSlice.reducer;
```

## Async — `createAsyncThunk`

```js
// redux/features/postSlice.js
import { createSlice, createAsyncThunk } from "@reduxjs/toolkit";

export const getPosts = createAsyncThunk(
  "posts/getPosts",
  async () => {
    const response = await fetch("/api/posts");
    return response.json();
  }
);

const postSlice = createSlice({
  name: "posts",
  initialState: { posts: [], loading: false },
  extraReducers: (builder) => {
    builder
      .addCase(getPosts.pending,   (state) => { state.loading = true; })
      .addCase(getPosts.fulfilled, (state, action) => {
        state.loading = false;
        state.posts   = action.payload;
      });
  },
});

export default postSlice.reducer;
```

## Redux vs Zustand

| Redux Toolkit | Zustand |
| --- | --- |
| Structured | Minimal |
| Enterprise | Fast development |
| More boilerplate | Very simple |
| Better for huge teams | Small/medium apps |

## Best Practices

- One slice per feature
- Keep reducers pure
- Use Redux Toolkit (not old Redux)
- Don't store everything in Redux
- Use selectors for performance

---

# 8.1. Redux Thunk

> Redux Thunk = middleware that allows async operations inside Redux. **Redux Toolkit already includes Thunk** — no extra install needed.

## Why Thunk?

Reducers MUST be **pure functions**. They cannot call APIs.

```js
// ❌ WRONG — reducers can't be async
reducers: {
  getPosts: async (state) => {
    const response = await fetch("/api/posts");
  }
}
```

## Async Thunk Flow

```text
Component
    ▼
dispatch(asyncThunk)
    ▼
Thunk Middleware
    ▼
API Request
    ▼
pending / fulfilled / rejected
    ▼
Reducer Update
    ▼
Store Update
```

## Full Example — Post Slice

```js
import { createSlice, createAsyncThunk } from "@reduxjs/toolkit";

export const getPosts = createAsyncThunk(
  "posts/getPosts",
  async () => {
    const response = await fetch("https://jsonplaceholder.typicode.com/posts");
    return response.json();
  }
);

const initialState = { posts: [], loading: false, error: null };

const postSlice = createSlice({
  name: "posts",
  initialState,
  reducers: {},
  extraReducers: (builder) => {
    builder
      .addCase(getPosts.pending, (state) => {
        state.loading = true;
        state.error   = null;
      })
      .addCase(getPosts.fulfilled, (state, action) => {
        state.loading = false;
        state.posts   = action.payload;
      })
      .addCase(getPosts.rejected, (state, action) => {
        state.loading = false;
        state.error   = action.error.message;
      });
  },
});

export default postSlice.reducer;
```

## Thunk States

| State | Meaning |
| --- | --- |
| `pending` | Loading |
| `fulfilled` | Success |
| `rejected` | Failed |

## PostList Component

```jsx
"use client";
import { useSelector, useDispatch } from "react-redux";
import { useEffect } from "react";
import { getPosts } from "@/redux/features/postSlice";

export default function PostList() {
  const dispatch = useDispatch();
  const { posts, loading, error } = useSelector((state) => state.posts);

  useEffect(() => { dispatch(getPosts()); }, [dispatch]);

  if (loading) return <h1>Loading...</h1>;
  if (error)   return <h1>{error}</h1>;

  return (
    <div>
      {posts.map((post) => <h1 key={post.id}>{post.title}</h1>)}
    </div>
  );
}
```

## Login Async Thunk

```js
export const loginUser = createAsyncThunk(
  "auth/login",
  async (formData) => {
    const response = await fetch("/api/login", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(formData),
    });
    return response.json();
  }
);
```

## Golden Rule

```text
Reducers = State Update Logic (synchronous)
Thunk    = Async API Logic
```

---

# 9. SWR & ISR

| Aspect | SWR | ISR |
| --- | --- | --- |
| Side | Client | Server |
| Best For | Dynamic user data | SEO-critical public pages |
| Auto revalidate | Yes | Yes (after `revalidate` seconds) |

## SWR — Client Side

```bash
npm install swr
```

```js
// lib/fetcher.js
export async function fetcher(url) {
  const response = await fetch(url);
  return response.json();
}
```

```jsx
// components/PostList.jsx
"use client";
import useSWR from "swr";
import { fetcher } from "@/lib/fetcher";

export default function PostList() {
  const { data, error, isLoading } = useSWR("/api/posts", fetcher);

  if (isLoading) return <h1>Loading...</h1>;
  if (error)     return <h1>Error...</h1>;

  return (
    <div>
      {data.map((post) => <h1 key={post.id}>{post.title}</h1>)}
    </div>
  );
}
```

SWR = **Stale While Revalidate** — show cached data first, then fetch fresh.

### SWR Mutation

```jsx
import useSWR, { mutate } from "swr";

async function addPost() {
  await fetch("/api/posts", { method: "POST" });
  mutate("/api/posts");            // refresh cache
}
```

### SWR Auto Revalidation Triggers

- Browser refocus
- Internet reconnect
- Reopen tab

## ISR — Server Side

```jsx
// app/posts/page.jsx
export const revalidate = 60;     // re-generate every 60 seconds

export default async function PostsPage() {
  const response = await fetch("https://jsonplaceholder.typicode.com/posts");
  const posts    = await response.json();

  return (
    <div>
      {posts.map((post) => <h1 key={post.id}>{post.title}</h1>)}
    </div>
  );
}
```

| Use ISR for | Avoid ISR for |
| --- | --- |
| Blog · News · Product Page · Marketing · Docs | Authenticated dashboards (use SWR) |

---

# 9.1. ISR + SWR Combined

The modern pattern: **ISR for fast SEO static content** + **SWR for live dynamic client data**.

## Why Combine?

| Benefit | Source |
| --- | --- |
| Fast First Load | ISR |
| SEO Friendly | ISR |
| Live Updates | SWR |
| Lower Server Cost | ISR |
| Better UX | SWR |

## Full Combined Example

### Step 1 — ISR Page

```jsx
// app/posts/page.jsx
import Comments from "@/components/Comments";

export const revalidate = 60;

export default async function PostsPage() {
  const response = await fetch("https://jsonplaceholder.typicode.com/posts");
  const posts    = await response.json();

  return (
    <div>
      <h1>ISR POSTS</h1>
      {posts.slice(0, 5).map((post) => (
        <div key={post.id}><h2>{post.title}</h2></div>
      ))}
      <Comments />     {/* SWR client component */}
    </div>
  );
}
```

### Step 2 — SWR Client Component

```jsx
// components/Comments.jsx
"use client";
import useSWR from "swr";

const fetcher = (url) => fetch(url).then((res) => res.json());

export default function Comments() {
  const { data, isLoading, error } = useSWR(
    "https://jsonplaceholder.typicode.com/comments",
    fetcher
  );

  if (isLoading) return <h1>Loading...</h1>;
  if (error)     return <h1>Error...</h1>;

  return (
    <div>
      <h1>LIVE COMMENTS</h1>
      {data.slice(0, 5).map((comment) => (
        <p key={comment.id}>{comment.name}</p>
      ))}
    </div>
  );
}
```

## Combined Flow

```text
User Open Page
        ▼
ISR Static HTML Instantly Loaded
        ▼
SEO Optimized Content Visible
        ▼
SWR Starts Client Fetching
        ▼
Fresh Dynamic Data Loaded
        ▼
UI Updates Automatically
```

## Real-World Use

| Project | Static (ISR) | Live (SWR) |
| --- | --- | --- |
| Ecommerce | Product Details | Stock Quantity |
| Blog | Article Content | Comments |
| News | Cached News | Live Reactions |
| Dashboard | Static Layout | Live Data |

---

# 10. Try / Catch / Finally + Error Logs

## Basic Try-Catch-Finally

```js
try {
  const data   = await fetch("/api/users");
  const result = await data.json();
} catch (error) {
  console.error("Error occurred:", error);
} finally {
  console.log("Always runs");
}
```

| Block | Purpose |
| --- | --- |
| `try` | Main logic |
| `catch` | Handle error safely |
| `finally` | Always executes |

## Error Handling in API Routes

```js
export async function GET() {
  try {
    const users = await prisma.user.findMany();
    return Response.json({ success: true, users });
  } catch (error) {
    console.error("API Error:", error);
    return Response.json(
      { success: false, message: "Internal Server Error" },
      { status: 500 }
    );
  }
}
```

## Server Action

```js
"use server";

export async function createUser(formData) {
  try {
    const name = formData.get("name");
    if (!name) throw new Error("Name is required");
    await prisma.user.create({ data: { name } });
  } catch (error) {
    console.error("Server Action Error:", error);
    throw new Error("Failed to create user");
  }
}
```

## Global Error UI (`error.js`)

```js
"use client";

export default function Error({ error, reset }) {
  console.error(error);
  return (
    <div>
      <h2>Something went wrong!</h2>
      <button onClick={() => reset()}>Retry</button>
    </div>
  );
}
```

## 404 Page (`not-found.js`)

```js
export default function NotFound() {
  return <h1>404 - Page Not Found</h1>;
}
```

## File-Based Logger

```js
// lib/logger.js
import fs from "fs";
import path from "path";

function writeLog(file, data) {
  const filePath = path.join(process.cwd(), "logs", file);
  fs.appendFileSync(filePath, data + "\n");
}

export function logError(error)   { writeLog("error.log", `[ERROR] ${error.message}`); }
export function logAuth(message)  { writeLog("auth.log",  `[AUTH]  ${message}`); }
export function logDB(message)    { writeLog("db.log",    `[DB]    ${message}`); }
```

```bash
logs/
 ├── error.log
 ├── auth.log
 ├── api.log
 └── db.log
```

## API Logging Example

```js
import { logError, logDB } from "@/lib/logger";

export async function GET() {
  try {
    logDB("Fetching users from database");
    const users = await prisma.user.findMany();
    return Response.json(users);
  } catch (error) {
    logError(error);
    return Response.json({ error: "Failed" }, { status: 500 });
  }
}
```

## Logging Levels

| Level | Use |
| --- | --- |
| INFO | Normal flow |
| WARN | Potential issue |
| ERROR | Failure |
| DEBUG | Development only |

## Production Tip

For real production: use **Winston**, **Pino**, **Datadog** or **Sentry**instead of plain files.

## Golden Rules

- Always wrap API logic in try-catch
- Never expose raw errors to client
- Log full error server-side only
- Separate logs by domain (auth/db/api)
- Use structured logs in production
- Keep error messages user-friendly

---

# 11. Caching with Redis

> Caching saves expensive DB / API results in a fast in-memory store.

## Flow

```text
User Request
        ▼
Check Redis
        ▼
Cache Hit → return Redis data
        ▼
Cache Miss → query DB → save to Redis (TTL) → return
```

## Install

```bash
npm install ioredis
```

## Redis Client

```js
// lib/redis.js
import Redis from "ioredis";

const redis = new Redis(process.env.REDIS_URL || "redis://localhost:6379");

export { redis };
```

## Cache Wrapper

```js
// app/actions/cacheActions.js
import { redis } from "@/lib/redis";
import { prisma } from "@/lib/prisma";

export async function getCachedUserData(userId) {
  const cacheKey = `user:${userId}`;

  try {
    const cachedData = await redis.get(cacheKey);
    if (cachedData) return { source: "redis", data: JSON.parse(cachedData) };

    const user = await prisma.user.findUnique({ where: { id: userId } });
    if (!user) return { success: false, message: "Not found" };

    await redis.set(cacheKey, JSON.stringify(user), "EX", 600);
    return { source: "database", data: user };

  } catch (error) {
    const backupUser = await prisma.user.findUnique({ where: { id: userId } });
    return { source: "database_fallback", data: backupUser };
  }
}
```

## Cache Invalidation

```js
// app/actions/userActions.js
import { redis } from "@/lib/redis";
import { prisma } from "@/lib/prisma";

export async function updateUserProfile(userId, newData) {
  const updatedUser = await prisma.user.update({
    where: { id: userId },
    data:  newData,
  });

  await redis.del(`user:${userId}`);          // clear stale cache
  return { success: true, updatedUser };
}
```

## Redis Quick Reference

| Action | Command | Use case |
| --- | --- | --- |
| Read cache | `redis.get(key)` | Dashboard user objects |
| Write cache | `redis.set(key, val, 'EX', sec)` | Result charts for 1h |
| Delete cache | `redis.del(key)` | Drop stale data after update |
| Flush all | `redis.flushall()` | Full cache wipe on deploy |

## Critical Rules

```js
// ❌ WRONG — Redis stores strings
await redis.set("profile", userObj);

// ✅ RIGHT — serialize
await redis.set("profile", JSON.stringify(userObj));
```

- Always wrap Redis calls in `try/catch` and fall back to the primary DB.

---

# 12. Observer — DB Observer (Prisma `$extends`)

> An observer listens for specific DB actions and automatically runs code **before** (pre-event) or **after** (post-event) the database call.

## Lifecycle

```text
Prisma Action Triggered
   ▼
PRE-DB EVENT   (hash password, lowercase email)
   ▼
Database Execution
   ▼
POST-DB EVENT  (send welcome email, clear Redis)
   ▼
Return Result to App
```

## Observer Instance (Prisma Extension)

```js
// lib/prisma.js
import { PrismaClient } from "@prisma/client";

const globalPrisma = new PrismaClient();

const prismaWithObservers = globalPrisma.$extends({
  query: {
    user: {
      async create({ args, query }) {
        // PRE-EVENT — transform email
        if (args.data.email) {
          args.data.email = args.data.email.toLowerCase();
        }

        const user = await query(args);     // run the actual query

        // POST-EVENT — side effect
        await triggerPostUserCreate(user);

        return user;
      },

      async update({ args, query }) {
        const user = await query(args);
        console.log(`[Observer] User ${user.id} updated. Invalidating cache...`);
        return user;
      },
    },
  },
});

async function triggerPostUserCreate(user) {
  console.log(`[Observer] User created with ID: ${user.id}. Sending welcome email...`);
}

export const prisma = prismaWithObservers;
```

## Triggering the Observer

The observer runs **silently** in the background. You don't call it.

```js
// app/actions/userActions.js
import { prisma } from "@/lib/prisma";

export async function registerUser(data) {
  try {
    const newUser = await prisma.user.create({
      data: { name: data.name, email: data.EMAIL_UPPERCASE, status: "pending" },
      // `email` will be lowercased by the PRE-event
    });
    return { success: true, user: newUser };
  } catch (error) {
    return { success: false, error: error.message };
  }
}
```

## Laravel ↔ Next.js Mapping

| Laravel Observer | Next.js Lifecycle Hook | Type |
| --- | --- | --- |
| `creating()`/`updating()` | before `await query(args)` | Pre-Event |
| `created()`/`updated()` | after `await query(args)` | Post-Event |
| `deleting()` | before `await query(args)` | Pre-Event |
| `deleted()` | after `await query(args)` | Post-Event |

## Critical Rules

```js
// ❌ WRONG — missing return
async create({ args, query }) {
  await query(args);
}

// ✅ RIGHT
async create({ args, query }) {
  const result = await query(args);
  return result;
}
```

- Keep post-events **non-blocking** when possible — fire-and-forget for slow side effects like external emails.

---

# 12.1. Event-Driven / Pub-Sub with Emitter — Real Code

> One action triggers multiple independent reactions — the **observer pattern** in Next.js via Node's built-in `EventEmitter`.

## Project Structure

```bash
project/
├── lib/eventBus.js
├── events/userEvents.js
├── services/userService.js
├── events/listeners/{emailListener,logListener,analyticsListener}.js
└── app/api/user/route.js
```

## Event Bus

```js
// lib/eventBus.js
import { EventEmitter } from "events";

export const eventBus = new EventEmitter();
```

## Event Constants

```js
// events/userEvents.js
export const USER_CREATED = "user.created";
export const USER_DELETED = "user.deleted";
```

## Publisher (Service)

```js
// services/userService.js
import { eventBus } from "../lib/eventBus.js";
import { USER_CREATED } from "../events/userEvents.js";

export async function createUser(user) {
  const savedUser = { id: Date.now(), ...user };
  console.log("User saved in DB");

  eventBus.emit(USER_CREATED, savedUser);   // publish
  return savedUser;
}
```

## Listeners

```js
// events/listeners/emailListener.js
import { eventBus } from "../../lib/eventBus.js";
import { USER_CREATED } from "../userEvents.js";

eventBus.on(USER_CREATED, (user) => {
  console.log("EMAIL Listener Triggered");
  sendWelcomeEmail(user.email);
});

function sendWelcomeEmail(email) {
  console.log("Sending email to:", email);
}
```

```js
// events/listeners/logListener.js
import { eventBus } from "../../lib/eventBus.js";
import { USER_CREATED } from "../userEvents.js";

eventBus.on(USER_CREATED, (user) => {
  console.log("LOG Listener Triggered");
  console.log("User Created:", user.id);
});
```

```js
// events/listeners/analyticsListener.js
import { eventBus } from "../../lib/eventBus.js";
import { USER_CREATED } from "../userEvents.js";

eventBus.on(USER_CREATED, (user) => {
  console.log("ANALYTICS Listener Triggered");
  console.log("Tracking user:", user.id);
});
```

## API Route (Trigger)

```js
// app/api/user/route.js
import { createUser } from "../../../services/userService.js";

export async function POST(req) {
  const body = await req.json();
  const user = await createUser(body);
  return Response.json(user);
}
```

## Pub/Sub Mental Model

```text
Publisher  =  triggers event
Subscriber =  reacts to event
EventBus   =  communication layer
```

```text
API Request
    ▼
Service Layer
    ▼
Event Emitted (user.created)
    ▼
Event Bus (Pub/Sub)
    ├── Email
    ├── Log
    └── Analytics
```

## Important Limitation

```text
EventEmitter is NOT persistent.
If server restarts → all events are lost.
```

For production: **Redis Pub/Sub → Kafka**.

---

# 13. Event-Driven / Pub-Sub with EventEmitter

> Same idea as 12.1, but more conceptual — the canonical reference.

## Pub/Sub Flow

```text
Publisher (emit event)
        ▼
     Event Bus
        ▼
 ┌──────┼────────┐
 ▼      ▼        ▼
Listener Listener Listener
```

## Why Use Event Systems?

✔ Decouple logic · ✔ Avoid spaghetti code · ✔ Scale background features · ✔ Easy feature extension

## Core Tool

```js
import { EventEmitter } from "events";   // built-in Node.js, no install
```

## Multiple Events

```js
eventBus.emit("order.created",   order);
eventBus.emit("payment.success", payment);
eventBus.emit("user.deleted",    user);
```

## Multiple Listeners for Same Event

```js
eventBus.on("order.created", sendInvoice);
eventBus.on("order.created", updateInventory);
eventBus.on("order.created", notifyAdmin);
```

## Async Handlers

```js
eventBus.on("user.created", async (user) => {
  await sendEmail(user.email);
});
```

## When NOT to Use EventEmitter

❌ Critical financial transactions ❌ Required persistence workflows ❌ Multi-server systems without Redis

## When to Use EventEmitter

✔ Notifications · ✔ Logging · ✔ Analytics · ✔ Internal decoupling

## Best Practice Architecture

```text
API
 ▼
Service Layer
 ▼
Emit Event
 ▼
Event Bus
 ├── Email
 ├── Logger
 ├── Analytics
 └── Notifications
```

---

# 14. Jobs & Queue

> Run heavy tasks **in the background**, outside the request lifecycle.

## Common Job Types

- Send Email / SMS
- Image processing / PDF generation
- Payment logging
- AI tasks
- Data sync with external APIs

## Why a Queue?

```text
Without queue: User request → wait → slow response → bad UX
With queue:    User request → instant response → job runs in background
```

## Architecture

```text
API Request
     ▼
Add Job to Queue
     ▼
Redis (Job Storage)
     ▼
Worker Process
     ▼
Execute Job (Email, SMS, etc.)
```

## Tools

1. **Redis** — message broker
2. **BullMQ** — queue library
3. **Node Worker** — job processor

## Install

```bash
npm install bullmq ioredis
```

## Redis Connection

```js
// lib/redis.js
import IORedis from "ioredis";

export const connection = new IORedis({ maxRetriesPerRequest: null });
```

## Queue

```js
// lib/queue.js
import { Queue } from "bullmq";
import { connection } from "./redis.js";

export const emailQueue = new Queue("emailQueue", { connection });
```

## Producer (Add Job)

```js
// services/emailService.js
import { emailQueue } from "../lib/queue.js";

export async function sendWelcomeEmailJob(user) {
  await emailQueue.add("sendWelcomeEmail", {
    email: user.email,
    name:  user.name,
  });
  console.log("Job added to queue");
}
```

## API Route

```js
// app/api/register/route.js
import { sendWelcomeEmailJob } from "../../../services/emailService.js";

export async function POST(req) {
  const body = await req.json();
  const user = { name: body.name, email: body.email };
  await sendWelcomeEmailJob(user);

  return Response.json({
    message: "User registered, email will be sent",
  });
}
```

## Worker (Processor)

```js
// worker/emailWorker.js
import { Worker } from "bullmq";
import { connection } from "../lib/redis.js";

const worker = new Worker(
  "emailQueue",
  async (job) => {
    if (job.name === "sendWelcomeEmail") {
      const { email, name } = job.data;
      console.log("Processing email job...");
      await sendEmail(email, name);
    }
  },
  { connection }
);

async function sendEmail(email, name) {
  console.log("Sending email to:", email);
  await new Promise((res) => setTimeout(res, 2000));
  console.log(`Email sent to ${name} <${email}>`);
}
```

## Job Types

| Job name | Purpose |
| --- | --- |
| `sendWelcomeEmail` | Welcome email |
| `sendOTP` | SMS / email OTP |
| `resizeImage` | Image processing |
| `generateInvoice` | PDF generation |

## Retry System

```js
await emailQueue.add("sendWelcomeEmail", data, {
  attempts: 3,
  backoff:  { type: "exponential", delay: 5000 },
});
```

## Job Statuses

```text
waiting   → in queue
active    → being processed
completed → finished
failed    → error occurred
```

## Why Redis?

✔ Fast in-memory storage · ✔ Handles high traffic jobs · ✔ Supports distributed workers.

## Production Best Practices

✔ Never send email inside API directly ✔ Always push heavy work to queue ✔ Run worker **separately** from Next.js ✔ Use retry + failure handling ✔ Keep queue jobs small and atomic

---

# 15. Advanced — Pub/Sub + Jobs + Redis + EventEmitter + BullMQ

> A **complete production observer architecture** combining everything from notes 12, 13, 14.

## Full System Design

```text
            ┌──────────────┐
            │   Client     │
            └──────┬───────┘
                   ▼
        ┌────────────────────┐
        │  API / Server Act. │
        └────────┬───────────┘
                 ▼
        ┌────────────────────┐
        │  Service Layer     │
        └────────┬───────────┘
                 ▼
     ┌───────────┼────────────┐
     ▼           ▼            ▼
 Prisma DB   Event Bus    Logger
                 │
                 ▼
           Redis Queue
                 │
                 ▼
            Worker Jobs
                 │
        ┌────────┴────────┐
        ▼                 ▼
   Email Service     Background Tasks
```

## Install

```bash
npm install @prisma/client prisma ioredis bullmq
```

## Prisma

```js
// lib/prisma.js
import { PrismaClient } from "@prisma/client";
export const prisma = new PrismaClient();
```

## Event Bus

```js
// lib/eventBus.js
import { EventEmitter } from "events";
export const eventBus = new EventEmitter();
```

## Redis Queue (BullMQ)

```js
// lib/queue.js
import { Queue } from "bullmq";
import IORedis from "ioredis";

const connection = new IORedis();

export const emailQueue = new Queue("emailQueue", { connection });
```

## Service Layer (Business Logic)

```js
// services/userService.js
import { prisma } from "../lib/prisma.js";
import { eventBus } from "../lib/eventBus.js";

export async function createUser(data) {
  const user = await prisma.user.create({ data });
  console.log("User created in DB");

  eventBus.emit("user.created", user);     // publish event
  return user;
}
```

## API Route (Entry Point)

```js
// app/api/user/route.js
import { createUser } from "../../../services/userService.js";

export async function POST(req) {
  const body = await req.json();
  const user = await createUser(body);
  return Response.json(user);
}
```

## Observer Listener → Enqueue Job (Non-Blocking)

```js
// observers/userObserver.js
import { eventBus } from "../lib/eventBus.js";
import { emailQueue } from "../lib/queue.js";

eventBus.on("user.created", async (user) => {
  console.log("Observer triggered for user:", user.id);

  // Push to queue — DO NOT block request
  await emailQueue.add("sendWelcomeEmail", {
    email: user.email,
    name:  user.name,
  });
});
```

## Worker (Background Processing)

```js
// worker/emailWorker.js
import { Worker } from "bullmq";
import IORedis from "ioredis";

const connection = new IORedis();

const worker = new Worker(
  "emailQueue",
  async (job) => {
    if (job.name === "sendWelcomeEmail") {
      const { email, name } = job.data;
      console.log("Sending email to:", email);
      await sendEmail(email, name);
    }
  },
  { connection }
);

async function sendEmail(email, name) {
  console.log(`Email sent to ${name} <${email}>`);
}
```

## Logger Side-Effect

```js
// lib/logger.js
export function logEvent(message, data) {
  console.log("[LOG]", message, data);
}

// Attach to observer
import { eventBus } from "../lib/eventBus.js";
import { logEvent } from "../lib/logger.js";

eventBus.on("user.created", (user) => {
  logEvent("USER_CREATED", user);
});
```

## Full Observer Flow

```text
User Request
    ▼
API Route
    ▼
Service Layer
    ├── Save to DB (Prisma)
    ├── Emit Event
    ▼
Event Bus (Observer Layer)
    ├── Logger
    ├── Queue Job (Redis)
    ▼
Worker
    ├── Send Email
    └── Background Tasks
```

## Laravel ↔ Next.js Equivalents

| Laravel | Next.js Equivalent |
| --- | --- |
| Observer | EventEmitter |
| Jobs | BullMQ Queue |
| Queue Worker | Node Worker |
| Model Event | Service Layer Trigger |
| Listener | `eventBus.on()` |

## When to Use What

| Tool | Best for |
| --- | --- |
| Service Layer | Main business logic |
| EventEmitter | Internal decoupled communication |
| Queue (BullMQ) | Heavy async tasks (email, SMS, processing) |
| Worker | Background execution engine |

## Interview Answer

> Next.js doesn't have a built-in Observer like Laravel; we implement it using **EventEmitter + Service Layer + Queue-based workers**.

---

# 16. Testing — AAA Pattern (Jest + Testing Library)

## AAA = Arrange → Act → Assert

```text
ARRANGE  Setup Data
    ▼
ACT     Run Function / Click Button
    ▼
ASSERT  Check Expected Result
```

## Test Types

| Type | Purpose |
| --- | --- |
| Unit Test | Single function |
| Feature Test | Full feature |
| View Test | React component UI |
| Integration Test | Multiple systems together |
| E2E Test | Full browser test |

## Libraries

| Library | Purpose |
| --- | --- |
| Jest | Test runner |
| Testing Library | React UI |
| jest-environment-jsdom | Browser environment |

## Install

```bash
npm install --save-dev jest jest-environment-jsdom \
  @testing-library/react @testing-library/jest-dom @testing-library/user-event
```

## Project Structure

```bash
next-testing-app/
├── app/
├── components/{Counter,LoginForm,UserCard}.jsx
├── lib/math.js
├── __tests__/
│   ├── unit/math.test.js
│   ├── view/{Counter,UserCard}.test.jsx
│   └── feature/{LoginForm,api}.test.jsx
├── jest.config.js
└── jest.setup.js
```

## Jest Config

```js
// jest.config.js
const nextJest = require("next/jest");
const createJestConfig = nextJest({ dir: "./" });

const customJestConfig = {
  testEnvironment: "jsdom",
  setupFilesAfterEach: ["<rootDir>/jest.setup.js"],
  moduleNameMapper: { "^@/(.*)$": "<rootDir>/$1" },
};

module.exports = createJestConfig(customJestConfig);
```

```js
// jest.setup.js
import "@testing-library/jest-dom";
```

```json
// package.json
{
  "scripts": {
    "test":        "jest",
    "test:watch":  "jest --watch"
  }
}
```

## Unit Test

```js
// lib/math.js
export function add(a, b)      { return a + b; }
export function multiply(a, b) { return a * b; }
```

```js
// __tests__/unit/math.test.js
import { add, multiply } from "@/lib/math";

describe("Math Functions", () => {
  test("should add two numbers", () => {
    // ARRANGE
    const a = 5, b = 10;
    // ACT
    const result = add(a, b);
    // ASSERT
    expect(result).toBe(15);
  });

  test("should multiply numbers", () => {
    const a = 2, b = 4;
    const result = multiply(a, b);
    expect(result).toBe(8);
  });
});
```

## Common Assertions

```js
expect(5).toBe(5);
expect([1, 2]).toEqual([1, 2]);
expect(true).toBeTruthy();
expect(false).toBeFalsy();
expect(user).toHaveProperty("name");
```

## View Test

```jsx
// components/Counter.jsx
"use client";
import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

```jsx
// __tests__/view/Counter.test.jsx
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import Counter from "@/components/Counter";

describe("Counter Component", () => {
  test("should increment count", async () => {
    // ARRANGE
    render(<Counter />);
    const button = screen.getByText("Increment");

    // ACT
    await userEvent.click(button);

    // ASSERT
    expect(screen.getByText("Count: 1")).toBeInTheDocument();
  });
});
```

## Feature Test

```jsx
// __tests__/feature/LoginForm.test.jsx
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import LoginForm from "@/components/LoginForm";

describe("Login Feature", () => {
  test("should show success message", async () => {
    render(<LoginForm />);
    const button = screen.getByText("Login");

    await userEvent.click(button);

    expect(screen.getByText("Login Success")).toBeInTheDocument();
  });
});
```

## API Feature Test

```js
// __tests__/feature/api.test.js
import { GET } from "@/app/api/users/route";

describe("Users API", () => {
  test("should return users", async () => {
    const response = await GET();
    const data     = await response.json();

    expect(data.success).toBe(true);
    expect(data.users.length).toBe(1);
  });
});
```

## Mock Function

```js
const mockFunction = jest.fn();
mockFunction();
expect(mockFunction).toHaveBeenCalled();

global.fetch = jest.fn(() =>
  Promise.resolve({ json: () => Promise.resolve({ success: true }) })
);

beforeEach(() => { jest.clearAllMocks(); });
```

## Async Test

```js
test("async example", async () => {
  const result = await Promise.resolve(10);
  expect(result).toBe(10);
});
```

## Red-Green-Refactor

```text
RED    fail test
  ▼
GREEN  pass test
  ▼
REFACTOR improve code
```

## Common Errors

| Error | Solution |
| --- | --- |
| `document is not defined` | Use jsdom |
| Cannot use import | Configure Jest |
| Module not found | Check alias |
| Test timeout | Use async/await |

## Golden Rules

- Test **behavior**, not implementation
- Use AAA pattern
- One test, one purpose
- Keep tests simple
- Mock external APIs

---

# Summary — Concepts at a Glance

| \# | Topic | Key Take-aways |
| --- | --- | --- |
| 0 | Folder Structure | Folders = routes, `page.js` = UI |
| 1 | Layout — Header/Body/Footer | Nested layouts via `{children}` |
| 1.1 | Page-wise Layout | Conditional UI per page (anti-pattern) |
| 1.2 | Route Groups | `(group)` folders with separate layout trees |
| 2 | Route Params | `[param]` folders + `params` prop |
| 3.0 | Basic Routes | `params`, `searchParams`, `<Link>` |
| 3.1 | Search Params | Query string from URL |
| 4 | Prisma ORM | Schema, CRUD, relations, raw SQL |
| 4.0 | Transactions | Auto (`prisma.$transaction`) vs Manual (`pg`) |
| 4.1 | SSR + CSR + Prisma | Server-fetched data + client buttons + API routes |
| 5 | Middleware | `middleware.js` for auth/role/rate-limit |
| 5.1 | Full-stack CRUD + Middleware | End-to-end SSR+CSR+Middleware+Auth+Logout |
| 6 | Form Validation | Manual `useState` validation, server-side re-validation |
| 6.1 | Zod + React Hook Form | Schema-based, `safeParse`, `.refine()` |
| 7 | Zustand Basics | `create()`, `set()`, persist, selectors |
| 7.1 | Zustand Multi-store | Feature stores, communication, slice pattern |
| 8 | Redux Toolkit | Slice + configureStore + Provider + dispatch/useSelector |
| 8.1 | Redux Thunk | `createAsyncThunk` → pending/fulfilled/rejected |
| 9 | SWR + ISR | Client cache vs static regeneration |
| 9.1 | ISR + SWR Combined | ISR for SEO, SWR for live updates |
| 10 | Try/Catch/Finally + Logging | API + Server Action + `error.js` + file-based logs |
| 11 | Redis Caching | `ioredis`, `EX` TTL, `del` invalidation, fallback to DB |
| 12 | Prisma Observer | `$extends` for pre/post DB events |
| 12.1 | EventEmitter Pub/Sub | `eventBus.emit/on`, listener modules |
| 13 | Pub/Sub Concept | Publisher → EventBus → Subscribers |
| 14 | Jobs + Queue | BullMQ + Redis + Worker, retry, exponential backoff |
| 15 | Combined Observer Architecture | Service + EventBus + Redis Queue + Worker |
| 16 | Testing (AAA) | Jest + Testing Library, mocks, feature/E2E tests |

Happy hacking! ⚡🚀
