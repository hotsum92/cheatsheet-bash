
## conditions

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

[ -e file.txt ] && echo 'file exists'
[ ! -e file.txt ] && echo 'file not exists'

[ -f file.txt ] && echo 'file exists'
[ -x file.sh ] && echo 'file is executable'
[ -d dir ] && echo 'directory exists'
[ -r file.txt ] && echo 'file is readable'
[ -w file.txt ] && echo 'file is writable'
[ -s file.txt ] && echo 'file is not empty'

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

