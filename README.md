## Kittygram API

### О проекте

Kittygram — это REST API для управления котами и их достижениями.
Реализованы CRUD-операции, JWT-аутентификация, фильтрация, поиск и пагинация.

---

### Переменные окружения

Перед запуском необходимо создать файл `.env`:

cp .env.example .env

Файл содержит настройки базы данных, секретный ключ и другие параметры проекта.

---

### Пример `.env.example`

SECRET_KEY=django-insecure-change-me-in-production
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1

DB_ENGINE=django.db.backends.sqlite3
DB_NAME=db.sqlite3

ACCESS_TOKEN_LIFETIME_MINUTES=60
REFRESH_TOKEN_LIFETIME_DAYS=1

---

### Запуск проекта

git clone https://github.com/cutiepiaki/kittygram
cd kittygram

cp .env.example .env
docker-compose up --build

---

### Применение миграций

В отдельном терминале:

docker-compose exec web python manage.py migrate

---

### Доступ к API

После запуска проект доступен по адресу:
http://127.0.0.1:8000/

Swagger-документация:
http://127.0.0.1:8000/api/docs/

---

### Аутентификация

Все эндпоинты требуют JWT-токен.

Получение токена:

POST /auth/jwt/create/

Пример запроса:

curl -X POST http://127.0.0.1:8000/auth/jwt/create/ \
-H "Content-Type: application/json" \
-d '{"username": "user", "password": "password"}'

Ответ:

{
  "access": "your_access_token",
  "refresh": "your_refresh_token"
}

Использование токена в запросах:

Authorization: Bearer <access_token>

---

### Пример запроса к API

Получение списка котов:

curl -X GET http://127.0.0.1:8000/cats/ \
-H "Authorization: Bearer <access_token>"

---

### Основные возможности API

* Регистрация и аутентификация пользователей
* Создание, просмотр, редактирование и удаление котов
* Работа с достижениями
* Фильтрация и поиск по котам
* Пагинация результатов

---

### Docker

Проект контейнеризирован:

* `Dockerfile` — сборка backend-приложения
* `docker-compose.yml` — запуск backend и базы данных
