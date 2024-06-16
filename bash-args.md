## options

```
while [ $# -gt 0 ]; do
do
  case $1 in
    -o | --option)
      if [ -z "$2" ]; then
        echo "option requires an argument"
        exit 1
      fi

      echo "option $2"
      ;;
    -h | --help)
      echo "help"
      exit 0
      ;;
    -*)
      echo "invalid option"
      exit 1
      ;;
    *)
      echo "argument $1"
      ;;
  esac
  shift
done
```

## arguments

```

function args { [ $# -eq 0 ] && echo 'no arguments'; }; args
function args { echo $#; }; args '1 2' '3' '4'
function args { for v in "$@"; do echo "$v"; done | cat; }; args '1 2' '3' '4'

```


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

