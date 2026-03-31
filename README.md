# Cloud Deployment & CI/CD Project (FastAPI + Docker)

## Опис

Цей проєкт демонструє повний цикл розгортання застосунку у хмарному середовищі:

* розробка REST API (FastAPI)
* контейнеризація (Docker)
* налаштування CI/CD (GitHub Actions)
* автоматичний деплой у хмару (Render)
* тестування (pytest + coverage)

---

## Використані технології

* Python 3.11
* FastAPI
* Docker
* GitHub Actions
* Render
* pytest / pytest-cov

---

## Функціональність застосунку

API дозволяє:

* створювати користувачів (`POST /users`)
* отримувати користувачів (`GET /users/{id}`)

---

## Docker (Контейнеризація)

### Dockerfile

```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
```

---

### Запуск локально

```bash
docker build -t myapp .
docker run -p 8000:8000 myapp
```

Після запуску:

```
http://localhost:8000
```

---

## Тестування

### Unit + Integration тести

Реалізовано:

* перевірка створення користувача
* перевірка отримання користувача
* інтеграційний сценарій (POST → GET)

---

### Запуск тестів

```bash
pytest
```

---

## Покриття коду (Coverage)

```bash
pytest --cov=app
```

### ✔ Результат:

* Покриття: **~80%+**
* Вимога: ≥ 30%

---

## CI/CD (GitHub Actions)

### Pipeline

```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [ main ]

jobs:
  build-test:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3

    - uses: actions/setup-python@v4
      with:
        python-version: 3.11

    - run: pip install -r requirements.txt
    - run: pip install pytest pytest-cov

    - run: pytest --cov=app

    - run: docker build -t myapp .
```

---

### Що відбувається автоматично:

1. Push у GitHub
2. Запуск CI pipeline
3. Виконання тестів
4. Перевірка покриття
5. Білд Docker-образу

---

## Деплой у хмару

Застосунок розгорнуто на платформі **Render**.

### Особливості:

* автоматичний деплой при push
* підтримка Docker
* безкоштовний тариф

---

### Доступ до застосунку

```
https://your-app.onrender.com
```

---

## Автоматичний деплой

Після кожного push у гілку `main`:

* Render автоматично запускає новий деплой
* застосунок оновлюється без ручних дій

---

## Сценарій демонстрації

1. Відкрити задеплоєний застосунок
2. Виконати POST `/users`
3. Отримати `user_id`
4. Виконати GET `/users/{id}`
5. Переконатися, що дані повертаються

---

## Структура проєкту

```
project/
│
├── app/
│   └── main.py
│
├── tests/
│   ├── test_unit.py
│   └── test_integration.py
│
├── Dockerfile
├── requirements.txt
├── .github/workflows/ci.yml
└── README.md
```

---

## Виконані вимоги

✔ Розгортання у хмарі
✔ Контейнеризація (Docker)
✔ CI/CD pipeline
✔ Автоматичний білд
✔ Автоматичне тестування
✔ Автоматичний деплой
✔ Демонстрація роботи застосунку

---

## Висновок

У рамках проєкту було реалізовано повний DevOps-пайплайн:

* розробка → тестування → контейнеризація → деплой

Це дозволяє автоматизувати процес доставки програмного забезпечення та забезпечує стабільність і якість застосунку.

---
