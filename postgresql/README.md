# Backup to Nextcloud

## Configuration
To create the necessary Kubernetes secrets for the postgresql credentials, use the following `kubectl` command:

```bash
kubectl create secret generic postgres-secret --from-literal=postgres-username=root --from-literal=postgres-password=password -n <namespace>
```

## Backup to Nextcloud
To create the necessary Kubernetes secrets for the Nextcloud credentials, use the following `kubectl` command:

```bash
kubectl create secret generic nextcloud-credentials --from-literal=username=<your-nextcloud-username> --from-literal=password=<your-nextcloud-password> --namespace <your-namespace>
```
    