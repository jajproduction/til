# How To Request The Data Every Second

This is an example on how to request the data every second or in any seconds.

```ts
const [orders, setOrders] = useState<string>("");

useEffect(() => {
  const data = async () => {
    try {
      const response = await axios.get("/api/admin/order-status/orders");
      setOrders(response.data.orders);
    } catch (error) {
      console.error(error);
    }
  };

  const intervalId = setInterval(data, 1000);
  return () => clearInterval(intervalId);
}, []);
```
