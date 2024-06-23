## connect docker mysql

```
mysql -h $(hostname -i) -P 3307 -u root
```

## create user table

docker run --rm --name mysql -p 3307:3306 -e MYSQL_ALLOW_EMPTY_PASSWORD=yes mysql

```
create database test;
```

```

create table user (
  id int primary key auto_increment,
  name varchar(255) not null default '',
  email varchar(255) not null default '',
  password varchar(255) not null default '',
  created_at timestamp not null default current_timestamp,
  updated_at timestamp not null default current_timestamp on update current_timestamp
);

```

```

create table login (
  id int primary key auto_increment,
  user_id int not null,
  token varchar(255) not null default '',
  created_at timestamp not null default current_timestamp,
  updated_at timestamp not null default current_timestamp on update current_timestamp,
  constraint fk_user_id foreign key (user_id) references user(id)
);

```

## log all queries

```
show variables like 'general_log';
set global general_log = 'ON';
" /var/lib/mysql/test-host.log
```

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

#### csv export

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
mysql> SELECT @@global.secure_file_priv;
```

without sudo

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '';
FLUSH PRIVILEGES;
```

#### csv import

```
LOAD DATA INFILE '/tmp/data.csv'
INTO TABLE <table_name>
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '\"'
IGNORE 1 LINES
(
  @date,
  @number_of_questions
)
SET
  seq_file_id = 'id'
  number_of_questions = @number_of_questions
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
    And PK.TABLE_NAME = '<target table name>';
```

## mysqldump

```
mysqldump -u root -p --databases <database name> > <file name>.sql
mysqldump <database name> -t where 'id in (1, 2, 3)' > <file name>.sql
```

--extended-insert

## jailer

[jailer](https://github.com/Wisser/Jailer)

##### localhost connection

```
jdbc:mysql://localhost:3307?useSSL=false
```

