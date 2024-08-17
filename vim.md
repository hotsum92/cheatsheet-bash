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

## filetype

```
echo &filetype
```

## list all filetypes

```
echo join(map(filter(split(globpath(&rtp, 'ftplugin/*.vim'), '\n'), 'fnamemodify(v:val, ":t:r")'), "\n")
```

## enclosing in parethese

```
cw(<C-r><C-o>")<ESC>
```

```
:h i_CTRL-R_CTRL-O
:h i_^-R_^-O
```

```
:put =system('date')
:put =system('echo $RANDOM')
```

## edit stream

```
echo "foo bar" | vim -E +%s/foo.// +%p -cq! /dev/stdin
```

Using ex command is equivalent to run Vim in Ex mode (vim -e).
+'cmd'/-c {cmd} - Invokes Ex command.
-cq! - Forcibly quit Vim as we're not saving any files.
-s - Run in silent mode (prevents extra screen flashes).
/dev/stdin - We use /dev/stdin as an input file, because using - doesn't work properly.
1s/pattern/something/g - Substitute pattern with something in the 1st line.
2,/pattern/d - Delete content starting from the 2nd line to the line with pattern.
%j - Joins all the lines together.
%p - Prints the buffer to the console output.
