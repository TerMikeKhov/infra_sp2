# Проект infra_sp2

## Описание

* Проект infra_sp2 упаковывает приложение api_yamdb в контейнеры Docker и настраивает взаимодействие контейнеров в Docker Compose. Так же в проекте заменена база данных на PostgreSQL и сервер разработчика заменен на взаимодействие двух серверов NGINX и Gunicorn. NGINX отвечает за раздачу статики и первичном приеме пользователей, а Gunicorn обеспечивает взаимодействие NGINX и Django. 

## Использованные технологии

* Python 3.9
* Django 2.2.16
* Django Rest Framework 3.12.4
* Simple-JWT 4.7.2
* Docker
* Docker Compose
* Nginx
* Gunicorn

## Установка

### Как запустить проект:

Клонировать репозиторий и перейти в него в командной строке:

```
git clone https://github.com/TerMikeKhov/infra_sp2.git
```

```
cd infra_sp2/infra/
```

Запустить рзвертывание проета в нескольких контенерах Docker путем запуска инструкций файла docker-compose.yaml

```
docker-compose up -d --build
```

Выполнить миграции
```
docker-compose exec web python manage.py migrate
```

```
docker-compose exec web python manage.py collectstatic --no-input 
```


Теперь проект доступен по адресу http://localhost/

Для остановки работы контейнеров и их удаления выполнить в командной строке:
```
docker-compose down -v
```

## Наполнение базы данных из файла с фикстурами

Для наполнения базы данных из файла с фикстурами необходимо выполнить следующие шаги:

1. До запуска проекта нужно скопировать файл с фикстурами fixtures.json в папку api_yamdb.

2. После запуска проета  выполнить комманду:

```
docker-compose exec web python manage.py loaddata fixtures.json
```

## Примеры

### Примеры запросов к API:

### Регистрация нового пользователя

POST запрос на адрес
http:/localhost/api/v1/auth/signup/

```
{

    "email": "string",
    "username": "string"

}
```

### Получение JWT-токена

POST запрос на адрес
http:/localhost/api/v1/auth/token/

```
{

    "username": "string",
    "confirmation_code": "string"

}
```


### Получение списка всех произведений

GET запрос на адрес
http://localhost/api/v1/titles/


Ответ API:

```
[

{

    "count": 0,
    "next": "string",
    "previous": "string",
    "results":
                        [
                        ......
                        ]
    }

]
```

### Добавление произведения

POST запрос на адрес
http://localhost/api/v1/titles/

Текст запроса:

```
{
  "name": "string",
  "year": 0,
  "description": "string",
  "genre": [
    "string"
  ],
  "category": "string"
}
```



### Более подробная документация API с примерами размещена по адресу:
http://localhost/redoc/

## Автор

* Терехов Михаил
