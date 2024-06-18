# cat

##### print file

```

cat <(echo -e 'A\nB\nC')
# A\nB\nC

```

##### concatenate files

```

cat <(echo 'A') <(echo 'B') <(echo 'C')
# A\nB\nC

```

##### C\nB\nA

```

tac <(echo -e 'A\nB\nC')

```

