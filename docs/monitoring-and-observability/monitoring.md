# Helm Chart Installation Guide

This README provides instructions for installing MySQL, Prometheus, and Grafana using Helm charts. This setup assumes you have Helm installed and configured in your Kubernetes cluster.

## Prerequisites

1. Kubernetes cluster
2. Helm installed and configured
3. Access to Docker Registry

## Installation Steps

### 1. Install MySQL
To install MySQL with specific configurations, run the following command:

```bash
helm install mysql oci://registry-1.docker.io/bitnamicharts/mysql \
    --set auth.username=grafana \
    --set auth.password=grafana \
    --set auth.database=grafana
```
For more options and detailed configurations, please refer to the https://artifacthub.io/packages/helm/bitnami/mysql.

    Configuration Parameters:

    auth.username: The username for MySQL (set to grafana).
    auth.password: The password for MySQL (set to grafana).
    auth.database: The database name to create (set to grafana).

### 2. Install Prometheus
To install Prometheus, execute the following command:

```bash
helm install prometheus prometheus.tgz \
    --set webapp= \
    --set basicauth.user= \
    --set basicauth.password=
```

Configuration Parameters:

webapp: The web application URL (leave empty if not used).  
basicauth.user: Basic authentication username (leave empty if not used).  
basicauth.password: Basic authentication password (leave empty if not used).
### 3. Install Grafana
To install Grafana and connect it to the Prometheus and MySQL instances, run:

```bash
helm install grafana grafana.tgz \
    --set prometheus.svc=prometheus \
    --set prometheus.namespace=default \
    --set prometheus.port=9090 \
    --set mysql.svc=mysql \
    --set mysql.namespace=default \
    --set mysql.port=3306 \
    --set mysql.user=grafana \
    --set mysql.password=grafana
```
Configuration Parameters:

prometheus.svc: The service name for Prometheus (set to prometheus).  
prometheus.namespace: The namespace for Prometheus (set to default).  
prometheus.port: The port for Prometheus (set to 9090).  
mysql.svc: The service name for MySQL (set to mysql).  
mysql.namespace: The namespace for MySQL (set to default).  
mysql.port: The port for MySQL (set to 3306).  
mysql.user: The MySQL username (set to grafana).  
mysql.password: The MySQL password (set to grafana).  

## Accessing the Applications

After installation, you can access the applications as follows:

MySQL: Connect using a MySQL client with the credentials specified.
Prometheus: Access Prometheus at http://<prometheus-service>:9090.
Grafana: Access Grafana at http://<grafana-service>:3000 (default port). Use the MySQL credentials to connect to the database.