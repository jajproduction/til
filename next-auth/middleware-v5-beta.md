# Middleware v5 Beta

## Structure

```sh
app/
├── api/
│ └── auth/
│ └── [...nextauth]/
│ └── route.ts
└── auth/
├── helpers.ts
└── index.ts
components/
├── AuthButton.client.tsx
└── AuthButton.server.tsx
middleware.ts
```

## Installation

**Note**:

- `beta version 5`. This setup works well if this version comes out.
- Use `bcryptjs` for hashing the password
- Use `prisma` for life.

```bash
npm install next-auth@beta #v5
npm install bcryptjs @types/bcryptjs
npm install prisma @prisma/client
```

## Setup

`app/api/auth/[...nextauth]/route.ts`

```tsx
import { handlers } from "@/app/auth";

export const { GET, POST } = handlers;
```

`app/auth/helper.ts`

```tsx
"use server";

import { signIn as naSignIn, signOut as naSignOut } from ".";

export async function signIn() {
  await naSignIn();
}

export async function signOut() {
  await naSignOut();
}
```

`app/auth/index.ts`

```tsx
import prisma from "@/prisma/prisma";
import bcrypt from "bcryptjs";
import NextAuth, { User, NextAuthConfig } from "next-auth";
import Credentials from "next-auth/providers/credentials";

export const BASE_PATH = "/api/auth";

const authOptions: NextAuthConfig = {
  providers: [
    Credentials({
      name: "Credentials",
      credentials: {
        username: { label: "Username", type: "text", placeholder: "willsmith" },
        password: { label: "Password", type: "password" },
      },
      async authorize(credentials): Promise<User | null> {
        if (!credentials?.username || !credentials?.password) {
          return null;
        }

        try {
          const username = credentials.username as string;
          const password = credentials.password as string;

          // Fetch user from the database
          const user = await prisma.user.findUnique({
            where: { username: username },
          });

          // Check if user exists and validate password
          if (user && (await bcrypt.compare(password, user.password))) {
            return {
              id: user.id.toString(),
              name: `${user.firstname} ${user.lastname}`,
              email: user.email,
            };
          }

          return null;
        } catch (error) {
          console.error("Error authorizing user:", error);
          return null;
        }
      },
    }),
  ],
  pages: {
    signIn: "/auth/signin",
  },
  basePath: BASE_PATH,
  secret: process.env.NEXTAUTH_SECRET,
};

export const { handlers, auth, signIn, signOut } = NextAuth(authOptions);
```

`components/AuthButton.client.tsx`

```tsx
"use client";

import { useSession } from "next-auth/react";
import { Button } from "@/components/ui/button";
import { signIn, signOut } from "@/app/auth/helpers";

export default function AuthButton() {
  const session = useSession();

  return session?.data?.user ? (
    <Button
      onClick={async () => {
        await signOut();
        await signIn();
      }}
    >
      {session.data?.user?.name} : Sign Out
    </Button>
  ) : (
    <Button
      onClick={async () => await signIn()}
      variant="default"
      className="bg-green-600 text-white hover:bg-green-500 hover:text-black"
    >
      Get Started Today
    </Button>
  );
}
```

`components/AuthButton.server.tsx`

```tsx
import { SessionProvider } from "next-auth/react";
import { BASE_PATH, auth } from "@/app/auth";
import AuthButtonClient from "./AuthButton.client";

export default async function AuthButton() {
  const session = await auth();

  if (session && session.user) {
    session.user = {
      name: session.user.name,
      email: session.user.email,
    };
  }

  return (
    <SessionProvider basePath={BASE_PATH} session={session}>
      <AuthButtonClient />
    </SessionProvider>
  );
}
```

`middleware.ts`

```tsx
import { NextResponse } from "next/server";
import { auth, BASE_PATH } from "@/app/auth";

export const config = {
  matcher: ["/((?!api|_next/static|_next/image|favicon.ico|auth/signup).*)"],
};

export default auth((req) => {
  const reqUrl = new URL(req.url);

  if (req.auth && reqUrl.pathname === "/") {
    return NextResponse.redirect(new URL(`/dashboard`, req.url));
  }

  if (
    !req.auth &&
    reqUrl.pathname !== "/" &&
    reqUrl.pathname !== `/auth/signin` &&
    reqUrl.pathname !== `/auth/signup`
  ) {
    return NextResponse.redirect(
      new URL(
        `${BASE_PATH}/signin?callbackUrl=${encodeURIComponent(reqUrl.pathname)}`,
        req.url,
      ),
    );
  }
});
```
