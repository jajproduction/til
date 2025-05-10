# Top Loader

Use this if you want to have a loader at the top, don't forget to put this also in your root `layout`.

We are using shadcn here, here is how you install:

```sh
npx shadcn@latest add progress
```

```tsx
"use client";

import { Progress } from "@/components/ui/progress";
import { usePathname } from "next/navigation";
import { useEffect, useState } from "react";

export function TopLoader() {
  const pathname = usePathname();
  const [progress, setProgress] = useState(0);
  const [visible, setVisible] = useState(false);

  useEffect(() => {
    setVisible(true);
    setProgress(30);

    const timeout = setTimeout(() => {
      setProgress(100);
    }, 200);

    const cleanup = setTimeout(() => {
      setVisible(false);
      setProgress(0);
    }, 600);

    return () => {
      clearTimeout(timeout);
      clearTimeout(cleanup);
    };
  }, [pathname]);

  if (!visible) return null;

  return (
    <div className="fixed top-0 left-0 right-0 z-50">
      <Progress value={progress} className="h-1" />
    </div>
  );
}
```
