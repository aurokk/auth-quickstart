# quickstarts

## docker (local)

### generate certificates for 
```
dotnet dev-certs https -ep /Users/dk/.aspnet/https/localhost.pfx -p localhost
dotnet dev-certs https --trust
dotnet dev-certs https --clean
```

### start / stop
```
docker compose up -d
docker compose down -v
```

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

### power ui
```
helm install -f power-ui-overrides.yaml power-ui /Users/dk/Repos/yaiam/charts/charts/power-ui
helm upgrade -f power-ui-overrides.yaml power-ui /Users/dk/Repos/yaiam/charts/charts/power-ui
helm uninstall power-ui
```