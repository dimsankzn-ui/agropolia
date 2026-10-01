# Агрополия

Production-проект «Агрополия». Источник требований — ФТЗ и принятые архитектурные поправки в `docs/`.

## I-0: локальный запуск

```bash
cp .env.example .env
docker compose up --build
```

После запуска:

- client: http://localhost:5173
- API: http://localhost:8000
- OpenAPI: http://localhost:8000/docs
- NATS monitoring: http://localhost:8222

Миграции выполняются отдельной командой:

```bash
docker compose run --rm backend-api alembic upgrade head
```

Development OTP задаётся `AGROPOLIA_DEV_OTP_CODE`; значение разрешено возвращать клиенту только при `AGROPOLIA_ENV=development`.

Документация нулевой итерации: `docs/i-0/`.
