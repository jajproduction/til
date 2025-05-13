# Get Started with tRPC

tRPC (TypeScript Remote Procedure Call) is a framework that simplifies and type-safely facilitates client-server communication in web development, especially when using TypeScript.

Install the following:

```sh
npm install @trpc/client @trpc/next @trpc/react-query @trpc/server zod
```

## Create these core files:

`server/trpc.ts`:

```ts
import { initTRPC } from "@trpc/server";
import { ZodError } from "zod";

export const t = initTRPC.create({
  errorFormatter({ shape, error }) {
    return {
      ...shape,
      data: {
        ...shape.data,
        zodError:
          error.code === "BAD_REQUEST" && error.cause instanceof ZodError
            ? error.cause.flatten()
            : null,
      },
    };
  },
});
```

`server/routers/_app.ts`:

```ts
import { t } from "../trpc";
import { authRouter } from "./auth";

export const appRouter = t.router({
  auth: authRouter,
  // add more routers here!
});

export type AppRouter = typeof appRouter;
```

## Create mutation

`server/routers/auth.ts`:

```ts
import { z } from "zod";
import { t } from "../trpc";
import prisma from "@/prisma/prisma";
import { getCurrentPhilippineTime } from "@/lib/functions";
import bcrypt from "bcryptjs";
import { createSession } from "@/session";

export const authRouter = t.router({
  register: t.procedure
    .input(
      z.object({
        name: z.string().min(2),
        email: z.string().email(),
        password: z.string().min(8),
      }),
    )
    .mutation(async ({ input }) => {
      const hashedPassword = await bcrypt.hash(input.password, 10);

      const user = await prisma.user.create({
        data: {
          name: input.name,
          email: input.email,
          password: hashedPassword,
          created_at: getCurrentPhilippineTime(),
          updated_at: getCurrentPhilippineTime(),
        },
      });

      return {
        success: true,
        message: "Account created successfully",
        user: {
          id: user.user_id,
          name: user.name,
          email: user.email,
        },
      };
    }),

  login: t.procedure
    .input(
      z.object({
        email: z.string().email(),
        password: z.string().min(8),
      }),
    )
    .mutation(async ({ input }) => {
      const user = await prisma.user.findUnique({
        where: { email: input.email },
      });

      if (!user || !(await bcrypt.compare(input.password, user.password))) {
        throw new Error("Invalid email or password");
      }

      if (user.verified === 0) {
        throw new Error("Your account is not verified");
      }

      await createSession(
        user.user_id,
        user.name,
        user.email,
        user.role as "superadmin" | "admin" | "staff",
      );

      return {
        success: true,
        user: {
          user_id: user.user_id,
          name: user.name,
          email: user.email,
          role: user.role,
        },
      };
    }),
});
```

## Add API handler

`app/api/trpc/[trpc]/route.ts`:

```ts
import { fetchRequestHandler } from "@trpc/server/adapters/fetch";
import { appRouter } from "@/server/routers/_app";

const handler = (req: Request) => {
  return fetchRequestHandler({
    endpoint: "/api/trpc",
    req,
    router: appRouter,
    createContext: () => ({}),
  });
};

export { handler as GET, handler as POST };
```

## Create a client hook

`hooks/trpc.ts`:

```ts
"use client";

import { createTRPCReact } from "@trpc/react-query";
import type { AppRouter } from "@/server/routers/_app";

export const trpc = createTRPCReact<AppRouter>();
```

`components/provider/trpc-provider.tsx`:

```ts
'use client'

import { trpc } from '@/lib/trpc'
import { httpBatchLink } from '@trpc/client'
import { QueryClient, QueryClientProvider } from '@tanstack/react-query'
import React, { useState } from 'react'

export function TrpcProvider({ children }: { children: React.ReactNode }) {
  const [queryClient] = useState(() => new QueryClient())
  const [trpcClient] = useState(() =>
    trpc.createClient({
      links: [
        httpBatchLink({
          url: '/api/trpc'
        })
      ]
    })
  )

  return (
    <trpc.Provider client={trpcClient} queryClient={queryClient}>
      <QueryClientProvider client={queryClient}>{children}</QueryClientProvider>
    </trpc.Provider>
  )
}
```

Then wrap the root `layout.ts` file with `<TrpcProvider>` using a TrpcProvider component:

```ts
import type { Metadata } from 'next'
import { Inter } from 'next/font/google'
import './globals.css'
import { Toaster } from 'react-hot-toast'
import { ThemeProvider } from '@/components/themes/theme-provider'
import { TrpcProvider } from '@/components/provider/trpc-provider'

const inter = Inter({ subsets: ['latin'] })

export const metadata: Metadata = {
  title: {
    default: 'Get Started with TRPC',
    template: '%s | Get Started with TRPC'
  },
  description: 'NextJS with TRPC'
}

export default function RootLayout({ children }: Readonly<{ children: React.ReactNode }>) {
  return (
    <html lang='en' suppressHydrationWarning>
      <body className={`${inter.className}`}>
        <TrpcProvider>
          <ThemeProvider attribute='class' defaultTheme='light'>
            <Toaster position='top-right' reverseOrder={false} />
            {children}
          </ThemeProvider>
        </TrpcProvider>
      </body>
    </html>
  )
}
```
