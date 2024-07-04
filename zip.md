# zip

## prepare file

```
mkdir -p /tmp/zip
dd if=/dev/zero of=/tmp/zip/1K.dummy bs=1K count=1
ls -lh /tmp/zip/1K.dummy
```

## zip

```
zip -r /tmp/data.zip /tmp/zip
ls -lh /tmp/data.zip
```

10M -> 11K

## zip with file lists

```
find . -name "*.md" | zip markdown -@
ls -lh markdown.zip
```

## standard output

```
zip -r - ./tmp/zip 2> /dev/null | \
curl \
    -s --trace-ascii /dev/stderr \
    -X POST \
    --header "Content-Type: application/zip" \
    --data-binary "@-" \
    example.com 1> /dev/null
```

## standard input

```
cat sample.json | zip /tmp/sample -
ls -lh /tmp/sample.zip
```

or

```
cat sample.json | zip > /tmp/sample.zip
ls -lh /tmp/sample.zip
```

## unzip

```
unzip -p /tmp/data.zip
unzip /tmp/data.zip -d /tmp/data
```
