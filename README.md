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
### Найдите в файле access.log все упоминания строки "404"
```
grep “404” ./var/logs/access.log // Ищем в файле access.log все совпадение с “404”
```

### На основании файла 404.html сделайте файл 403.html заменив в его содержимом все упоминания 404 на 403
```
sed s/”404”/”403”/g < ./var/www/html/404.html > ./var/www/html/403.html // Копируем содержимое из файла 404.html в буфер, заменяем  строки “404” на строки “403”, и записываем содержимое в новый файл 403.html
```

### Модифицируйте права доступа и владельца файла index.html следующим образом: Текущий пользователь должен иметь права на чтение/запись Группа www-data на чтение Все остальные не имеют доступа к файлу
```
sudo chown :www-data ./var/www/html/index.html // Делаем владельцем группу www-data
chmod 640 ./var/www/html/index.html // Устанавливаем права u=rw, g=r, o=
```

### Сделайте символическую ссылку на файл access.log в папке html.
```
ln -sr ./var/logs/access.log ./var/www/html // Создаем ссылку с относительными путями
```

### Выведите на экран все файлы в папке var
```
find ./var/ -type f -exec cat {} + # Ищем рекурсивно все файлы в папке var и поочередно выводим содержимое на экран
```
