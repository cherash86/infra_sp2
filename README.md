# Проект: запуск docker-compose
## Яндекс Практикум. Спринт 15. Финальное задание - запуск docker-compose.
С помощью технологии Docker можно упаковать приложение со всеми зависимостями и окружением в контейнер, сделать это приложение независимым от системы и запустить его на любом устройстве.

Docker позволяет:
- быстро развернуть полную инфраструктуру для тестирования и отладки приложения, не отправляя проект на сервер;
- развернуть выполненный проект на другом компьютере без опасений, что он не запустится.

## Задание
Отправить проект api_yamdb в контейнере, для чего:

- клонировать репозиторий infra_sp2
- сохранить в нём проект api_yamdb
- структуру проекта привести в соответствие с финальным заданием спринта
- равернуть контейнеры в новой структуре и заполнить базу данными
- создать дамп базы данных

## Технологии

Для выполнения задания и правильной работы потребуется использование следущих технологий:

- Python
- Django
- Docker

## Инструкция по запуску

 1. Установить Docker для Вашей операционной системы.
 
2. Клонировать репозиторий на локальный компьютер

   ```bash
   git clone https://github.com/_________/infra_sp2.git
   ```

3. В корневой директории создать файл `.env` согласно примеру:

   ```bash
   DB_ENGINE=django.db.backends.postgresql
   DB_NAME=postgres
   POSTGRES_USER=postgres
   POSTGRES_PASSWORD=postgres
   DB_HOST=db
   DB_PORT=5432
   ```

4. Запустить `docker-compose`

   Выполнить из корневой директории команду:

   ```bash
   docker-compose up -d
   ```

5. Заполнить БД

   Подготовить и выполнить миграции:

   ```bash
   docker-compose exec web python manage.py makemigrations reviews
   docker-compose exec web python manage.py migrate
   ```

6. Подгрузить статику

   ```bash
   docker-compose exec web python manage.py collectstatic
   ```

7. Заполнить БД тестовыми данными

   Для заполнения базы использовать файл `fixtures.json`, в директории `infra_sp2`. Выполните команду:

   ```bash
   docker-compose exec web python manage.py loaddata fixtures.json
   ```

8. Создать суперпользователя

   ```bash
   docker-compose exec web python manage.py createsuperuser
   ```

9. Остановить работу всех контейнеров

   ```bash
   docker-compose down
   ```

10. Пересобрать и запустить контейнеры

    ```bash
    docker-compose up -d --build
    ```

11. Мониторинг запущенных контейнеров

    ```bash
    docker stats
    ```

12. Остановить и удалить контейнеры, тома и образы

    ```bash
    docker-compose down -v
    ```

- ✨Magic ✨

Автор 
- Черашкин Александр
