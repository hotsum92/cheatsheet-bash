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
