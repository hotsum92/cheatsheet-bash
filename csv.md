```
csvcut -c name,age foobar.csv | csvlook
```

```
csvstack foo.csv bar.csv | csvlook
```

```
cat ./foobar.csv | cols -c age body sort -nr | csvlook 
```

```
cat ./foobar.csv | header -d | header -a v1,v2,v3 | csvlook
cat ./foobar.csv | header -r v1,v2,v3
```

```
cat ./foobar.csv | body grep foo | csvlook
```

```
cat ./foobar.csv | csvstat
cat ./foobar.csv | csvsql
```

https://github.com/shenwei356/csvtk
