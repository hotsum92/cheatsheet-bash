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

