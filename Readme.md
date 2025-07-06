# Order Monorepo

## Клонирование репозитория с сабмодулями

```bash
git clone --recurse-submodules https://github.com/Sanchir01/order-monorepo.git
cd order-monorepo
```

Если уже клонировали без сабмодулей:

```bash
git submodule update --init --recursive
```

---

## Backend (order-service)

### Установка зависимостей

```bash
cd order-service
go mod download
```

### Запуск через Docker Compose (рекомендуется)

```bash
docker-compose up --build -d or make docker
```

### Применение миграций (PostgreSQL)

Если контейнеры уже запущены, примените миграции:

```bash
# В отдельном терминале
cd order-service
# Пример для golang-migrate (если используется):
make migrations-up
```

---

## Frontend (order-service-front)

### Установка зависимостей

```bash
cd ../order-service-front
pnpm install # или npm install
```

### Запуск

```bash
pnpm dev # или npm run dev
```

---

## Запуск через Docker (опционально)

### Backend

```bash
cd order-service
docker build -t order-service .
docker run --env-file ./config/dev.env -p 8080:8080 order-service
```

### Frontend

```bash
cd ../order-service-front
docker build -t order-service-front .
docker run -p 3000:3000 order-service-front
```

---

## Примечания

- Проверьте настройки подключения к БД в `order-service/config/dev.yaml`.
- Для работы миграций нужен установленный [golang-goose](https://github.com/pressly/goose).
- Для запуска фронта нужен установленный [pnpm](https://pnpm.io/) или npm.
