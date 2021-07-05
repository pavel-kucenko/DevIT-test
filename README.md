# DevIT-test
## Linux навигация и поиск
## Файловая структура
```
/
--/var/
----/www/
------/html/
--------/index.html
--------/404.html
--------/.htaccess
----/logs/
------/access.log
```

### Выведите список всех файлов в папке html
```
find ./var/www/html/ -type f // Ищем все файлы в папке html и выводим списком
```
