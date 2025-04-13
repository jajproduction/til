# PH time function

Instead of using the default time and date for storing date and time in the database I used to add this function for real-time date and time.

```ts
function getCurrentPhilippineTime() {
  const now = new Date();
  const phtOffset = 8 * 60;
  const phtTime = new Date(now.getTime() + phtOffset * 60 * 1000);
  return phtTime;
}
```

This is an example on how you display the exact time, but if it's not try to adjust the 16hr offset.

```tsx
{
  accessorKey: 'created_at',
  header: () => <div className='text-right'>Date Created</div>,
  cell: ({ row }) => {
    const iso = row.getValue('created_at') as string
    const date = new Date(iso)

    const phtOffset = 16 * 60 * 60 * 1000
    const adjustedDate = new Date(date.getTime() + phtOffset)

    const formatted = adjustedDate.toLocaleString('en-PH', {
      year: 'numeric',
      month: 'long',
      day: 'numeric',
      hour: 'numeric',
      minute: 'numeric',
      hour12: true
    })

    return <div className='text-right text-muted-foreground'>{formatted}</div>
  }
}
```
