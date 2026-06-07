# Prisma + PostgreSQL Setup Guide

## Prerequisites

Install the required dependencies:

### Development Dependencies

```bash
npm install prisma @types/pg --save-dev
```

or

```bash
npm install prisma @types/pg -D
```

### Runtime Dependencies

```bash
npm install @prisma/client @prisma/adapter-pg dotenv
```

---

## Initialize Prisma

Run:

```bash
npx prisma init
```

This will create:

```text
prisma/
└── schema.prisma

.env
```

---

## Configure Environment Variables

Update the `.env` file with your PostgreSQL connection string:

```env
DATABASE_URL="postgresql://username:password@localhost:5432/database_name"
```

Replace:

* `username` with your PostgreSQL username
* `password` with your PostgreSQL password
* `database_name` with your database name

---

## Update the Prisma Generator

Open `prisma/schema.prisma`.

If you see something like:

```prisma
generator client {
  provider = "prisma-client"
  output   = "../generated/prisma"
}
```

Remove the `output` field and change the provider to:

```prisma
generator client {
  provider = "prisma-client-js"
}
```

---

## Create Your Models

Example:

```prisma
model Student {
  id   Int    @id @default(autoincrement())
  Name String
  Roll String
}
```

Add your own models as needed.

---

## Push Schema to Database

To verify that the database connection is working and create the tables:

```bash
npx prisma db push
```

If successful, Prisma will create the corresponding tables in your PostgreSQL database.

---

## Generate Prisma Client

After pushing the schema, generate the Prisma Client:

```bash
npx prisma generate
```

You can now import Prisma in your project:

```js
import { PrismaClient } from "@prisma/client";

const prisma = new PrismaClient();
```

---

## Verify Tables

You can inspect your database using:

```bash
npx prisma studio
```

or by connecting with pgAdmin/PostgreSQL directly and checking that the tables have been created.
