
## Pretty output

```
cat ./sample.json | jq .
```

## Compact output

```
cat ./sample.json | jq -c .
```

## specific key

```
cat ./sample.json | jq '.total_count'
```

## value in array

```
cat ./sample.json | jq '.items[0].name'
```

## array of values

```
cat ./sample.json | jq '.items[].name'
```

## rm quotes

```
cat ./sample.json | jq -r '.items[].name'
```

## select

```
cat ./sample.json | jq '[.items[] | {name: .name, size: .size}]'
```

## filter

```
cat ./sample.json | jq '[.items[] | select(.size >= 25)]'
```

## tsv

```
cat ./sample.json | jq -r '.items[] | [.name, .size] | @tsv'
```

## csv

```
cat ./sample.json | jq -r '.items[] | [.name, .size] | @csv'
```

## format

```
cat ./sample.json | jq -rc '.items[] | "\(.name)(\(.size))"'
```

## escape

echo '{ "value": "foo\nbar" }' | jq -r "[.value] | @tsv"

## unescape

printf 'foo\nbar'

## get value keep line breaks

```
cat ./sample.json | jq -r '.' | awk -F: '/"[^"]+":[^\[{]+$/ {print $2; next} {print "" }' | tr -d '", '
```
