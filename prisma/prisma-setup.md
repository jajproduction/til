# Prisma Setup

This guide shows you how to use Prisma with Next.js 15, a fullstack React framework. You'll learn how to create a Prisma Postgres instance, set up Prisma ORM with Next.js, handle migrations, and deploy your application to Vercel.

## Set up Prisma ORM

First, we need to install a few dependencies. At the root of your project in your terminal, run:

```sh
npm install prisma tsx --save-dev
npm install @prisma/client @prisma/extension-accelerate
```

Then, run `prisma init` to initialize Prisma ORM in your project.

```sh
npx prisma init
```

This will create a new `prisma` directory in your project, with a `schema.prisma` file inside of it. The `schema.prisma` file is where you will define your database models.

The `prisma init` command also creates a `.env` file in your project root to store your database connection string.

Next, let's add two models to your `schema.prisma` file. A `User` model and a `Post` model:

```prisma
generator client {
  provider = "prisma-client-js"
  output   = "./generated/prisma"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id    Int     @id @default(autoincrement())
  email String  @unique
  name  String?
  posts Post[]
}

model Post {
  id        Int     @id @default(autoincrement())
  title     String
  content   String?
  published Boolean @default(false)
  authorId  Int
  author    User    @relation(fields: [authorId], references: [id])
}
```

This represents a simple blog with users and posts. Each Post can have a User as an author and each User can have many Posts.

Now that we have a Prisma schema and two models, let's map this schema to our Prisma Postgres database with a migration.

Finally, add the path of the generated Prisma Client to your `.gitignore` file so you're not checking in the query engine into version control:

```sh
/prisma/generated
```

Update your database schema:

```sh
npx prisma migrate dev
```

## Set up Prisma Client

Now that we have a database, we can set up Prisma Client and connect it to our database.

Inside the prisma folder at the root of your project, create a `prisma.ts` file to it.

Now, add the following code to your `prisma/prisma.ts` file:

```ts
import { PrismaClient } from "@/prisma/generated/prisma";
import { withAccelerate } from "@prisma/extension-accelerate";

const globalForPrisma = global as unknown as {
  prisma: PrismaClient;
};

const prisma =
  globalForPrisma.prisma || new PrismaClient().$extends(withAccelerate());

if (process.env.NODE_ENV !== "production") globalForPrisma.prisma = prisma;

export default prisma;
```

## Source

If you want more information about Prisma check the [link here](https://prisma.io/docs/guides/nextjs)
