# Use Mutation

Unlike queries, mutations are typically used to create/update/delete data or perform server side-effects.

Here's an example of a mutation that adds a new user to the server:

`server/routers/auth.ts`

```ts
export const authRouter = t.router({
  register: t.procedure
    .input(
      z.object({
        name: z.string().min(2),
        email: z.string().email(),
        password: z.string().min(8)
      })
    )
    .mutation(async ({ input }) => {
      const hashedPassword = await bcrypt.hash(input.password, 10)

      const user = await prisma.user.create({
        data: {
          name: input.name,
          email: input.email,
          password: hashedPassword,
          created_at: getCurrentPhilippineTime(),
          updated_at: getCurrentPhilippineTime()
        }
      })

      return {
        success: true,
        message: 'Account created successfully',
        user: {
          id: user.user_id,
          name: user.name,
          email: user.email
        }
      }
    })

// You can also add more here!
```

I assume that you are using zod for validation.

Then in your register form add this codes:

```tsx
const mutation = trpc.auth.register.useMutation();

async function handleSubmit(values: RegisterProps) {
  const promise = mutation.mutateAsync(values);

  toast.promise(promise, {
    loading: "Please wait...",
    success: "Acoount created successfully!",
    error: "Could not create an account!.",
  });

  try {
    setSaveLoading(true);
    const response = await promise;
    if (response.success) {
      form.reset();
      window.location.href = "/login";
    }
  } catch (error) {
    console.error(error);
  } finally {
    setSaveLoading(false);
  }
}
```
