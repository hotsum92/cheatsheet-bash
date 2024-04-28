# cheatsheet-bash

## execute in Vim

```bash
:.w !bash
```
##### map it to a key in Vim

```
nnoremap <Enter> :.w !bash<CR>
```

## brace expansion

##### A.js B.js

```
echo {A,B}.js
```

##### 1.txt 2.txt ... 10.txt

```
echo {1..10}.txt
```

##### 1\n2\n ... 10

```
seq 1 10
```

##### 1 2 ... 10

```
echo {1..10}
```

##### AB ... Z

```
echo {A..Z} | tr -d ' '
```

## echo

##### echo with new line

```
echo -e 'A\nB\nC'
```

##### echo multiple lines

```
echo """AAA
BBB
CCC"""
```


## Parameter expansions

### basics

```
file='image.jpg'; echo "${file/jpg/png}" # image.png
```

```
text='error ABC error'; echo "${text//error/}" # remove all

day='2024-10-23'; echo "The day is ${day:8:2}" # slice
echo "${day:-empty}" # default value
echo ${day:=empty} > /dev/null; echo ${day} # assign default value
```

## redirect

```
echo 'test' > file.txt # new file
echo 'test' >> file.txt # append
echo 'test' 2> error.txt
echo 'test' &> error-std.txt
grep AA < letters.txt
```

### pattern match

```
ls dir/*.txt
ls dir/?0.txt
ls dir/[1-4].txt
ls dir/[24].txt
```

## range

```
echo {1..10}
echo {A..Z}
```

### substitution

```
path='/path/to/file.txt'; echo "${path%/*}" # /path/to
path='/path/to/file.txt'; echo "${path%.*}" # /path/to/file
path='/path/to/file.txt'; echo "${path##*.}" # txt
path='/path/to/file.txt'; echo "${path##*/}" # file.txt
```

## loop

```
for i in ./*.txt; do echo $i; done # can be with spaces
while read file; do echo $file; done < <(find . -name '*.txt') # can be with spaces
for i in {1..10}; do echo $i; done
while read line; do echo $line; done < file.txt
```

## arguments

```
echo "$#" # number of arguments
echo "$@" # "$1" "$2" ...
echo "$*" # "$1 $2 ..."
echo "$1" # first argument
```

## conditions

```
[ -z '' ] && echo 'empty'
[ -n 'v' ] && echo 'no empty'
[ 'a' == 'a' ] && echo 'equal'
[ 'a' != 'b' ] && echo 'not equal'
[ 1 -eq 1 ] && echo 'equal'
[ 1 -ne 2 ] && echo 'not equal'
[ 1 -lt 2 ] && echo 'less than'
[ 2 -gt 1 ] && echo 'greater than'
[ 1 -le 1 ] && echo 'less or equal'
[ 1 -ge 1 ] && echo 'greater or equal'
[ -f file.txt ] && echo 'file exists'
[ -d dir ] && echo 'directory exists'
[ -r file.txt ] && echo 'file is readable'
[ -w file.txt ] && echo 'file is writable'
[ -x file.txt ] && echo 'file is executable'
[ -s file.txt ] && echo 'file is not empty'
[ -e file.txt ] && echo 'file exists'
[ -z '' ] && echo 'empty'
[ -n 'v' ] && echo 'no empty'
[ 'a' == 'a' ] && echo 'equal'
[ 'a' != 'b' ] && echo 'not equal'
[ 1 -eq 1 ] && echo 'equal'
[ 1 -ne 2 ] && echo 'not equal'
[ 1 -lt 2 ] && echo 'less than'
[ 2 -gt 1 ] && echo 'greater than'
[ 1 -le 1 ] && echo 'less or equal'
[ 1 -ge 1 ] && echo 'greater or equal'
[ -f file.txt ] && [ ! -f dir ] && echo 'file exists'
[ -d dir ] && [ ! -d file.txt ] && echo 'directory exists'
[ -e file.txt ] && [ -e dir ] && echo 'file and dir exists'
```

## date

```
date "+%Y-%m-%d %H:%M:%S"
```

## curl

```
cat sample.json | curl -X POST -d @- -H "Content-Type: application/json" http://localhost:3000
```

## cut

```
cat numbers.txt | cut -f1,4 | head -n2
cat numbers.txt | cut -f2-4
cat numbers.csv | cut -d, -f1,4
cat dates.txt | cut -c1-4
df | awk '{ print $1 }' # separate field with space and tab but cut is default tab
```

## cat

```
cat A.txt B.txt
tac A.txt B.txt # reverse. useful for time sequence file
diff A.txt B.txt
```

## paste

```
paste A.txt B.txt
paste -d, A.txt B.txt
paste -d, -s A.txt B.txt
paste -d'\n' A.txt B.txt
```

## join

```
join <(echo -e '1 A\n2 B') <(echo -e '1 C\n2 E\n3 F')
```

```
join -j 2 <(echo {1..3} | xargs -n1) <(echo {1..3} | xargs -n1)
```

## tr

```
echo 'path/A:path/B:root/C' | tr : '\n'
```

## grep

```
grep -i dog animals.txt
grep -v Chicken animals.txt | wc -l
grep -l AA *.txt # print file contains AA
grep -n AA BB letters.txt # print line number
echo 'AA BB CC' | grep -o '[a-zA-Z]*'
echo 'href="http://test.com/test"' | grep -oE 'http(s?)://[0-9a-zA-Z?=#+_&:/.%]+'
```

## head

```
tail -n+2 header.csv
```

## sort

```
sort animals.txt | head
sort -r animals.txt | head
```

## uniq

```
echo -e 'A\nA\nB\nB\nC\nC' | uniq -c
```

```
uniq -c letters.txt | sort -nr | head
```

## md5sum

```
md5sum letters.txt
```

## rm

```
ls *.txt
rm !$ # remote last matched
```

```
head file.txt # see the contain
rm !$
```

```
echo '1+1' | bc
echo {1..10} | tr ' ' '+' | bc
echo {1..10} | xargs -n1 | paste -sd+ | bc
echo {1..10} | xargs -n1 | awk '{ sum += $1 } END { print sum }'
echo -e '2 2\n2 2\n3 2\n3 4' | awk '{count[$1]++; sum[$1]+=$2} END{for(i in count) print i, sum[i]/count[i]}'
```

## find

```
find . -type f
find . -type d
find . -name '*.txt'
find . -exec echo @ {} @ ';'
```

## yes

```
yes 'test' | head -n3
```

## xargs

```
echo 'test' | xargs -I{} echo {} A
echo {1..10} | xargs -n1
echo {1..10} | tr ' ' '\n' | xargs
find . -print0 | xargs -0 #avoid space
cat ./tmp.txt | tr '\n' '\0' | xargs -0 -n1
```

```
echo 'A B C' | xargs -n1
```

```
echo -e 'A\nB\nC' | xargs
```

## bash

```
bash -c 'cd ./dir; pwd'; pwd
echo 'print "created command"' | sed 's/print/echo/' | bash
```

## background

```
fg # foreground
echo 'test' & #background
ctrl-z #background
```

## words

```
shuf /usr/share/dict/words | head # random words
echo $RANDOM # random number
```

## sed

```
echo '<h2>test</h2>' | sed 's/<[^>]*>//g'
cat tmp.html | grep -o '<h1>.*</h1>' | sed 's#<h1>\(.*\)</h1>#\1#'
```

```
echo 'XXX 2024-10-23 XXX 2024-10-23 XXX' | sed 's/.*\(....-..-..\).*\(....-..-..\).*/\1 \2/' # extract value: 2024-10-23 2024-10-23
```

## awk

```
echo 'A B C' | awk '{ print $0 }'
echo 'A B C' | awk '{ print $2 }'
echo -e 'A B C\nA B C D' | awk '{ print "NR:" NR , "NF:" NF }'
echo -e 'A B C\nA B C D' | awk '/C D/'
echo -e 'A B C\nA B C D' | awk '$0 == "A B C"'
echo -e '1 2 3\n4 5 6\n2 3 4' | awk '$1 % 2 == 0'

awk '/<ul class="list-main"/,/<\/ul/' ./tmp.html
awk '{ letters[$1] += 1 } END { for (letter in letters) { print letter, letters[letter] } }' letters.txt | sort -nr -k2 | head
echo -e "A\nB\nC" | awk '{ printf $0 }' # remove new line
echo '1 2 3' | awk '{ printf("%04d-%02d-%02d\n", $1, $2, $3) }'
echo -e "A\n\nB\nC" | awk 'NF'
echo 'A,B,C' | awk -F, '{ print $1 }'
echo '"A B", C, D' | gawk -v FPAT='([^,]+)|(\"[^\"]+\"))' '{ print $1 }' # deal with csv but not perfect. cannot deal with new line
echo 'a b c d' | awk 'BEGIN { OFS = "," } { $1 = $1; print $0 }'
```

```
echo -e 'A\nB\nC' | awk 'NR==2' # print second line: B
```

```
paste <(echo {1..11} | xargs -n1) <(echo {11..1} | xargs -n1) | awk '$1 == $2 { print $1, $2}'
```

```
paste <(echo {1..11} | xargs -n1) <(echo {11..1} | xargs -n1) | awk '$1 >= $2 { print $1, $2}'
```

```
paste <(echo {1..11} | xargs -n1) <(echo {11..1} | xargs -n1) | awk '$1 <= $2 { print $1, $2}'
```

```
echo -e 'A\nB\nC' | awk 'NR==2' # print second line: B
```

```
echo -e 'A\nB\nC' | awk 'NR==2' # print second line: B
```

## docker

docker exec some-mysql sh -c 'exec mysqldump --all-databases -uroot -p"$MYSQL_ROOT_PASSWORD"' > ./all-databases.sql
docker exec -i some-mysql sh -c 'exec mysql -uroot -p"$MYSQL_ROOT_PASSWORD"' < ./all-databases.sql


## commands

awk
diff
cut
expand
expr
fmt
grep
head
lex
mre
paste
roff
sed
sort
tail
test
tr
wc
