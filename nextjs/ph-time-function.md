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
    const iso = row.original.created_at
    const date = new Date(iso)

    const year = date.getUTCFullYear()
    const month = date.toLocaleString('en-PH', { month: 'long', timeZone: 'UTC' })
    const day = date.getUTCDate()
    let hour = date.getUTCHours()
    const minute = date.getUTCMinutes().toString().padStart(2, '0')
    const ampm = hour >= 12 ? 'PM' : 'AM'

    hour = hour % 12
    hour = hour ? hour : 12

    const formatted = `${month} ${day}, ${year} ${hour}:${minute} ${ampm}`

    return <div className='text-right text-muted-foreground'>{formatted}</div>
  }
}
```
