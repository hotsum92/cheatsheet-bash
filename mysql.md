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

```
SHOW GRANTS FOR 'username'@'%' \G
show variables like '%s3_role%';
```

#### csv

```
  SELECT column1, column2, column3
    FROM table_name
    INTO OUTFILE '/tmp/data.csv'
  FIELDS TERMINATED BY ','
ENCLOSED BY '"'
 ESCAPED BY '"'
   LINES TERMINATED BY '\r\n';
```

```
エラー「ERROR 1290 (HY000): The MySQL server is running with the –secure-file-priv option so it cannot execute this statement」
```

```
mysql> SELECT @@global.secure_file_priv;
```

without sudo

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '';
FLUSH PRIVILEGES;
```

## get relative tables

```
Select FK.TABLE_SCHEMA, FK.TABLE_NAME
From INFORMATION_SCHEMA.REFERENTIAL_CONSTRAINTS As RC
    Join INFORMATION_SCHEMA.TABLE_CONSTRAINTS As PK
        On PK.CONSTRAINT_NAME = RC.UNIQUE_CONSTRAINT_NAME
    Join INFORMATION_SCHEMA.TABLE_CONSTRAINTS As FK
        On FK.CONSTRAINT_NAME = RC.CONSTRAINT_NAME
Where PK.TABLE_SCHEMA = 'dbo'
    And PK.TABLE_NAME = '<target table name>'  
```
