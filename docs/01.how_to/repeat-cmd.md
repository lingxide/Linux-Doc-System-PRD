# How To Repeat Last Argument in Last Command

## Background

Suppose you are going to enter:

```
cp test.log test.bak
vim test.log
```

## How To

1. Enter `cp test.log test.bak`
2. Enter `vim[space]`
3. Enter `Alt+1`, hold `Alt` and press`.`

## Obtain other argument

Modify with `Alt+[numbers]`, for the first one use `Alt+0`

## Limitation

Only work in `emacs` mode.

`set -o emacs`
