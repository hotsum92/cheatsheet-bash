# aspell

## spell check interactive mode

```bash
aspell -a
```

## list misspelled words

```bash
echo -e 'tist\ncheet' | aspell list
```

```bash
echo -e 'tist\ncheet' | aspell -a | grep '^&'
```
