≡ Краткое руководство LittleSocNet

# Описание проекта LittleSocNet

Данное приложение является очень упрощенной социальной сетью. Пользователи этой сети могут публиковать свои посты, оставлять комментарии и подписываться на интересных им авторов других статей. Вот собственно и все. 
Чем богаты ). 
***

## Алгоритм регистрации пользователей:
- Пользователь отправляет запрос с параметром email на /auth/email/.
- YaMDB отправляет письмо с кодом подтверждения (confirmation_code) на адрес email.
- Пользователь отправляет запрос с параметрами email и confirmation_code на /auth/token/, в ответе на запрос ему приходит token (JWT-токен).
- При желании пользователь отправляет PATCH-запрос на /users/me/ и заполняет поля в своём профайле (описание полей — в документации). Подробная API документация находится по адресу /redoc

## Установка
Проект собран в Docker 20.10.06 и содержит три образа:
- web - образ проекта
- postgres - образ базы данных PostgreSQL v 12.04
- nginx - образ web сервера nginx

#### Команда клонирования репозитория:
    git clone https://github.com/19870208/infra_sp2
Для запуска проекта на чистом Django нужно в консоли Bash сначала активировать виртуальное окружение, а потом установить все необходимые компоненты в это окружение.

#### Запуск проекта:
-[Установите Докер](https://code.s3.yandex.net/backend-developer/learning-materials/db.sqlite3.zip)
-Выполнить команду:

    docker pull 19870208/api_yamdb_web:latest

#### Первоначальная настройка Django:
```
- docker-compose exec web python manage.py migrate --noinput
- docker-compose exec web python manage.py collectstatic --no-input
```
#### Загрузка тестовой фикстуры в базу:
Для этого перейдите в консоли в корень проекта и наберите команду:
    
    docker-compose exec web python manage.py loaddata fixtures.json

#### Создание суперпользователя:

    - docker-compose exec web python manage.py createsuperuser
    
#### Заполнение .env:
Чтобы добавить переменную в .env необходимо открыть файл .env в корневой директории проекта и поместить туда переменную в формате имя_переменной=значение. Пример .env файла:

    DB_ENGINE=my_db DB_NAME=db_name POSTGRES_USER=my_user POSTGRES_PASSWORD=my_pass DB_HOST=db_host DB_PORT=db_port

#### Автор:
Владимир Половников. Задание было выполнено в рамках курса от Яндекс.Практикум.