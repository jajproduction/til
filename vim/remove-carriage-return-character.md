# Remove Carriage Return Character

When you see this `^M` at the end of the line of your code and you wanted to remove them use the following command:

1. Enter command mode by pressing `:`
2. Run this command

```vim
:%s/\r$//
```
