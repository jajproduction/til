# Advanced React Native Setup

## Project Structure Overview

```sh
my-app/
├── apps/
│   ├── mobile/              # React Native (Expo)
│   └── web/                 # Optional Next.js or web app
├── packages/
│   ├── api/                 # tRPC router definitions
│   ├── db/                  # Drizzle + PostgreSQL setup
│   └── shared/              # shared types, utils, zod schemas
└── package.json
```

## Setup Turborepo + Monorepo Layout

```sh
npx create-turbo@latest my-app
cd my-app
```

Pick Expo for mobile.

You’ll get a ready structure with apps/mobile and apps/web.

## Setup PostgreSQL + Drizzle ORM

Inside `packages/db`:

```sh
mkdir packages/db
cd packages/db
npm init -y
npm install drizzle-orm drizzle-kit pg dotenv
```

Create `.env`:

```sh
DATABASE_URL=postgresql://user:password@localhost:5432/mydb
```

Create `drizzle.config.ts`:

```ts
import { defineConfig } from "drizzle-kit";

export default defineConfig({
  out: "./drizzle",
  schema: "./schema.ts",
  dialect: "postgresql",
  dbCredentials: {
    url: process.env.DATABASE_URL!,
  },
});
```

Create `schema.ts`:

```ts
import { pgTable, serial, text, timestamp } from "drizzle-orm/pg-core";

export const users = pgTable("users", {
  id: serial("id").primaryKey(),
  name: text("name").notNull(),
  createdAt: timestamp("created_at").defaultNow().notNull(),
});
```

And `index.ts`:

```ts
import { drizzle } from "drizzle-orm/node-postgres";
import { Pool } from "pg";
import * as schema from "./schema";

const pool = new Pool({ connectionString: process.env.DATABASE_URL });
export const db = drizzle(pool, { schema });
```

Run migrations:

```sh
npx drizzle-kit generate
npx drizzle-kit migrate
npx drizzle-kit push
```

## Setup tRPC API (Express backend)

In `packages/api`:

```sh
mkdir packages/api
cd packages/api
npm init -y
npm install @trpc/server zod express @trpc/server/adapters/express cors dotenv
```

Create `index.ts`:

```ts
import express from "express";
import cors from "cors";
import * as trpcExpress from "@trpc/server/adapters/express";
import { appRouter } from "./routers/_app";
import dotenv from "dotenv";

dotenv.config();
const app = express();
app.use(cors());

app.use(
  "/trpc",
  trpcExpress.createExpressMiddleware({
    router: appRouter,
  })
);

const port = process.env.PORT || 4000;
app.listen(port, () => {
  console.log(`✅ tRPC server running on http://localhost:${port}/trpc`);
});
```

Create router at `routers/_app.ts`:

```ts
import { initTRPC } from "@trpc/server";
import { z } from "zod";
import { db } from "@my-app/db";

const t = initTRPC.create();

export const appRouter = t.router({
  getUsers: t.procedure.query(async () => {
    return await db.query.users.findMany();
  }),
  addUser: t.procedure
    .input(z.object({ name: z.string() }))
    .mutation(async ({ input }) => {
      await db.insert(db.users).values({ name: input.name });
      return { success: true };
    }),
});

export type AppRouter = typeof appRouter;
```

## Setup React Native (Expo)

Inside `apps/mobile`:

```sh
cd apps/mobile
npx create-expo-app . --template
npm install @trpc/client @tanstack/react-query react-query
npm install @my-app/api
```

Create `utils/trpc.ts`:

```ts
import { createTRPCReact } from '@trpc/react-query';
import type { AppRouter } from '@my-app/api';
import Constants from 'expo-constants';

export const trpc = createTRPCReact<AppRouter>();

export const API_URL = Constants.expoConfig?.extra?.API_URL ?? 'http://localhost:4000/trpc';
```

In `App.tsx`:

```tsx
import { QueryClient, QueryClientProvider } from '@tanstack/react-query';
import { trpc, API_URL } from './utils/trpc';
import { httpBatchLink } from '@trpc/client';
import { Text, View, Button } from 'react-native';

const queryClient = new QueryClient();
const trpcClient = trpc.createClient({
  links: [
    httpBatchLink({
      url: API_URL,
    }),
  ],
});

export default function App() {
  const usersQuery = trpc.getUsers.useQuery();
  const addUserMutation = trpc.addUser.useMutation({
    onSuccess: () => usersQuery.refetch(),
  });

  return (
    <trpc.Provider client={trpcClient} queryClient={queryClient}>
      <QueryClientProvider client={queryClient}>
        <View style={{ marginTop: 50, padding: 20 }}>
          {usersQuery.data?.map((u) => (
            <Text key={u.id}>{u.name}</Text>
          ))}
          <Button title="Add User" onPress={() => addUserMutation.mutate({ name: 'New User' })} />
        </View>
      </QueryClientProvider>
    </trpc.Provider>
  );
}
```

## Add API URL to Expo Config

In `apps/mobile/app.config.js`:

```js
export default {
  expo: {
    name: "mobile",
    slug: "mobile",
    extra: {
      API_URL: "http://192.168.1.5:4000/trpc", // your local IP for testing
    },
  },
};
```

Replace `192.168.1.5` with your machine’s local IP (Expo needs LAN access).

## Run Everything

```sh
# Start the backend
cd packages/api
ts-node index.ts

# Start mobile
cd apps/mobile
npx expo start
```

## Bonus: Reuse code from your Next.js app

If your web app already uses tRPC + Drizzle:

- You can move your existing server/routers and server/db into packages/api and packages/db.
- Make sure to export AppRouter so the mobile app can consume the same types.
- Use the same zod schemas and procedures, so your React Native app will automatically have typed endpoints — just like Next.js.
