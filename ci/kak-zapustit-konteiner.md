# Как запустить контейнер?

Запуск контейнера в Docker выполняется командой `docker run`, которая создаёт и запускает контейнер из образа.

***

#### **Базовая команда**

```bash
docker run <image_name>
```

* `<image_name>` — имя образа, например `myapp:latest`.

***

#### **Часто используемые опции**

1. **-d** — запуск в фоне (detached mode):

```bash
docker run -d myapp:latest
```

2. **--name** — задать имя контейнера:

```bash
docker run -d --name my_container myapp:latest
```

3. **-p** — проброс портов между хостом и контейнером:

```bash
docker run -d -p 8080:80 myapp:latest
```

* Сервис внутри контейнера слушает порт 80, а снаружи доступен на 8080.

4. **-v** — подключение томов (volumes) для хранения данных:

```bash
docker run -d -v /host/path:/container/path myapp:latest
```

5. **-it** — интерактивный режим с терминалом (для командной работы внутри контейнера):

```bash
docker run -it myapp:latest /bin/bash
```

***

#### **Просмотр запущенных контейнеров**

```bash
docker ps
```

#### **Остановка контейнера**

```bash
docker stop my_container
```

#### **Удаление контейнера**

```bash
docker rm my_container
```

***

Итог: **`docker run` создаёт и запускает контейнер из образа**, а опции позволяют настроить порты, тома, режим работы и имя контейнера.
