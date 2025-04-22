# Count Line of Code

This is a command that will tell you the total lines of code in your NextJS app:

```sh
find . -type f \
! -path "./.git/*" \
! -path "./.next/*" \
! -path "./node_modules/*" \
\( -name "*.ts" -o -name "*.tsx" \) \
| xargs wc -l
```
