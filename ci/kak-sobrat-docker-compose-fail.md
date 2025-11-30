# Как собрать docker compose файл

**Docker Compose** — это инструмент для **определения и запуска многоконтейнерных приложений** через единый YAML-файл (`docker-compose.yml`).

***

#### **1. Структура docker-compose.yml**

Пример для Python-приложения с базой данных PostgreSQL:

```yaml
version: "3.9"

services:
  app:
    build: .
    container_name: my_app
    ports:
      - "8000:8000"
    volumes:
      - ./app:/app
    depends_on:
      - db

  db:
    image: postgres:15
    container_name: my_db
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydatabase
    ports:
      - "5432:5432"
    volumes:
      - db_data:/var/lib/postgresql/data

volumes:
  db_data:
```

**Объяснение:**

* `services` — отдельные контейнеры (app и db).
* `build` — путь к Dockerfile для сборки образа.
* `image` — образ для использования.
* `ports` — проброс портов.
* `volumes` — маунт директорий или томов.
* `depends_on` — порядок запуска сервисов.
* `volumes:` внизу — именованные тома.

***

#### **2. Сборка и запуск**

В директории с `docker-compose.yml`:

```bash
docker-compose up --build
```

* `--build` — пересобирает образ для сервиса `app`.
* Контейнеры запускаются в интерактивном режиме.

Запуск в фоне:

```bash
docker-compose up -d
```

***

#### **3. Просмотр состояния контейнеров**

```bash
docker-compose ps
```

#### **4. Остановка и удаление контейнеров**

```bash
docker-compose down
```

***

Итог: **docker-compose.yml описывает все сервисы приложения и их связи**, а команда `docker-compose up` собирает образы (если нужно) и запускает контейнеры.
