# Middleware

This is how I manage middleware on my nextjs projects.

```ts
import { NextResponse } from "next/server";
import type { NextRequest } from "next/server";

export function middleware(req: NextRequest) {
  const { pathname } = req.nextUrl;
  const role = req.cookies.get("role")?.value;

  if (pathname.startsWith("/dashboard/c") && role !== "CASHIER") {
    return NextResponse.redirect(new URL("/not-found", req.url));
  }

  if (pathname.startsWith("/dashboard/a") && role !== "ADMIN") {
    return NextResponse.redirect(new URL("/not-found", req.url));
  }

  return NextResponse.next();
}

export const config = {
  matcher: ["/dashboard/:path*"],
};
```
