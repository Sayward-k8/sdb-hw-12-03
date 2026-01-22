## Домашнее задание к занятию «`SQL. Часть 1`» - ` Игонин В.А.`

# Задание 1
Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

# Решение 1

![alt text](https://github.com/Sayward-k8/sdb-hw-12-03/blob/main/img/1.png)

# Задание 2
Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года включительно и стоимость которых превышает 10.00.

# Решение 2

![alt text](https://github.com/Sayward-k8/sdb-hw-12-03/blob/main/img/2.png)

# Задание 3
Получите последние пять аренд фильмов.

# Решение 3

![alt text](https://github.com/Sayward-k8/sdb-hw-12-03/blob/main/img/3.png)

# Задание 4
Одним запросом получите активных покупателей, имена которых Kelly или Willie.

**Сформируйте вывод в результат таким образом:**

  - все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
  - замените буквы 'll' в именах на 'pp'.

# Решение 4

![alt text](https://github.com/Sayward-k8/sdb-hw-12-03/blob/main/img/4.png)

# Задание 5*
Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.

# Решение 5

![alt text](https://github.com/Sayward-k8/sdb-hw-12-03/blob/main/img/5.png)

# Задание 6*
Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.

# Решение 6

Сначала я получил значения до @
```sql
 SUBSTRING_INDEX(email, '@', 1)
```
Затем мне нужно было 1 букву сделать большой, а со 2ой буквы маленькими
```sql
(UPPER(LEFT(SUBSTRING_INDEX(email, '@', 1), 1)),LOWER(SUBSTR(SUBSTRING_INDEX(email, '@', 1), 2)))
```
Полученные значения я объединил и назвал username 
```sql
CONCAT(UPPER(LEFT(SUBSTRING_INDEX(email, '@', 1), 1)),LOWER(SUBSTR(SUBSTRING_INDEX(email, '@', 1), 2)))  AS username,
```
Скопировал, но для значений после @
```sql
SELECT email, 
	CONCAT(UPPER(LEFT(SUBSTRING_INDEX(email, '@', 1), 1)),LOWER(SUBSTR(SUBSTRING_INDEX(email, '@', 1), 2)))  AS username,
	CONCAT(UPPER(LEFT(SUBSTRING_INDEX(email, '@', -1), 1)),LOWER(SUBSTR(SUBSTRING_INDEX(email, '@', -1), 2)))  AS domain
FROM customer;
```

![alt text](https://github.com/Sayward-k8/sdb-hw-12-03/blob/main/img/6.png)
