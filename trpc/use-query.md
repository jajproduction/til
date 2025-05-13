# Use Query

This is how you read data from the server.

```ts
export const superadminRouter = t.router({
  getUsers: t.procedure.query(async () => {
    const users = await prisma.user.findMany({
      orderBy: {
        updated_at: 'desc'
      }
    })
    return users
  }),

  getCountUsers: t.procedure.query(async () => {
    const totalUsers = await prisma.user.count()

    const active = await prisma.user.count({
      where: { status: 1 }
    })

    const inActive = await prisma.user.count({
      where: { status: 0 }
    })

    const notVerified = await prisma.user.count({
      where: { verified: 0 }
    })

    return {
      totalUsers,
      active,
      inActive,
      notVerified
    }
  })

// You can also add more here!
```

Then this is how you display the data to the client.

```ts
const { data: reqData = [], refetch } = trpc.superadmin.getUsers.useQuery(
  undefined,
  {
    refetchOnWindowFocus: false,
  },
);
const [data, setData] = useState<TeamProps[]>([]);

useEffect(() => {
  if (!isEqual(reqData, data)) {
    setData(reqData);
  }

  refetch();
}, [reqData, data]);
```
