# Request Multiple Asynchronous Data Sources at Once

**How It Works:**

- If all promises in the array resolve, `Promise.all` returns an array of their results.
- If any promise rejects, `Promise.all` immediately rejects with that error.

This is an example of how I used `Promise.all`:

```tsx
useEffect(() => {
  const data = async () => {
    try {
      const [monthRes, weekRes] = await Promise.all([
        axios.get<{ month: MonthlyProps[] }>(`/api/admin/overview/chart/month`),
        axios.get<{ week: WeeklyProps[] }>(`/api/admin/overview/chart/week`),
      ]);

      setMonthly(monthRes.data.month);
      setWeekly(weekRes.data.week);
      setLoading(false);
    } catch (error) {
      console.error("Error monthly and weekly data:", error);
    }
  };

  const intervalId = setInterval(data, 1000);
  return () => clearInterval(intervalId);
}, []);
```
