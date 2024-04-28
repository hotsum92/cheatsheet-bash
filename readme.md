# cheatsheet-bash

## execute in Vim

```bash
:.w !bash
```
##### map it to a key in Vim

```
nnoremap <Enter> :.w !bash<CR>
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

## curl

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

##### join with firt column

```
join <(echo -e '1 A\n2 B') <(echo -e '1 C\n2 E\n3 F')
```

##### all combinations

```
join -j 2 <(echo -e '1\n2\n3') <(echo -e '1\n2\n3')
```

join -j 2 <(echo -e '1\n2\n3') <(echo -e '1\n2\n3') | awk '!a[$1][$2]{ print $1, $2, a[$1][$2] } {a[$2][$1]++}'

## tr

##### A\nB\nC

```
echo 'A:B:C' | tr : '\n'
```

##### ABC

```
echo 'A B C' | tr -d ' '
```

## grep

##### A\nB

```
echo -e 'A\na\nB\nb' | grep -i a
```

##### A\nB\nD

```
echo -e 'A\nB\nC\nD' | grep -v C
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
echo 'href="http://test.com/test"' | grep -oE 'http(s?)://[0-9a-zA-Z?=#+_&:/.%]+'
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

## uniq

##### 2 A\n2 B\n1 C

```
echo -e 'A\nA\nB\nB\nC' | uniq -c
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

##### extract text inside tag

```
echo "<h1>test</h1>" | grep -o '<h1>.*</h1>' | sed 's#<h1>\(.*\)</h1>#\1#'
```

##### extract field

```
echo 'XXX 2024-10-23 XXX 2024-10-23 XXX' | sed -n 's/.*\(....-..-..\).*\(....-..-..\).*/\1 \2/p'
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
echo '"A B", C, D' | gawk -v FPAT='([^,]+)|(\"[^\"]+\"))' '{ print $1 }' # 
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

## docker

##### dump database

```
docker exec some-mysql sh -c 'exec mysqldump --all-databases -uroot -p"$MYSQL_ROOT_PASSWORD"' > ./all-databases.sql
```

##### restore database

```
docker exec -i some-mysql sh -c 'exec mysql -uroot -p"$MYSQL_ROOT_PASSWORD"' < ./all-databases.sql
```
