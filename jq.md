
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

## select deep

```
cat ./sample.json | jq '[.items[] | {name: .name, size: .size, owner_id: .owner.id, owner_name: .owner.name}]'
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

```
jq -s -R 'split("\n")|map(split(","))|map({"id": .[0], "name": .[1]})' foobar.csv
```

```
ruby -rcsv -rjson -e 'print CSV.new(STDIN.read, headers: true).to_a.map { |row| row.to_hash }.to_json' < foobar-2.csv
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

## yaml

##### json to yaml

```
ruby -rjson -ryaml -e 'print JSON.parse(STDIN.read).to_yaml' < sample.json
```

##### yaml to json

```
ruby -rjson -ryaml -e 'print YAML.load(STDIN.read).to_json' < sample.json
```


ruby -rjson -ryaml -e 'print JSON.parse(STDIN.read).to_yaml' | tr -d ' ' | awk -F: '{ print "key:", $1",", "value:", $2 }'


pup 'head meta json{}' | jq '.[] | select(.property != null) | { (.property): .content }' | jq -s add
