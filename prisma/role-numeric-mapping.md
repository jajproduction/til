# Role Numeric Mapping

Prisma does not natively support numeric enums directly, but you can achieve this by using a regular `Int` field instead of an `enum`.

Here’s how you can do it:

**Option 1: Use an Int Instead of an Enum** Modify your Prisma schema like this:

```prisma
model User {
  id   String @id @default(uuid())
  role Int    @default(1) // 0 = Admin, 1 = User
}
```

Then, in your application code, you can define constants to improve readability:

```prisma
const Role = {
  ADMIN: 0,
  USER: 1,
};

// Example Usage:
const newUser = await prisma.user.create({
  data: {
    role: Role.USER, // 1
  },
});
```

**Option 2: Keep the Enum but Map It to Numbers** Prisma allows mapping enum values to different database representations using `@map`:

```prisma
enum Role {
  ADMIN @map(0)
  USER  @map(1)
}

model User {
  id   String @id @default(uuid())
  role Role   @default(USER)
}
```

However, **this only works in PostgreSQL** and doesn’t work for all database providers.
