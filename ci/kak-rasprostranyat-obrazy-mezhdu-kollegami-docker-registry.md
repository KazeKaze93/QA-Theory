# Как распространять образы между коллегами (docker registry)

Для совместного использования Docker-образов между коллегами используют **Docker Registry** — централизованное хранилище образов.

***

#### **1. Публичные и приватные регистры**

* **Docker Hub** — публичный (есть бесплатные и платные приватные репозитории).
* **GitHub Container Registry / GitLab Registry** — встроенные регистры в платформу.
* **Собственный приватный регистр** — `docker registry` на сервере компании.

***

#### **2. Процесс распространения образа**

1. **Авторизация в регистре**:

```bash
docker login
```

* Вводим логин и пароль для Docker Hub или другого регистра.

2. **Тэгирование образа**:

```bash
docker tag myapp:latest username/myapp:latest
```

* `username` — ваш логин в регистре.

3. **Публикация (push) в регистр**:

```bash
docker push username/myapp:latest
```

4. **Скачивание (pull) коллегой**:

```bash
docker pull username/myapp:latest
```

***

#### **3. Собственный приватный регистр**

* Можно поднять с помощью образа `registry`:

```bash
docker run -d -p 5000:5000 --name registry registry:2
```

* Публикация в локальный регистр:

```bash
docker tag myapp:latest localhost:5000/myapp:latest
docker push localhost:5000/myapp:latest
```

* Коллеги подтягивают:

```bash
docker pull localhost:5000/myapp:latest
```

***

#### **4. Преимущества**

* Централизованное хранение образов.
* Возможность версионирования (теги).
* Быстрое распространение между командами и серверами.

***

Итог: **Docker Registry используется для хранения и обмена образами**, а команды `docker tag`, `docker push` и `docker pull` позволяют легко публиковать и получать образы между коллегами.
