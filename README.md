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
find ./var/ -type f -exec cat {} + // Ищем рекурсивно все файлы в папке var и поочередно выводим содержимое на экран
```

### Создайте новый файл 503.html в папке html с следующим содержимым:
```
<html>
    <head>
        <title>503</title>
    </head>
</html>
```
```
cat ./var/www/html/503.html << EOF
<html>
    <head>
        <title>503</title>
    </head>
</html>
EOF // Записываем в файл 503.html многострочный текст, завершением которого является ключевое слово “EOF”
```
## GIT внесение изменений
### Рабочее окружение
У вас чистая операционная система с установленными программами git, nano, ssh. Ваш публичный ключ уже добавлен к git репозиторию и вы имеете полный доступ на чтение/запись, но он отсутствует на вашем компьютере. Репозиторий: git@example.com:example/test.git Ветки: master, dev, stage, release
Задание
Внести изменения в ветке dev репозитория git@example.com:example/test.git, добавив в корень файл Readme.md с текстом ### May be in future и залить их на удаленный репозиторий. Напишите набор команд для решения этой задачи с комментариями.

---
 
Нам нужно узнать публичный shh ключ от удаленного git репозитория.##
Потом записать его в файл ~/.ssh/id_rsa.pub и при условии, что открытый ключ “совпадает” с нашим закрытым ключом, мы сможем клонировать удаленный репозиторий.
Или сгенерировать новую пару ключей $ ssh-keygen . И добавить публичный ключ на удаленный сервер.

```
git clone git@example.com:example/test.git // Клонируем репозиторий
cd test // Заходим в репозиторий
git branch // Смотрим существующие ветки
git switch dev // Переходим на ветку dev
touch ./Readme.md // Создаем в корне файл Readme.md
nano ./Readme.md // Открываем файл с помощью текстового редактора nano
### May be in future // Вносим изменение в файл
git status // Проверяем есть ли измененные/новые файлы
git add Readme.md // Добавляем файл в index
git commit -m “add Readme.md” // Коммитим изменения
git push -u git@example.com:example/test.git dev // Заливаем изменения на удаленный репозиторий в ветку dev
```

## CSS, HTML
### Опишите все известные вам способы позиционирования 5 элементов по центру, каждый из которых должен занимать 20%.
--- 
Если 5 элементов занимают по 20% ширины родителя, то горизонтальное центрирование им не нужно, они и так растянутся на всю ширину родителя.
Для родителя display: flex; justify-content: center; align-items: center; для дочерних элементов flex-basis: 20%; или width: 20%; height: 20%;
Горизонтальное центрирование с фиксированной шириной можно сделать через margin: 0 auto;
Если inline-block то можно горизонтально центрировать через text-align: center; (убрать пробелы можно задав у родителя font-size: 0;)
 
 
### Опишите все известные вам способы позиционирования модального окна, по центру экрана.
---
 
Можно центрировать через position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%);
 
### Напишите стили для кнопки, которая может иметь несколько состояний: active, disabled, danger. Цвета произвольные.
 ```
  <button class=”btn active”>btn</button>
  <button class=”btn disabled”>btn</button>
  <button class=”btn danger”>btn</button>
.active {background-color: blue}; .disabled {background-color: grey;}; .danger {background-color: red};
```
 
### Сверстайте страницу логина, которая должна содержать только форму с полями email, password.
 
   https://github.com/pavel-kucenko/login-form
   
## JS логика
### Данные для заданий
```
let testData = [1, 2, 1990, 85, 24, "Vasya", "colya@example.com", "Rafshan", "ashan@example.com", true, false];
let testData2 = [1, 2, 1990, 85, 24, 5, 7, 8.1];
let testData3 = [{"name":"Vasya","email":"vasya@example.com","age":20,"skills":{"php":0,"js":-1,"madness":10,"rage":10}},{"name":"Dima","email":"dima@example.com","age":34,"skills":{"php":5,"js":7,"madness":3,"rage":2}},{"name":"Colya","email":"colya@example.com","age":46,"skills":{"php":8,"js":-2,"madness":1,"rage":4}},{"name":"Misha","email":"misha@example.com","age":16,"skills":{"php":6,"js":6,"madness":5,"rage":2}},{"name":"Ashan","email":"ashan@example.com","age":99,"skills":{"php":0,"js":10,"madness":10,"rage":1}},{"name":"Rafshan","email":"rafshan@example.com","age":11,"skills":{"php":0,"js":0,"madness":0,"rage":10}}]
let testData4 = [{"name":"Vasya","email":"vasya@example.com","age":20},{"name":"Dima","email":"dima@example.com","age":34},{"name":"Colya","email":"colya@example.com","age":46},{"name":"Misha","email":"misha@example.com","age":16},{"name":"Ashan","email":"ashan@example.com","age":99},{"name":"Rafshan","email":"rafshan@example.com","age":11},1,2,1990,85,24,"Vasya","colya@example.com","Rafshan","ashan@example.com",true,false,[[[[1,2,1990,85,24,"Vasya","colya@example.com","Rafshan","ashan@example.com",true,false,[{"name":"Rafshan","email":"rafshan@example.com","age":11}]]]]]]
```
### Напишите функцию cloneDeep таким образом, чтобы она была способна клонировать переданный как параметр объект.
```
function cloneDeep(dest, obj) {
  for (let key in obj) {
    dest[key] = obj[key];
  }
  return dest;
}
```
### Свертка. Используйте метод reduce в комбинации с concat для свёртки массива массивов в один массив, у которого есть все элементы входных массивов.
```
var arrays = [[1, 2, 3], [4, 5], [6]];

let a = arrays.reduce(function(prev, item) {
  return prev = prev.concat(item);
});

// → [1, 2, 3, 4, 5, 6]
```

### Допустим, у вас есть функция primitiveMultiply, которая в 50% случаев перемножает 2 числа, а в остальных случаях выбрасывает исключение типа MultiplicatorUnitFailure. Напишите функцию, обёртывающую эту, и просто вызывающую её до тех пор, пока не будет получен успешный результат.
```
function MultiplicatorUnitFailure() {}
function primitiveMultiply(a, b) {
  if (Math.random() < 0.5)
    return a * b;
  else
    throw new MultiplicatorUnitFailure();
}
function reliableMultiply(a, b) {
  // Ваш код
}
console.log(reliableMultiply(8, 8));
```
---
```
function MultiplicatorUnitFailure(message) {
	this.message = message;
	this.stack = (new Error()).stack;
}
 
MultiplicatorUnitFailure.prototype = Object.create(Error.prototype);
 
function primitiveMultiply(a, b) {
	if (Math.random() < 0.5)
		return a * b;
	else
		throw new MultiplicatorUnitFailure("Не повезло!");
}
 
function reliableMultiply(a, b) {
	while(true) {
		try {
			return primitiveMultiply(a, b);
		} catch (e) {
			if (e instanceof MultiplicatorUnitFailure)
				console.log(e.message);
			else
				throw e;
		}
	}
}

console.log(reliableMultiply(8, 8));
```
### Расширить прототип Array, добавив к нему метод добавления элемента в начало без использование unshift.
```
var arr = [1, 2, 3];
arr.append(0);
//[0, 1, 2, 3]
```
---
``` 
Array.prototype.append = function(arg) {
  return [arg, ...this];
}
```
### Выведите все элементы массива используя рекурсию.
```
var arr = ['Solnce', 'vishlo', 'iz', 'za', 'tuchi']; 
fuction recuseLog(* Ваши атрибуты *) { } 
recuseLog(arr);
```
---
``` 
function recurseLog(array) { 
  console.log(array.shift());
  if (array.length != 0) {
    recurseLog(array)
  }
}
```
### Написать функцию для выполнения параллельных вычислений без использования Promise.
```
var a = function(one, two) {
  return one + two
}
var b = function() {
  return false;
}
paralell([[a, [1, 2]], [b]], function(results) {
    console.log(results); // [3, false]
});
```
---
Не смог сделать(

### Сделать функцию поиска значений в массиве.
```
Синтаксис: array_find(arr: array, search: string|regex): string|number[]|null
Пример: 
let result = array_find(testData, '/^raf.*/i') // ["Rafshan"]
let result2 = array_find(testData, "Rafshan") // ["Rafshan"]
```
---

``` 
function array_find(arr, search) {
  let result = arr.filter(function(currentValue, index) {
    return search == currentValue;
  })
  return result;
}
```

### Сделать функцию которая обрезает массив до указанного значения.
```
Синтаксис: array_skip_until(arr: array, value: any): any[]
Пример: 
let result = array_skip_until(testData, 2) // [2, 1990, 85, 24, "Vasya", "colya@example.com", "Rafshan", "ashan@example.com", true, false]
let result2 = array_skip_until(testData, "Rafshan") // ["Rafshan", "ashan@example.com", true, false]
let result3 = array_skip_until(testData, "asd") // []
```
---
``` 
 function array_scip_until(arr, value) {
    let result;
    for(i=0; i < arr.length; i++) {
      if (value == arr[i]) {
        result = arr.splice(i);
      } else {
        result = [];
      }
    }
    return result;
  }
  ```
  
### Создать функцию которая нормализует данные в массиве исключая или преобразуя не подходящие.
```
Доступные шаблоны: 
'string' => строки, 
'number' => числа, 
'int' => целые числа, 
'float' => числа с плавающей точкой, 
'bool' => true | false, 
'function' => функция, 
'array' => массив, 
Object => объект {name: 'string'}
Синтаксис: array_normalize(arr: array, shema: string|Object[, transform: bool = false]): any[]
Пример: 
let result = array_normalize(testData4, 'string') // ['Vasya', 'colya@example.com', 'Rafshan', 'ashan@example.com']
let result2 = array_normalize(testData4, 'string', true) // ['1', '2', '1990', '85', '24', 'Vasya', 'colya@example.com', 'Rafshan', 'ashan@example.com']
let result3 = array_normalize(testData4, {age: 'float'}) // []
let result4 = array_normalize(testData4, {age: 'float'}, true) // [{age: 20}, {age: 34}, {age: 46}, {age: 16}, {age: 99}, {age: 11}]
```
Не смог сделать(

### Сделать функцию которая возвращает уникальные элементы массива.
```
Синтаксис: array_unique(arr: array): any[]
Пример:
let result = array_unique(testData.concat(testData2)) // [1, 2, 1990, 85, 24, 5, 7, 8.1, "Vasya", "colya@example.com", "Rafshan", "ashan@example.com", true, false]
```
---
``` 
function array_unique(arr) {
  let result = [...new Set(arr)];
  return result;
}
```
### Сделать функцию которая сможет делать срез данных с ассоциативного массива.
 ```
Синтаксис: array_pluck(arr: array, path: string): any[]
Пример:
let result = array_pluck(testData3, 'name') // ["Vasya", "Dima", "Colya", "Misha", "Ashan", "Rafshan"]
let result2 = array_pluck(testData3, 'skills.php') // [0, 5, 8, 6, 0, 0]
```
---
``` 
function array_pluck(arr, patch) {
  let result = [];
  for (let key in arr) {
    result.push(arr[key][patch]);
  }
  return result;
}
```
# Создать функцию которая создает объект на основании двух представленных массивов используя один как ключи, а другой как значения. Не подходящие ключи массивов должны быть исключены.
``` 
Синтаксис: array_combine(keys: array, values: array): Object
Пример: 
let result = array_combine(testData, testData2) // {1: 1, 2: 2, 1990: 1990, 85: 85, 24: 24, "Vasya": 5, "colya@example.com": 7, "Rafshan": 8.1, "ashan@example.com": undefined}
```
---
```
function array_combine(keys, values) {
  let result = {};
  for(i=0;i<keys.length;i++) {
    if (typeof(keys[i]) === "string" || typeof(keys[i]) === "number") {
      result[keys[i]] = values[i];
    }
  }
  return result;
}
```


