## db summary

```
select
    table_name,
    table_rows,
    data_length,
    index_length,
    data_length + index_length,
    floor((data_length+index_length)/1024) AS KB,
    floor((data_length+index_length)/1024/1024) AS MB,
    floor((data_length+index_length)/1024/1024/1024) AS GB
from information_schema.tables
where table_schema = database();
```

```
`registered_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '登録日時',
`updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新日時',
```

```
SHOW WARNINGS
```
