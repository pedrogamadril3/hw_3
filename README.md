Проверка счетчика
запрос начального значения:

    curl http://127.0.0.1:8080/

Ответ:

    {"greeting": "Hello", "count": 0, "hostname": "eb457d7f820c", "storage": "sqlite"}

Увеличил счетчик с 0 до 1 запросом POST /increment:

    curl -X POST http://127.0.0.1:8080/increment

Ответ:

    {"greeting": "Hello", "count": 1, "hostname": "eb457d7f820c", "storage": "sqlite"}

Посмотрел логи:

    sudo docker compose logs app

Ответ:

    app-1  | 2026-11-22 18:53:46,789 listening port=8000 storage=sqlite
    app-1  | 2026-11-22 18:54:21,587 http 172.18.0.1 "GET / HTTP/1.1" 200 -
    app-1  | 2026-11-22 19:11:35,211 http 172.18.0.1 "POST /increment HTTP/1.1" 200 -

Проверка сохранения счетчика после удаления контейнера:
    Удалил контейнер:

        sudo docker compose down

    Запустил новый контейнер и запросил значение счётчика:

        sudo docker compose up -d
        curl http://127.0.0.1:8080/

    Ответ:

        {"greeting": "Hello", "count": 1, "hostname": "d6a2c990ceb1", "storage": "sqlite"}

    После пересоздания контейнера hostname изменился с eb457d7f820c на d6a2c990ceb1, счетчик сохранил значение 1.

Запуск через Docker Compose
При первом запуске из корня проекта надо скопировать пример настроек:

    cp .env.example .env

В файле ".env" можно изменить "HOST_PORT" - порт на компьютере и "GREETING" - текст приветствия:
Соберите образ и запустите приложение:

    sudo docker compose up -d --build

