# My Default Layout

This is how I modify the default `layout.tsx` file.

```tsx
import type { Metadata } from "next";
import { Inter } from "next/font/google";
import "./globals.css";

const inter = Inter({ subsets: ["latin"] });

export const metadata: Metadata = {
  metadataBase: new URL("#"), // Replace this to your domain
  alternates: { canonical: "/" },

  title: {
    default: "Jaj Dollesin",
    template: "%s | Jaj Dollesin",
  },
  description: "Developed by Jaj Dollesin.",
};

export default function RootLayout({
  children,
}: Readonly<{ children: React.ReactNode }>) {
  return (
    <html lang="en" suppressHydrationWarning>
      <body className={`${inter.className}`}>{children}</body>
    </html>
  );
}
```
