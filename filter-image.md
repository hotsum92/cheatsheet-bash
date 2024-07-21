## print file size

```
find . -type f -name '*.png' -size +1M -exec du -h {} \; | awk '{print $2, $1}'
```

## print image size

```
find . -type f -name "*.jpg" -exec identify {} \; | awk '{print $1, $2, $3}'
```

path type size
