# Change Last Character

For this example we will change the last character into comma.

1. Single line:

```vim
$ r,
```

2. Multiple lines

- Select the lines visually (`V` and move up/down)
- Then type:

```vim
:'<,'>normal $r,
```
