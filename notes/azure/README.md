# Microsoft Azure

## Login and Multiple Tenants

Log in to Azure with a specific tenant:
```
az login --tenant <tenant-id>
```
Sessions will persist across terminal sessions.

Show all subscriptions and tenants:
```
az account list --output table
```

Show current subscription:
```
az account show --output table
```

Switch subscription:
```
az account set --subscription <subscription-id>
```
