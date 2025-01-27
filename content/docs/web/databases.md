+++
date = '2025-01-25T10:55:07-08:00'
draft = false
title = 'Databases'
weight = 3
+++

# Databases

Most modern web applications often require a database to store and manage data. This guide will lead you through setting up a database for a Next.js project, using hosted database services, and performing basic CRUD (Create, Read, Update, Delete) operations with Prisma, a popular ORM (Object Relational Mapper).

---

## Choosing a Database
### SQL (PostgreSQL via Supabase)
- Choose when you need: Data relationships, ACID compliance, complex queries
- Free tier available, excellent documentation
- Built-in row-level security and authentication

### NoSQL (MongoDB Atlas)
- Choose when you need: Flexible schema, high write throughput, horizontal scaling
- Free tier available, great for prototypes
- Native JSON support

## Setup Guide for Hosted Databases
### PostgreSQL via Supabase
1. Sign up [here](https://supabase.com)
2. Create project
3. Get connection string from: Settings -> Database

### MongoDB Atlas
1. Sign up [here](https://mongodb.com/atlas)
2. Create cluster (M0 Free tier)
3. Get connection string from: Connect -> Connect your application

---

## Adding Prisma to Your Next.js Project

Prisma makes working with databases in Next.js efficient and type-safe. Follow these steps:

Install Prisma by running the following commands in your project:
```bash
npm install prisma --save-dev
npm install @prisma/client
```

Initialize Prisma
```bash
npx prisma init
```
This creates a `prisma/` directory with a `schema.prisma` file.

Update the `schema.prisma` file by replacing the `datasource` block with your connection string. For example:
```
datasource db {
  provider = "postgresql"  // Change to "mongodb" for MongoDB
  url      = env("DATABASE_URL")
}
```

Add a simple model:
```
model Post {
  id        Int      @id @default(autoincrement())
  title     String
  content   String
  createdAt DateTime @default(now())
}
```
Move the model to your database:
```bash
npx prisma migrate dev --name description_of_changes
```
or for quick prototyping and no version control:
```bash
npx prisma db push 
```
This creates the `Post` table in your database.

---

## CRUD Operations in Next.js

Here’s how to perform basic CRUD operations using Prisma in API routes:

#### **a. Create a Post**
Create a new file `app/api/posts/create.js`:
```javascript
import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();

export default async function handler(req, res) {
  if (req.method === "POST") {
    const { title, content } = req.body;
    const post = await prisma.post.create({
      data: {
        title,
        content,
      },
    });
    res.status(200).json(post);
  } else {
    res.status(405).json({ message: "Method not allowed" });
  }
}
```

#### **b. Read Posts**
Create a new file `app/api/posts/index.js`:
```javascript
import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();

export default async function handler(req, res) {
  if (req.method === "GET") {
    const posts = await prisma.post.findMany();
    res.status(200).json(posts);
  } else {
    res.status(405).json({ message: "Method not allowed" });
  }
}
```

#### **c. Update a Post**
Create a new file `app/api/posts/update.js`:
```javascript
import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();

export default async function handler(req, res) {
  if (req.method === "PUT") {
    const { id, title, content } = req.body;
    const post = await prisma.post.update({
      where: { id: Number(id) },
      data: { title, content },
    });
    res.status(200).json(post);
  } else {
    res.status(405).json({ message: "Method not allowed" });
  }
}
```

#### **d. Delete a Post**
Create a new file `app/api/posts/delete.js`:
```javascript
import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();

export default async function handler(req, res) {
  if (req.method === "DELETE") {
    const { id } = req.body;
    await prisma.post.delete({
      where: { id: Number(id) },
    });
    res.status(200).json({ message: "Post deleted" });
  } else {
    res.status(405).json({ message: "Method not allowed" });
  }
}
```

You have now created RESTful API Endpoints for your database operations!

---

## Environment Variables
Store your database connection string securely in a `.env` file:
```env
DATABASE_URL=your-database-connection-string
```
Ensure `.env` is added to your `.gitignore` to prevent it from being committed.
___
## Performance Tips
- Add indexes for frequently queried fields
- Use `select` to limit returned fields
- Consider caching for read-heavy operations