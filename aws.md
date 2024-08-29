```
aws sts get-caller-identity
```

```
aws --version
aws configure list
```

```
aws s3 ls --profile default
```

## s3

```
aws s3 ls bucket/data/
```

```
aws s3 cp test s3://tabdri-sample/seq/SEQ150/yearly/dir/
aws s3 cp --recursive s3://tabdri-sample/seq/SEQ150/yearly/ ./dir
```

```
aws s3 rm --recursive s3://tabdri-sample/seq/SEQ150/yearly/dir/
```

## logs

```
aws logs describe-log-groups
```

```
aws logs tail --follow
```


aws logs filter-log-events --log-group-name [ロググループ名] [その他オプション]
sqs
lambda


## 時間の指定
  --start-time "$(date --date='15minutes ago' +%s%3N)"

# 相対時間指定
$ date --date='15minutes ago' +%s%3N

# 絶対時間指定
$ date --date='2022-07-05 17:30:10' +%s000
