# Как настроить Job или Pipeline на знакомом вам CI-инструменте?

Рассмотрим пример настройки **Pipeline и Job** на популярном CI-инструменте **GitLab CI/CD**, так как он часто используется в корпоративной разработке.

***

#### **1. Создаём файл `.gitlab-ci.yml`**

Файл находится в корне репозитория и описывает pipeline и job.

```yaml
# Определяем стадии (stages)
stages:
  - build
  - test
  - deploy

# Job для сборки
build_job:
  stage: build
  image: python:3.11
  script:
    - pip install -r requirements.txt
    - python setup.py build
  artifacts:
    paths:
      - dist/

# Job для тестирования
test_job:
  stage: test
  image: python:3.11
  script:
    - pip install -r requirements.txt
    - pytest tests/

# Job для деплоя (пример на staging)
deploy_job:
  stage: deploy
  script:
    - echo "Deploying to staging server..."
  when: manual   # запуск вручную
```

***

#### **2. Как это работает**

1. **Pipeline** запускается при каждом коммите в ветку (по умолчанию `push`).
2. Pipeline состоит из **трёх стадий** (`stages`): `build`, `test`, `deploy`.
3. В каждой стадии выполняется **Job**:
   * `build_job` — собирает проект, создаёт артефакты.
   * `test_job` — запускает автоматические тесты.
   * `deploy_job` — выполняет деплой (можно ручной через `when: manual`).
4. Jobs внутри одной стадии могут выполняться **параллельно**, стадии выполняются **последовательно**.

***

#### **3. Дополнительные возможности**

* **Кэширование зависимостей** для ускорения сборки:

```yaml
cache:
  paths:
    - .venv/
```

* **Использование разных образов Docker** для job через `image`.
* **Ограничение запуска job на конкретной ветке**:

```yaml
only:
  - main
```

***

Итог:

* **Pipeline** — это последовательность стадий для автоматизации CI/CD.
* **Job** — отдельная задача, выполняемая на агенте CI/CD.
* Настройка производится в файле `.gitlab-ci.yml`, где указываются стадии, скрипты, зависимости, артефакты и условия запуска.
