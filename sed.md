
## insert block upper

```
sed '/line3/e cat insert.txt' sample.txt
```

## insert block lower

```
sed '/line3/r insert.txt' sample.txt
```



