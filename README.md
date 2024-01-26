# MariaDB Galera Cluster on Kubernetes

This project deploys a highly available MariaDB Galera Cluster on Kubernetes, ensuring that all database engines have the same data and providing high availability in case of node failures.

## Prerequisites

- Kubernetes cluster up and running.
- Helm installed on your local machine.

## Getting Started

### 1. Install Helm

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update

2. Customize Configuration

Edit the values.yaml file to customize the MariaDB and Galera Cluster configurations.

yaml

# values.yaml
# Customize the following values according to your needs

mariadb:
  rootUser:
    password: your-root-password
  db:
    name: your-database-name
    user: your-db-user
    password: your-db-password

galera:
  wsrep:
    clusterAddress: "gcomm://mariadb-galera-0.mariadb-galera-headless,your-service-name.namespace.svc.cluster.local,mariadb-galera-2.mariadb-galera-headless.your-namespace.svc.cluster.local"
  persistence:
    storageClass: your-storage-class
    size: 1Gi

3. Deploy MariaDB Cluster

bash

helm install mariadb-galera bitnami/mariadb-galera -f values.yaml

4. Apply Services

bash

kubectl apply -f galera-service.yaml
kubectl apply -f galera-headless-service.yaml

5. Expose MariaDB Service

Depending on your requirements, expose the MariaDB service using a LoadBalancer or NodePort service.
6. Handle Client Connections

Configure your application or clients to connect to the MariaDB service endpoint.
7. Test High Availability

Test the high availability scenario by intentionally stopping one of the MariaDB pods and ensuring automatic rerouting of clients to available nodes.
Additional Considerations

    Security: Configure secure communication, enable authentication, and set up proper access controls.

    Monitoring: Set up monitoring using tools like Prometheus and Grafana to keep track of the cluster's health.

    Backup and Restore: Implement regular backup strategies to prevent data loss.

Contributing

Feel free to contribute to this project by creating issues or submitting pull requests.
