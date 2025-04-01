# Conventional Commits Format

Here are some **best practices** to make your Git commit messages even more effective.

1. Follow a clear format

✅ Example: `typee(scope): short description.`

- `type`: Describes the purpose (feat, fix, chore, refector, etc.)
- `scope`: The area of code affected (optional but useful)
- `description`: A concise summary

2. Use the right commit types

- `feat`: New feature
- `fix`: Bug fix
- `chore`: Maintenance or setup tasks
- `docs`: Documentation updates
- `style`: Code formatting (no logic changes)
- `refactor`: Code restructuring (no feature change)
- `perf`: Performance improvements
- `test`: Adding or updating tests
- `ci`: Changes to CI/DI pipeline
- `build`: Build-related changes

Example:

```sh
git commit -m 'feat(inventory): add low stock warning feature.'
git commit -m 'fix(auth): resolve login redirect issue.'
git commit -m 'chore(deps): update Prisma to latest version.'
```

3. Write in the imperative mood

- ✅ `fix(auth): resolve login issue.`
- ❌ `fixed login issue`
- ❌ `fixes login issue`

_Think of the message as a command to Git: "Apply this fix."_

4. Keep it concise but meaningful

- ✅ `fix(cart): prevent duplicate items on checkout.`
- ❌ `fixes some issue in the cart.`

5. Group related changes into a single commit

- Avoid commits like:

```sh
git commit -m 'fix: update header.'
git commit -m 'fix: adjust margin.'
git commit -m 'fix: change color.'
```

- Instead, use:

```sh
git commit -m 'fix(ui): adjust header styles for better alignment.'
```

6. Use `--amend for small fixes before pushing`

If you need to correct your last commit before pushing:

```sh
git commit --amend
```

7. Reference issues/tickets when needed

- ✅ `fix(auth): resolve login issue (#123)`
- ✅ `feat(inventory): add stock  alert system (closes #456)`

8. If your deleting the contents inside the `master` branch and pushing another contents to the master branch.

```sh
git commit -m 'refactor(branch): reset master to branch-name'
```
