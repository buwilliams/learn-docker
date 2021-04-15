# Project

## Todo

- [ ] Get Postgres version running on arm64 w/ tests
- [ ] Get Clickhouse version running on arm64 w/ tests
- [ ] Get Postgres version running on amd64 w/ tests
- [ ] Get Clickhouse version running on amd64 w/ tests

## Done

- [x] Finish docker tutorial
- [x] Read existing PostHog docker compose
- [x] List PostHog services, images, and sizes (399MB)
    - db -> postgres:12-alpine (156MB)
    - redis -> redis:5-alpine (29.3MB)
    - worker -> python:3.8-slim (107MB)
    - web -> python:3.8-slim (107MB)
- [x] List PostHog Enterprise services, images, and sizes (3.09GB)
    - db -> postgres:12-alpine (156MB)
    - redis -> redis:alpine (32.3MB)
    - clickhouse -> yandex/clickhouse-server (557MB)
    - zookeeper -> wurstmeister/zookeeper (510MB)
    - kafka -> wurstmeister/kafka (438MB)
    - worker -> python:3.8-slim (107MB)
    - web -> python:3.8-slim (107MB)
    - plugins -> posthog/plugin-server:0.15.4 (1.19GB) -> node:14
- Issues for `docker compose -f docker-compose.dev.yml up`
    1. [Error: pg_config executable not found](https://stackoverflow.com/questions/11618898/pg-config-executable-not-found)