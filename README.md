# Helm Charts Repository

This repository contains a collection of Helm charts. The charts are automatically packaged and published to GitHub Pages, making it easy to use them in your Kubernetes clusters.

## Available Charts

Currently, this repository includes the following chart:

- **postgresql**: A Helm chart to deploy PostgreSQL with optional backup to Nextcloud.

## Using the Charts

To use these charts in your Kubernetes cluster, follow these steps:

1. Add this Helm repository to your Helm installation:

   ```bash
   helm repo add l4r-s-charts https://l4r-s.github.io/helm-charts/
   ```

2. Update your local Helm chart repository cache:

   ```bash
   helm repo update
   ```

3. Install a chart, for example, the PostgreSQL chart:

   ```bash
   helm install my-postgres l4r-s-charts/postgresql
   ```

## PostgreSQL Chart

The PostgreSQL chart deploys a PostgreSQL database with the following features:

- Configurable resource requests and limits
- Persistent volume claim for data storage
- Optional backup to Nextcloud using a CronJob

### Configuration

To configure the PostgreSQL deployment, you can override the default values in `values.yaml`. Here are some important configuration options:

- `secret_name`: Name of the Kubernetes secret containing PostgreSQL credentials
- `db_name`: Name of the PostgreSQL database to create
- `storage_size`: Size of the persistent volume claim
- `image`: PostgreSQL Docker image to use
- `resources`: CPU and memory requests and limits
- `enable_backup`: Enable or disable the backup CronJob
- `backup_schedule`: Cron schedule for backups
- `keepBackups`: Number of backups to retain in Nextcloud
- `nextcloud`: Configuration for Nextcloud backup destination

For more details on configuration options, please refer to the `values.yaml` file in the `postgresql` directory.

### Secrets

Before deploying the PostgreSQL chart, you need to create two Kubernetes secrets:

1. PostgreSQL credentials:

   ```bash
   kubectl create secret generic postgres-secret --from-literal=postgres-username=root --from-literal=postgres-password=password -n <namespace>
   ```

2. Nextcloud credentials (if using backup feature):

   ```bash
   kubectl create secret generic nextcloud-credentials --from-literal=username=<your-nextcloud-username> --from-literal=password=<your-nextcloud-password> --namespace <your-namespace>
   ```

## Contributing

To contribute to this repository:

1. Fork the repository
2. Create a new branch for your changes
3. Make your changes and commit them
4. Push your changes to your fork
5. Create a pull request

## Automatic Deployment

This repository uses GitHub Actions to automatically package and deploy the Helm charts to GitHub Pages. When changes are pushed to the `main` branch, the workflow will:

1. Check out the repository
2. Set up Helm
3. Package all Helm charts in the repository
4. Generate a Helm repository index
5. Deploy the packaged charts and index to GitHub Pages

The packaged charts are then available at `https://l4r-s.github.io/helm-charts/`.

## License

This project is licensed under the [MIT License](LICENSE).
