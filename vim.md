# vim

## default shell

```
set shell=/bin/bash
```

## open link

```
vim http://www.google.com
```

```
curl http://www.google.com | vim -
```

## cmd

### execute commmand

```
:!ls
```

### bring the output of the command into the buffer

```
:r!ls
```

```
:'<,'>!ls
```

### execute command passed as argument

current line

```
:.w !bash
```

```
:'<,'>w !bash
```

## vim-grep

### current buffer

```
:vim {pattern} %
```

### all files

```
:vim {pattern} **
:vim {pattern} app/views/**
:vim {pattern} app/views/users/*
:vim {pattern} app/views/**/*.erb
:vim {pattern} app/views/**/_*.erb
```

### diff

```
windo diffthis
```

## env

```
:let $v = 'value'
:!echo $v
```

help let-environment
