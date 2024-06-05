# cheatsheet-bash

## font

https://github.com/yuru7/bizin-gothic

```
あいうえお
漢字
アイウエオ
abcdefghijklmnopqrstuvwxyz
ABCDEFGHIJKLMNOPQRSTUVWXYZ
0123456789
@#$%^&*-_=+~
\|/
?!
''""``''
,.:;
07DZlrz|
(){}[]<>
（）〔〕［］｛｝〈〉《》「」『』【】
☆★○●◎◇◆
□■△▲▽▼※〒→←↑↓
　←全角スペース
```

## execute in Vim

```bash
:.w !bash
```
##### map it to a key in Vim

```
nnoremap <Enter> :.w !bash<CR>
```

## args

https://zenn.dev/kawarimidoll/articles/d546892a6d36eb

## deal with tmp file

[more detail](https://unix.stackexchange.com/questions/181937/how-create-a-temporary-file-in-shell-script)

```bash
tmpfile=$(mktemp /tmp/apc-script.XXXXXX)

exec 3>"$tmpfile"
exec 4<"$tmpfile"

rm "$tmpfile"
```

## trap

```bash
trap "echo 'clean tmp file($tmpfile)'; rm $tmpfile;" 0
```

0: when script exit


## options

### not continue script

```
#!/bin/bash -eu
```

-e: exit when error
-u: exit when undefined variable

### debug

```
set -x
echo "$(echo 'A') B" "C $(echo 'D')"
set +x
```

### string

### heredoc

```
json=$(cat << EOS
{
  "key": "value"
}
EOS
)
echo "$json"
```

### avoid expanding variable

```
json=$(cat << 'EOS'
{
  "key": "value"
}
EOS
)
echo "$json"
```

## quotes

##### xargs cat

/Place/='http://www.google.com'

```
echo "/Place/=\'http://www.google.com\'" | xargs echo
echo "/Place/='http://www.google.com'" | sed "s/\'/\\\'/g" | xargs echo
```

a'b'c
d

```
{ echo "a'b'c"; echo d; } | xargs -0 echo
```

abc d

```
{ echo "a'b'c"; echo d; } | xargs echo
```

test

```
echo ''\'''\''"test"'\'''\''' | xargs echo
```

''"test"''

```
echo ''\'''\''"test"'\'''\''' | cat -
```


##### 'A'

```
echo ''\''A'\'''
```

## word splitting

```
function first { echo $1; }
```

##### A

```
v='A B C'; first $v
```

##### A B C

```
v='A B C'; first "$v"
```

##### A\nB\nC

```
v='A B C';
for i in $v; do
  echo $i
done
```

##### A B C

```
v='A B C';
for i in "$v"; do
  echo $i
done
```

##### A A\nB B\nC C

```
v='A B C';
while read i; do
  echo $i
done < <(echo -e "A A\nB B\nC C")
```

##### A A.txt\nB B.txt\nC C.txt

```
for i in *.txt; do
  echo $i
done
```

## arguments

##### number of arguments

```
function len { echo "$#"; }; len A B C
```

##### all arguments

```
function args { echo "$@"; }; args A B C
```

##### first argument

```
function first { echo "$1"; }; first A B C
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

##### uuid

```
for i in `seq 50`; do echo `uuidgen`; done | sort | uniq
```

##### random string

```
cat /dev/urandom | tr -dc 'A-Z' | fold -w 16 | head -10000
```

##### 010 020 ... 100

```
seq -s " " -w 010 100
```

##### 1 2 ... 10

```
echo {1..10}
```

##### AB ... Z

```
echo {A..Z} | tr -d ' '
```

## pattern match

##### AA.txt BB.txt

```
ls *.txt
```

##### A.txt B.txt

```
ls ?.txt
```

##### 1.txt 2.txt 3.txt 4.txt

```
ls [1-4].txt
```

##### 2.txt 4.txt

```
ls [24].txt
```

```
echo ???[1-9]*
```

0001-seq22 0002-seq23 0003-seq26 0004-seq37 0005-seq41 0006-seq42 0007-seq42 0008-seq45

## Parameter expansions

##### image.jpg -> image.png

```
file='image.jpg'; echo "${file/jpg/png}"
```

##### ABA -> B

```
text='ABA'; echo "${text//A/}" # remove all
```

##### 2024-10-23 -> 23

```
day='2024-10-23'; echo "${day:8:2}"
```

##### default value

```
echo "${day:-empty}"
```

##### assign default value

```
echo ${day:=empty} > /dev/null; echo ${day}
```

##### /path/to

```
path='/path/to/file.txt'; echo "${path%/*}"
```

##### /path/to/file

```
path='/path/to/file.txt'; echo "${path%.*}"
```

##### txt

```
path='/path/to/file.txt'; echo "${path##*.}"
```

##### file.txt

```
path='/path/to/file.txt'; echo "${path##*/}"
```

## loop

##### basic

```
for i in {1..10}; do echo $i; done
```

##### read file line by line

```
while read file; do echo $file; done < <(find . -name '*.txt')
```

```
while read line; do echo $line; done < file.txt
```

## redirect

##### new file

```
echo 'test' > file.txt
```

##### append

```
echo 'test' >> file.txt
```

##### redirect error

```
echo 'test' 2> error.txt
```

##### redirect error and standard output

```
echo 'test' &> error-std.txt
```

##### redirect standard input

```
grep BB <(echo -e 'AA\nBB\nCC')
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
[[ '{errors: {}}' =~ .*errors.* ]] && echo 'errors'
function args { [ $# -eq 0 ] && echo 'no arguments'; }; args
```

### test arguments

```
CMD_NAME=$(basename $0)

if [ $# -eq 2 ]; then
  echo "$CMD_NAME <arg1> <arg2>"
  exit 1
fi
```

### test return code

```
if [ $? -ne 0 ]; then
  echo "Error: command failed"
  exit 1
fi
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

## date

```
date "+%Y-%m-%d %H:%M:%S"
```

ISO 8601UTC: year=2024 month=4 day=15 hour=8 minitue=16 second=16

```
date -d "2024-04-15T08:16:16.000Z" -u +"%Y-%m-%dT%H:%M:%S.000Z"
```

## curl

##### get global ip

```
curl ifconfig.me
```

##### get with parameter

```
curl -G -d key='value' localhost:8080
```


##### post json

```
curl -d "{\"hello\": \"world\"}" -H "Content-Type: application/json" http://localhost:8000
```

##### read from stdin

```
cat sample.json | curl -X POST -d @- -H "Content-Type: application/json" http://localhost:8000
```

##### use cookie

```
curl -c cookie.txt -b cookie.txt -b "name1=value1" http://localhost:8000/cookie
```

-c: save cookie
-b: load cookie

##### query parameter

```
curl -G -d key='value' http://localhost:8000
```

or

```
curl http://localhost:8000?key=value
```

##### Basic Auth

```
curl --basic -u user:password http://localhost:8000
```

##### Basic Auth without option

```
curl -u user:password http://localhost:8000 \
    -H "Authorization:Basic $(echo -n user:password | base64)"
```

echo -n: no new line for avoiding encoding new line

##### echo error

```
result=$(curl localhost:8000)

if [ $? -ne 0 ]; then
  echo "Error: curl failed"
  exit 1
fi

echo "$result"
```

## tar

c create
x extract
v verbose
z gzip
f name of file
t list

## expand

```
echo 'A	B	C' | expand
echo 'A	B	C' | expand -t 1
```

## unexpand

```
echo 'A	B	C' | expand | unexpand -a
```

## cut

##### 1 4

```
echo '1	2	3	4	5	6' | cut -f1,4
```

##### 2 3 4

```
echo '1 2 3 4 5' | cut -d' ' -f2-4
```

##### 2 3 4 5

```
echo '1 2 3 4 5' | cut -d' ' -f2-
```

##### 1234

```
echo '1234-67-90' | cut -c1-4
```

## cat

##### A\nB\nC

```
cat <(echo -e 'A\nB\nC')
```

##### A\nB\nC

```
cat <(echo 'A') <(echo 'B') <(echo 'C')
```

##### C\nB\nA

```
tac <(echo -e 'A\nB\nC')
```

## paste

use generate data from different source

##### A\t1\nB\t2\nC\t3

```
paste <(echo -e 'A\nB\nC') <(echo -e '1\n2\n3')
```

##### A,1\nB,2\nC,3

```
paste -d, <(echo -e 'A\nB\nC') <(echo -e '1\n2\n3')
```

##### A,B,C\n1,2,3

```
paste -d, -s <(echo -e 'A\nB\nC') <(echo -e '1\n2\n3')
```

## join

join need sort

##### join with firt column

```
join <(echo -e '1 A\n2 B') <(echo -e '1 C\n2 E\n3 F')
join -1 1 -2 1 <(echo -e '1 A\n2 B') <(echo -e '1 C\n2 E\n3 F')
```

##### left join

```
join -a 1 <(echo -e '1 A\n2 B\n4 G') <(echo -e '1 C\n2 E\n3 F')
join -a 1 -e 'NULL' -o '1.1,1.2,2.2' <(echo -e '1 A\n2 B\n4 G') <(echo -e '1 C\n2 E\n3 F')
```

##### all permutation

```
join -j 2 <(echo -e '1\n2\n3') <(echo -e '1\n2\n3')
```

##### all combinations

```
join -j 2 <(echo -e '1\n2\n3') <(echo -e '1\n2\n3') | awk '!a[$1][$2]{ print $1, $2, a[$1][$2] } {a[$2][$1]++}'
```

## tr

##### A\nB\nC

```
echo 'A:B:C' | tr : '\n'
```

##### ABC

```
echo 'A B C' | tr -d ' '
```

### A B C

```
echo "a b c" | tr [a-z] [A-Z]
```

### squize space

```
echo "a   b   c" | tr -s ' '
```

## grep

##### fixed string

```
echo '$-[]' | grep -F -e '$-[]'
```

##### A\nB

```
echo -e 'A\na\nB\nb' | grep -i a
```

##### A\nB\nD

```
echo -e 'A\nB\nC\nD' | grep -v C
```

##### match shortest

```
echo 'test;test;test;' | grep -oE 't[^;]*;'
```

##### print only file name

```
grep -l AA <(echo -e 'AA\nBB\nCC') <(echo -e 'nDD\nEE')
```

##### file:1:AA

```
grep -n AA <(echo -e 'AA\nBB\nCC') <(echo -e 'nDD\nEE')
```

##### AA\nBB

```
echo 'AA BB CC' | grep -o '[abAB]*'
```

##### extract url

```
echo 'href="http://test.com/test"' | grep -oE 'http(s?)://(\w|:|%|#|\$|&|\?|\(|\)|~|\.|=|\+|\-|/)+'
```

##### print first line

```
grep -rn -m1 .
```

## head

##### A\nB

```
head -n2 <(echo -e 'A\nB\nC')
```

## sort

##### A\nB\nC

```
echo -e 'B\nA\nC' | sort
```

##### C\nB\nA

```
echo -e 'B\nA\nC' | sort -r
```

##### 1\n02\n03

```
echo -e '03\n1\n02' | sort -n
```

-t,: separator
-r: reverse
-k2: second column
-n: number

## uniq

##### 2 A\n2 B\n1 C

```
echo -e 'A\nA\nB\nB\nC' | uniq -c
```

##### A\nB

```
echo -e 'A\nA\nB\nB\nC' | uniq -d
```

## md5sum

##### md5 filename

```
md5sum <(echo 'test')
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

## mv

```
ls *.bak | sed 's/\(.*\).bak/mv & \1/' | bash
```

## split

##### create file with line

```
echo -e 'A\nB\nC' split -l 1
```

## bc

##### 2

```
echo '1+1' | bc
```

##### sum

```
echo {1..10} | tr ' ' '+' | bc
```

##### sum

```
echo {1..10} | xargs -n1 | paste -sd+ | bc
```

paste -sd+: paste line and delimeter with +

##### sum

```
echo {1..10} | xargs -n1 | awk '{ sum += $1 } END { print sum }'
```

##### sum second column grouping by first column

```
echo -e '2 2\n2 2\n3 2\n3 4' | awk '{count[$1]++; sum[$1]+=$2} END{for(i in count) print i, sum[i]/count[i]}'
```

## find

##### find all files

```
find . -type f
```

##### find all directories

```
find . -type d
```

##### find all files with extension

```
find . --maxdepth 1 -name '*.txt'
```

##### find all files with extension

```
find . -exec echo @ {} @ ';'
```

#### find files exceeding 1M

```
find . -size +1M
```

## yes

```
yes 'test' | head -n3
```

## xargs

##### test A

```
echo 'test' | xargs -I{} echo {} A
```

##### 1\n2\n3

```
echo {1..3} | xargs -n1
```

##### 1 2 3

```
echo -e '1\n2\n\3' | xargs
```

##### avoid new line

```
find . -print0 | xargs -0
```

##### separate by new line and space

```
echo -e 'a a\nb b\nc c' | xargs -n1
```

##### avoid new line

```
echo -e 'a a\nb b\nc c' | tr '\n' '\0' | xargs -0 -n1
```

## bash

##### without cd

```
bash -c 'cd ../; pwd'; pwd
```

##### execute created command

```
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

##### options

BRE .[\*^$
ERE .[\*^$()+?{|

```
echo 'test' | sed -E 's/(es)/x\1x/g'
```

```
echo '++xx++' | sed 's/+/a/g'
```

##### test test

```
echo 'test' | sed 's/.*/& &/'
```

##### insert first line

```
echo -e 'B\nC' | sed '1iA'
```

##### append first line

```
echo -e 'A\nC' | sed '1aB'
```

##### print second line

```
echo -e 'A\nB\nC' | sed -n '2p'
```

##### delete tag

```
echo '<h2>test</h2>' | sed 's/<[^>]*>//g'
```

##### extract tag

```
echo 'test<a>test</a>test' | grep -oE '<a.*>.*?</a>'
```

`.*?` : shortest match

##### extract text inside tag

```
echo "<h1>test</h1>" | grep -o '<h1>.*</h1>' | sed 's#<h1>\(.*\)</h1>#\1#'
```

##### PascalCase or camelCase to snake_case

```
echo 'PascalCase' | sed 's/\(.\)\([A-Z]\)/\1_\2/g' | tr '[A-Z]' '[a-z]'
```

##### template

```
{ "value": "\1", "value": "\2" }
```

```
sed -e 's/\\1/A/' -e 's/\\2/B/' template
sed -e 's/\\1/C/' -e 's/\\2/D/' template
```

```
echo -e "A B\nC D" | awk '{ print "sed -e '\''s/\\\\1/" $1 "/'\''" " -e '\''s/\\\\2/" $2 "/'\''" " template" }' | bash
```

or

```
echo $data | awk -f file | bash
```

file will be ...

```
{ print "sed -e 's/\\\\1/" $1 "/'" " -e 's/\\\\2/" $2 "/'" " template" }
```

or

```
{
  str="sed ";

  for(i=1;i<=NF;i++) {
    str=str" -e 's/\\\\"i"/"$i"/'";
  }

  str=str" "template;

  print str;
}
```

```
awk -f file -v template=template data.txt
```

##### snake_case to PascalCase

```
echo 'snake_case' | awk -F '_' '{ str=""; for(i=1; i<=NF; i++) {str = str toupper(substr($i,1,1)) substr($i,2)} print str}'
```

##### snake_case to camelCase

```
echo 'snake_case' | awk -F '_' '{ str=$1; for(i=2; i<=NF; i++) {str = str toupper(substr($i,1,1)) substr($i,2)} print str}'
```

##### extract multi text inside tag

```
echo """
<head>
<title>
A
B
C
</title>
</head>
""" | sed -n '/<title>/,/<\/title>/p'
```

##### extract field

```
echo 'XXX 2024-10-23 XXX 2024-10-23 XXX' | sed -n 's/.*\(....-..-..\).*\(....-..-..\).*/\1 \2/p'
```

## mkdir

##### create directory

ignore error, create parent directory

```
mkdir -p dir1/dir2
```


## awk

##### A B C : A B C

```
echo 'A B C' | awk '{ print $0, ":", $1, $2, $3 }'
```

##### NR:1 NF:3

```
echo -e 'A B C' | awk '{ print "NR:" NR , "NF:" NF }'
```

##### A B C D

```
echo -e 'A B C\nA B C D' | awk '/C D/'
```

##### A B C D

```
echo -e 'A B C\nA B C D' | awk '$4 == "D"'
```

##### 4 5 6

```
echo -e '1 2 3\n4 5 6' | awk '$1 % 2 == 0'
```

##### print target tag

```
echo -e '<ul class="list-main">\ntest\n</ul>' | awk '/<ul class="list-main"/,/<\/ul/'
```

##### 0001-02-03

```
echo '1 2 3' | awk '{ printf("%04d-%02d-%02d\n", $1, $2, $3) }'
```
##### remote empty line

```
echo -e "A\n\nB\nC" | awk 'NF'
```

##### remote duplicate line

```
echo -e "A\nA\nB\nC" | awk '!a[$1]++'
```

##### remote duplicate combination

```
echo -e "A B\nA B\nB A\nC D" | awk '!a[$1][$2]++ && !a[$2][$1]++'
```

##### deal with csv but not perfect. cannot deal with new line

```
echo '"A B", C, D' | gawk -v FPAT='([^,]+)|(\"[^\"]+\"))' '{ print $1 }'
```

##### print second line

```
echo -e 'A\nB\nC' | awk 'NR==2'
```

##### print same column

```
paste <(echo {1..11} | xargs -n1) <(echo {11..1} | xargs -n1) | awk '$1 == $2 { print $1, $2}'
```

##### print greater column

```
paste <(echo {1..11} | xargs -n1) <(echo {11..1} | xargs -n1) | awk '$1 >= $2 { print $1, $2}'
```

##### print less column

```
paste <(echo {1..11} | xargs -n1) <(echo {11..1} | xargs -n1) | awk '$1 <= $2 { print $1, $2}'
```

##### group by line

```
echo -e 's a\n1\n1\ne\ns b\n2\n2\n2\ns c\n3\ne' | awk '/^s.?/{ group = $2 } /^s.?/,/^e.?/{ print group, $1 > group}'
```

##### group by file

```
awk '{ print FILENAME, $0 }' <(echo -e 'A\nB\nC') <(echo -e '1\n2\n3')
```

##### remove last 2 columns

```
echo '1	2	3r	4' | awk -F'\t' 'BEGIN { OFS = "\t" } {$NF="";$(NF-1)="";print $0}'
```

## column

```
echo -e 'AAAA,BBB,CCCC\n001,00002,03' | column -t -s ','
```

-t : table format, delete separator
-s : separator

## database output with tab

```
column -t -s "`printf '\t'`"
```

## set operation

##### union

A B C || B C D = A B C D

```
cat <(echo -e 'A\nB\nC') <(echo -e 'B\nC\nD') | sort | uniq
```

##### intersection

A B C && B C D = B C

```
cat <(echo -e 'A\nB\nC') <(echo -e 'B\nC\nD') | sort | uniq -d
join <(echo -e 'A\nB\nC') <(echo -e 'B\nC\nD')
```

##### difference

A B C diff B C D = A D

```
cat <(echo -e 'A\nB\nC') <(echo -e 'B\nC\nD') | sort | uniq -u
```

A B C - B C D = A

pass multiple times "BCD" to remove "BCD"

```
cat <(echo -e 'A\nB\nC') <(echo -e 'B\nC\nD') <(echo -e 'B\nC\nD') | sort | uniq -u
```

## docker

##### dump database

```
docker exec some-mysql sh -c 'exec mysqldump --all-databases -uroot -p"$MYSQL_ROOT_PASSWORD"' > ./all-databases.sql
```

##### restore database

```
docker exec -i some-mysql sh -c 'exec mysql -uroot -p"$MYSQL_ROOT_PASSWORD"' < ./all-databases.sql
```

## mysql

##### execute query

```
MYSQL_PWD=pwd mysql -u root -p -e 'show databases;'
```

##### execute query without header and border

```
mysql -N -s -u root -p -e 'show databases;'
```

##### db summary

```
select "db_name" as DB_NAME, table_name, table_rows
from information_schema.TABLES where table_schema = 'db_name' and table_rows > 0;
```

-N: no header

##### mysql dump

```
mysqldump --single-transaction {database} {table} > {file}
```

##### user list

```
select user, host from mysql.user;
```

##### user authorization

```
select * from mysql.db;
```

```
show grants for {username};
```

## php

##### interactive php

```
php -a
```

##### develop server

```
php -S localhost:8000 <rouetr.php>
```

##### execute php by every input line

```
echo {1..3} | xargs -n1 | php -R 'echo $argn,"\n";'
```

##### decode url

```
echo 'http%3A%2F%2F%E3%83%86%E3%82%B9%E3%83%88.com' | php -R 'echo urldecode($argn), "\n";'
```

##### encode url

```
jq --arg q 日本語 --arg ie UTF-8 -nr '@uri "https://www.google.com/search?q=\($q)&ie=\($ie)"'
```

## jq

##### "1"\n"2"

```
echo '{"items":[{"name":"1"},{"name":"2"}]}' | jq '.items[].name'
```

##### 1\n2

```
echo '{"items":[{"name":"1"},{"name":"2"}]}' | jq -r '.items[].name'
```

##### format { "n": "1", "v": "a" }

```
echo '{"items":[{"name":"1", "value":"a"},{"name":"2", "value":"b"}]}' | jq '.items[] | { n: .name, v: .value }'
```

##### csv

```
echo '{"items":[{"name":"1", "value":"a"},{"name":"2", "value":"b"}]}' | jq -r '.items[] | [ .name, .value ] | @csv'
```

```
echo '[{"name":"1", "value":"a"},{"name":"2", "value":"b"}]' | jq -c '.[]'
```

## diff

```

a=$(cat << EOS
A
B	K
C
EOS
)
b=$(cat << EOS
 A
B K
D
EOS
)
diff -w <(echo "$a") <(echo "$b")

```

## inconv

```
iconv -f ENCODING -t ENCODING INPUTFILE
```

-c : ignore error

| Encoding   | Alias |
|------------|-------|
| UTF-8      | UTF8  |
| UTF-16     | UTF16 |
| Shift-JIS  | SJIS  |
| EUC-JP     | EUCJP |
| JIS(ISO2022) | ISO2022JP+ |

## nkf

```
nkf -w input > output
nkf -w --overwrite input
```
