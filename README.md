# auth-quickstart

## Commands
```
docker compose up -d
docker compose down -v
```

## https && kestrel
```
dotnet dev-certs https -ep /Users/dk/.aspnet/https/localhost.pfx -p localhost
dotnet dev-certs https --trust
dotnet dev-certs https --clean
```