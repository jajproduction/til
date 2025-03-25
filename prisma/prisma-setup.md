# Prisma Setup

## Prisma Client

```bash
npm install @prisma/client
```

If prisma not yet installed:

```bash
npm install prisma
npx prisma init
```

After creating models:

```bash
npx prisma migrate dev
```

## prisma.ts

```ts
import { PrismaClient } from "@prisma/client";

let prisma: PrismaClient;
declare global {
  namespace NodeJS {
    interface Global {
      prisma?: PrismaClient;
    }
  }
}

const globalForPrisma = global as typeof globalThis & { prisma?: PrismaClient };

if (process.env.NODE_ENV === "production") {
  prisma = new PrismaClient();
} else {
  if (!globalForPrisma.prisma) {
    globalForPrisma.prisma = new PrismaClient();
  }
  prisma = globalForPrisma.prisma;
}

export default prisma;
```
