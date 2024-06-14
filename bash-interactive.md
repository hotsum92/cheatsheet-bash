## color

```

ESC=$(printf '\033')
echo "${ESC}[31mRED${ESC}"
echo "${ESC}[32mGREEN${ESC}"
echo "${ESC}[33mYELLOW${ESC}"
echo "${ESC}[34mBLUE${ESC}"
echo "${ESC}[35mMAGENTA${ESC}"
echo "${ESC}[36mCYAN${ESC}"
echo "${ESC}[37mWHITE${ESC}"
echo "${ESC}[0mRESET${ESC}"

```

## read

```

read -p "Do you want to continue? [y/n] " answer

case $answer in
  [Yy]* )
    echo "Yes."
    ;;
  * )
    echo "Canceled."
    ;;
esac

```
