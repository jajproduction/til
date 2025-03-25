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
