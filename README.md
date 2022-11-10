# yamdb_final
![yamdb](https://github.com/ilshat2/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

YAMDB собирает отзывы пользователей на произведения в категориях «Книги», «Фильмы», «Музыка». Проект представляет собой web-приложение и базу данных, поднятых в двух docker-контейнерах.
При разработке приложения использованы фреймфорки django и django-rest-framework. В качестве базы выступает postgresql Запуск проекта осуществляется средствами docker

## Начало работы

Для запуска проекта на локальной машине в целях разработки и тестирования. See deployment for notes on how to deploy the project on a live system.


### Предварительная подготовка

#### Установка Docker
Установите Docker, используя инструкции с официального сайта:
- для [Windows и MacOS](https://www.docker.com/products/docker-desktop) 
- для [Linux](https://docs.docker.com/engine/install/ubuntu/). Установите [Docker Compose](https://docs.docker.com/compose/install/)

### Установка проекта (на примере Linux)

- Создайте папку для проекта YaMDb `mkdir yamdb` и перейдите в нее `cd yamdb`
- Склонируйте этот репозиторий в текущую папку `git clone https://github.com/ifize/yamdb_final .`.
- Создайте файл `.env` командой `touch .env` и добавьте в него переменные окружения для работы с базой данных:
```sh
DB_NAME=postgres # имя базы данных
POSTGRES_USER=postgres # логин для подключения к базе данных
POSTGRES_PASSWORD=postgres # пароль для подключения к БД (установите свой)
DB_HOST=db # название сервиса (контейнер в котором будет развернута БД)
DB_PORT=5432 # порт для подключения к БД
SECRET_KEY=... # секретный ключ
DEBUG = True # данную опцию следует добавить для отладки
```
- Запустите docker-compose `sudo docker-compose up -d` 
- Примените миграции `sudo docker-compose exec web python manage.py migrate`
- Соберите статику `sudo docker-compose exec web python manage.py collectstatic --no-input`
- Создайте суперпользователя Django `sudo docker-compose exec web python manage.py createsuperuser --email 'admin@yamdb.com'`
## Примеры эндпоинтов
- Создать пользователя        /api/v1/auth/signup/
```
{ "email": "string", "username": "string" }
```
- Получить Jwt Token      /api/v1/auth/token/
```
{ "username": "string", "confirmation_code": "string" }
```
- Категории      /api/v1/categories/
- Жанры         /api/v1/genres/
- Произведения         /api/v1/titles/
- Отзывы        /api/v1/titles/1/reviews/
- Комментарии       /api/v1/titles/1/reviews/1/comments/
- Пользователи          /api/v1/users/

