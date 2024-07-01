
## local built-in server

```bash
php -S localhost:8000
```

## docker access from inside container

```bash
php -S 0.0.0.0:8000
curl http://host.docker.internal
```

## print all header to server log

```php
foreach (getallheaders() as $name => $value) {
    error_log(print_r("$name: $value", true));
}
```
