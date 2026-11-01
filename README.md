# sentry-self-hosted

Наш self-hosted Sentry для сбора ошибок: форк [getsentry/self-hosted](https://github.com/getsentry/self-hosted) (Docker Compose-сборка Sentry) с собственной настройкой почты. Инфраструктура, серверная часть. Новые версии оригинала регулярно вливаются по тегам.

## Что изменено относительно оригинала

Оригинал: https://github.com/getsentry/self-hosted. Сейчас влита версия 26.8.0. Наши изменения затрагивают только два файла:

- `docker-compose.yml`: сервис `smtp` вместо образа exim (`registry.gitlab.com/egos-tech/smtp`) использует `freinet/postfix-relay` с TLS (`TLS_SECURITY_LEVEL=encrypt`) и DKIM (селектор `sentry`). Логи и ключи DKIM монтируются из `/home/postfix/sentry.gravitlauncher.com` на хосте. `SENTRY_MAIL_HOST` задан как `sentry.gravitlauncher.com`.
- `sentry/config.yml`: файл добавлен в репозиторий (в оригинале есть только `config.example.yml`), отправитель писем `Gravit Launcher Sentry <sentry@sentry.gravitlauncher.com>`, хранилище файлов `filesystem`.

Всё остальное совпадает с оригиналом.

## Установка и обновление

Как в оригинале:

```
./install.sh
docker compose up --wait
```

Обновление: влить тег новой версии из `getsentry/self-hosted`, решить конфликты в `docker-compose.yml` (сервис `smtp`), затем снова запустить `./install.sh`. Документация: https://develop.sentry.dev/self-hosted/.

## Оригинальный README

# Self-Hosted Sentry 26.8.0

[Sentry](https://sentry.io/), feature-complete and packaged up for low-volume deployments and proofs-of-concept.

Documentation [here](https://develop.sentry.dev/self-hosted/).
