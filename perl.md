# perl

$_: each line
$.: line number

```
echo 'test' | perl -n -e 'print($.)'
```

```
echo 'test' | perl -p -e 'print("test")'
```

-p: print $_

```
echo '1 2 3' | perl -a -F' ' -e 'print(@F[2])'
echo '1 2 3' | perl -a -F' ' -e 'print(@F)'
```


## print second line

```
echo -e '1\n2\n3' | perl -n -e 'print if $.==2'
```

## print first line

```
echo -e '1\n2\n3' | perl -n -e 'print; exit'
```

## replace with random number

```
echo -e 'a 1\n2 b\n3 c' | perl -n -e 's/\d+/int(rand(100))/eg; print'
```

## replace with seq number

```
echo -e 'a 1\n2 3 b\n4 c' | perl -n -e 's/\d+/++$i/eg; print'
```

## insert line number

```
echo -e 'a\nb\nc' | perl -n -e 'print($. . " " . $_)'
```

## remove comment

```
echo -e 'a\n#b\nc' | perl -n -e 'print unless /^#/'
echo -e 'a\n#b\nc' | perl -n -e 'print if !/^#/'
```
