# quickstarts

Репозиторий содержит готовые конфигурации запуска всей платформы.

## docker compose (local)

### Для запуска в докере необходимо:
1. Убедиться, что порты `20000—20100` свободны
1. Перейти в директорию `00-docker-local`
1. Создать файл `.env.local` (скопировать `.env` и назвать его `.env.local`)
1. Опционально. Указать теги образов приложений (`DENJI_TAG`, `POWER_TAG`, ...)
1. Указать абсолютный путь до ssl-сертификата для домена `localhost` (`LOCALHOST_PFX_PATH`) и пароль (`LOCALHOST_PFX_PASSWORD`)
1. Запустить compose `docker compose --env-file .env.local up -d`

### Для проверки работоспособности (oauth 2.0 implicit flow):
1. Создать тестовые данные: `curl -IX POST https://localhost:20000/api/private/configuration/seed`
1. Запустить в [инкогнито-]браузере процесс авторизации, открыв ссылку: `https://localhost:20000/connect/authorize?client_id=implicit&redirect_uri=http%3A%2F%2Flocalhost%3A10000&response_type=token&scope=beam.read&state=abc&nonce=xyz`
1. После регистрации и согласия на доступ к данным получаем в адресной строке access_token

Лучше использовать режим инкогнито, так как приложения создают cookie, которые привязаны к домену localhost и их нужно периодически чистить.

Остановить и удалить всё: `docker compose down -v`

### Как сгенерировать ssl-сертификат для localhost

Один из вариантов — использовать dotnet sdk:
1. Создать сертификат и экспортировать его: `dotnet dev-certs https -ep /Users/dk/.aspnet/https/localhost.pfx -p localhost`
1. Сделать сертификат доверенным: `dotnet dev-certs https --trust`

В случае проблем, можно удалить сертификаты и затем выполнить команды выше заново: `dotnet dev-certs https --clean`

Так же, можно использовать любой другой вариант генерации сертификатов, например, утилиту `openssl`.

## helm (local)

### denji
```
helm install -f denji-overrides.yaml denji /Users/dk/Repos/yaiam/charts/charts/denji
helm upgrade -f denji-overrides.yaml denji /Users/dk/Repos/yaiam/charts/charts/denji
helm uninstall denji
```

### power
```
helm install -f power-overrides.yaml power /Users/dk/Repos/yaiam/charts/charts/power
helm upgrade -f power-overrides.yaml power /Users/dk/Repos/yaiam/charts/charts/power
helm uninstall power
```

### cosmo
```
helm install -f cosmo-overrides.yaml cosmo /Users/dk/Repos/yaiam/charts/charts/cosmo
helm upgrade -f cosmo-overrides.yaml cosmo /Users/dk/Repos/yaiam/charts/charts/cosmo
helm uninstall cosmo
```

### beam
```
helm install -f beam-overrides.yaml beam /Users/dk/Repos/yaiam/charts/charts/beam
helm upgrade -f beam-overrides.yaml beam /Users/dk/Repos/yaiam/charts/charts/beam
helm uninstall beam
```