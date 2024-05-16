# git

## git bisect

```sh
git bisect run ./test.sh
```

return 125 to skip

## git diff log .. ...

### git diff

git diff ..  : diff A and B
git diff ... : diff A - B

### git log

git log ..  : log A to B
git log ... : log A and B but not mutual

## git log

git log --grep="pattern" : search pattern in commit message
git log -S"pattern"      : search pattern in content
git log --author="author" : search author

## git commit

git commit --reuse-message ORIGIN_HEAD

## git blame

git blame -L 1,10 file

## save old file

git show HEAD^:main.cpp > old_main.cpp


