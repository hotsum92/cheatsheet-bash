# cheatsheet-bash

## execute oneline in Vim

```bash
:.w !bash
```
##### map it to a key in Vim

```
nnoremap <Enter> :.w !bash<CR>
```

## brace expansion

```
echo {A,B}.js # A.js B.js
echo {1..10}.txt # 1.txt 2.txt ... 10.txt
seq 1 10
echo {1..10} | xargs -n1
echo {1..10} | tr ' ' '\n'
echo {A..Z} | tr -d ' '
```

## Parameter expansions

### basics

```
file='image.jpg'; echo "${file/jpg/png}" # replace
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
```
paste A.txt B.txt
paste -d, A.txt B.txt
paste -d, -s A.txt B.txt
paste -d'\n' A.txt B.txt
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
shuf /usr/share/dict/words | head
echo $RANDOM
```

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
