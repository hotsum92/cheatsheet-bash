


```

[ -z '' ] && echo 'zero'
[ -n 'v' ] && echo 'no zero'
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

```
