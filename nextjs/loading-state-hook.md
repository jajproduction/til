# Loading State Hook

Reusable loading state is nice!

1. Create the hook `hooks/useLoading.ts`:

```tsx
import { useState } from "react";

export const useLoading = () => {
  const [loading, setLoading] = useState(false);
  return { loading, setLoading };
};
```

2. Import and use them on your components.

```tsx
import { useLoading } from '@/hooks/useLoading'

const { loading, setLoading } = useLoading()

<Button type="submit" className="w-full" disabled={loading}>
  {loading ? (
    <div className="flex items-center gap-3">
      <Spinner size="small" show={true} />
      <span>Please wait...</span>
    </div>
  ) : (
    "Login"
  )}
</Button>
```
