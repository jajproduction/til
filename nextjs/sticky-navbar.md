# Sticky Navbar

We use shadcn for this navbar.

**Installation:**

```sh
npx shadcn@latest init
npx shadcn@latest add sheet button navigation-menu
```

**navbar.tsx:**

```tsx
import {
  Sheet,
  SheetTrigger,
  SheetContent,
  SheetHeader,
  SheetTitle,
  SheetDescription,
} from "@/components/ui/sheet";
import { Button } from "@/components/ui/button";
import Link from "next/link";
import {
  NavigationMenu,
  NavigationMenuList,
  NavigationMenuLink,
} from "@/components/ui/navigation-menu";
import { Cloud, Menu } from "lucide-react";

export default function Navbar() {
  return (
    <nav className="flex sticky top-0 z-50 h-16 w-full shrink-0 items-center px-4 bg-zinc-950/50 backdrop-blur-lg md:px-6">
      <Sheet>
        <SheetTrigger asChild>
          <Button variant="ghost" size="icon" className="lg:hidden">
            <Menu className="h-6 w-6" />
          </Button>
        </SheetTrigger>
        <SheetContent side="left" className="bg-zinc-950/50 backdrop-blur-lg">
          <SheetHeader>
            <SheetTitle>
              <Link href="#" prefetch={false}>
                <Cloud className="h-6 w-6 text-zinc-200" />
              </Link>
            </SheetTitle>
            <SheetDescription className="sr-only">Lorem ipsum</SheetDescription>
          </SheetHeader>
          <div className="p-4 pt-0">
            <Link
              href="#"
              className="flex w-full items-center py-2 text-lg font-semibold"
              prefetch={false}
            >
              Home
            </Link>
            <Link
              href="#"
              className="flex w-full items-center py-2 text-lg font-semibold"
              prefetch={false}
            >
              About
            </Link>
            <Link
              href="#"
              className="flex w-full items-center py-2 text-lg font-semibold"
              prefetch={false}
            >
              Services
            </Link>
            <Link
              href="#"
              className="flex w-full items-center py-2 text-lg font-semibold"
              prefetch={false}
            >
              Portfolio
            </Link>
            <Link
              href="#"
              className="flex w-full items-center py-2 text-lg font-semibold"
              prefetch={false}
            >
              Contact
            </Link>
          </div>
        </SheetContent>
      </Sheet>
      <div className="flex items-center justify-between w-full">
        <div>
          <Link
            href="/"
            className="mr-6 hidden lg:flex lg:space-x-1"
            prefetch={false}
          >
            <Cloud className="h-6 w-6" />
            <span>Jaj Products</span>
          </Link>
        </div>
        <div>
          <NavigationMenu className="hidden lg:flex">
            <NavigationMenuList>
              <NavigationMenuLink asChild>
                <Link
                  href="#"
                  className="group inline-flex h-9 w-max items-center justify-center rounded-md px-4 py-2 text-sm font-medium transition-colors text-zinc-500 hover:bg-transparent hover:text-zinc-100 focus:bg-transparent focus:text-zinc-100 focus:outline-none disabled:pointer-events-none disabled:opacity-50 data-[active]:bg-zinc-100/50 data-[state=open]:bg-zinc-100/50"
                  prefetch={false}
                >
                  Home
                </Link>
              </NavigationMenuLink>
              <NavigationMenuLink asChild>
                <Link
                  href="#"
                  className="group inline-flex h-9 w-max items-center justify-center rounded-md px-4 py-2 text-sm font-medium transition-colors text-zinc-500 hover:bg-transparent hover:text-zinc-100 focus:bg-transparent focus:text-zinc-100 focus:outline-none disabled:pointer-events-none disabled:opacity-50 data-[active]:bg-zinc-100/50 data-[state=open]:bg-zinc-100/50"
                  prefetch={false}
                >
                  About
                </Link>
              </NavigationMenuLink>
              <NavigationMenuLink asChild>
                <Link
                  href="#"
                  className="group inline-flex h-9 w-max items-center justify-center rounded-md px-4 py-2 text-sm font-medium transition-colors text-zinc-500 hover:bg-transparent hover:text-zinc-100 focus:bg-transparent focus:text-zinc-100 focus:outline-none disabled:pointer-events-none disabled:opacity-50 data-[active]:bg-zinc-100/50 data-[state=open]:bg-zinc-100/50"
                  prefetch={false}
                >
                  Services
                </Link>
              </NavigationMenuLink>
              <NavigationMenuLink asChild>
                <Link
                  href="#"
                  className="group inline-flex h-9 w-max items-center justify-center rounded-md px-4 py-2 text-sm font-medium transition-colors text-zinc-500 hover:bg-transparent hover:text-zinc-100 focus:bg-transparent focus:text-zinc-100 focus:outline-none disabled:pointer-events-none disabled:opacity-50 data-[active]:bg-zinc-100/50 data-[state=open]:bg-zinc-100/50"
                  prefetch={false}
                >
                  Portfolio
                </Link>
              </NavigationMenuLink>
              <NavigationMenuLink asChild>
                <Link
                  href="#"
                  className="group inline-flex h-9 w-max items-center justify-center rounded-md px-4 py-2 text-sm font-medium transition-colors text-zinc-500 hover:bg-transparent hover:text-zinc-100 focus:bg-transparent focus:text-zinc-100 focus:outline-none disabled:pointer-events-none disabled:opacity-50 data-[active]:bg-zinc-100/50 data-[state=open]:bg-zinc-100/50"
                  prefetch={false}
                >
                  Contact
                </Link>
              </NavigationMenuLink>
            </NavigationMenuList>
          </NavigationMenu>
        </div>
      </div>
    </nav>
  );
}
```
