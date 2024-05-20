# awk

## pattern for use

### valification

```awk
NF != 3 { print "Error: expected 3 fields" }
$2 < 3.35 { print "Error: rate < 3.35" }
$2 > 6.00 { print "Error: rate > 6.00" }
```

### change separator

```
echo 'a,b,c' | awk -F, 'BEGIN {OFS="\t"} {$1=$1;print $0}'
```

### summarization

```awk
BEGIN { print "name" "rate" "hours"; print "" }
{ print }
END { print total }
```

## regular expression test

```
awk '$1 ~ $2' <(echo 'http://test.com/path/1 http(s?)://(\w|:|%|#|\$|&|\?|\(|\)|~|\.|=|\+|\-|/)+')
```

## transform

```


## print certain line

```
echo -e 'Beth 0\nDan 40\nBenny 30' | awk 'NR == 2'
```

## skip empty line

```
echo -e 'Beth 0\n\nDan 40' | awk 'NF > 0'
```

## skip certain field

```
echo -e 'Beth 0 ...other\nDan 40 ...other' | awk '{$2 = ""; print $0}'
```

## print line number

```
echo -e 'Beth 0\nDan 40' | awk '{print NR, $0}'
```

## print filename

```
awk '{print FILENAME, "FNR="FNR, "NR="NR, $0}' <(echo -e 'Beth 0\nDan 40') <(echo -e 'Beth 0\nDan 40')
```

## length

```
echo -e 'Beth 0\nDan 40' | awk '{print length($1)}'
```

## sort by column

```
echo -e 'Beth 0\nDan 40' | awk '{printf("%6.2f %s\n", $2, $0)}' | sort -r
```

## print valuables

```bash
echo -e "a b c\nd e f" | awk '{print $0, "NR="NR, "NF="NF,  "$NF="$NF}'
```

## print formatted valuables

```bash
echo -e 'Beth 0\nDan 40' | awk '{printf("%-8s %6.2f\n", $1, $2)}'
```

```bash
echo -e 'Beth 0\nDan 40' | awk '{printf("%+8s %6.2f\n", $1, $2)}'
```

## select columns

```bash
echo -e 'Beth 0\nDan 40' | awk '$2 > 10'
```

```bash
echo -e 'Beth 0\nDan 40' | awk '$1 ~ /Dan/'
```

```bash
echo -e 'Beth 0\nDan 40' | awk '!($1 == "Beth")'
```

```bash
echo -e 'Beth 0\nDan 40' | awk '$1 == "Beth" && !($1 == "Dan")'
```

## pipe

```bash
ls | awk '{print $0 | ls}'
```

## split by empty line

```
text="""data1
1
2

data2
3
4
"""

echo "$text" | awk 'BEGIN { RS="" } /data1/'
echo "$text" | awk 'BEGIN { RS="";FS="\n" } /data1/ { print $2 }'
echo "$text" | awk 'BEGIN { RS="";FS="\n";OFS=" " } /data1/ {$1=$1; print $0 }'
```

## dictionnary

```
text="""header 1
data1 2

header 4
data1 5
"""

echo "$text" | awk '/^header/ { header=$2; next } /^data1/ { data1=$2; next } { print header, data1 }'
```

