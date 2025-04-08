# Custom Spinner UI

Add this to your `components/ui/spinner.tsx`:

```tsx
import React from "react";
import { cn } from "@/lib/utils";
import { VariantProps, cva } from "class-variance-authority";
import { Loader2 } from "lucide-react";

const spinnerVariants = cva("flex-col items-center justify-center", {
  variants: {
    show: {
      true: "flex",
      false: "hidden",
    },
  },
  defaultVariants: {
    show: true,
  },
});

const loaderVariants = cva("animate-spin text-zinc-200 dark:text-zinc-900", {
  variants: {
    size: {
      small: "size-4",
      medium: "size-8",
      large: "size-12",
    },
  },
  defaultVariants: {
    size: "medium",
  },
});

interface SpinnerContentProps
  extends VariantProps<typeof spinnerVariants>,
    VariantProps<typeof loaderVariants> {
  className?: string;
  children?: React.ReactNode;
}

export function Spinner({
  size,
  show,
  children,
  className,
}: SpinnerContentProps) {
  return (
    <span className={spinnerVariants({ show })}>
      <Loader2 className={cn(loaderVariants({ size }), className)} />
      {children}
    </span>
  );
}
```

You could also use [hooks](nextjs/loading-state-hook.md) for your loading state but for this example I did not include the hook because I believe that you know how to do it!

```tsx
import { Spinner } from "@/components/ui/spinner";

<div className="flex items-center gap-3">
  <Spinner size="small" show={true} />
  <span>Please wait...</span>
</div>;
```
