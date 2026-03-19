# 📊 Observability Stack with Docker (Prometheus + Grafana + Loki)

## Overview 

This project provides a complete observability stack using Docker Compose, combining metrics, logs, and visualization tools in a unified environment  

It includes:  

- Prometheus → Metrics collection
- Node Exporter → System-level metrics
- Grafana → Visualization and dashboards
- Loki → Log aggregation
- Promtail → Log shipping
- Nginx → Example service generating logs

This setup is commonly used in modern DevOps and cloud-native environments.

## 🧩 Architecture

The system is composed of the following components: 

* Prometheus scrapes metrics from Node Exporter

* Node Exporter exposes host system metrics (CPU, memory, disk, etc.)  

* Loki stores and indexes logs  

* Promtail collects logs from Docker containers and sends them to Loki  

* Grafana connects to Prometheus and Loki to visualize metrics and logs  

* Nginx acts as a sample service whose logs are monitored  

```mermaid  

flowchart LR
  P[Prometheus]
  NE[Node Exporter]
  G[Grafana]
  L[Loki]
  PT[Promtail]
  N[Nginx]
  S[System]
    
  NE --> P
  P --> G
  PT --> L
  L --> G
  N --> PT
  S --> PT

```

## Features

* Real-time system metrics monitoring

* Custom dashboards with Grafana

* Centralized log aggregation with Loki

* Log exploration and filtering

* Docker-native logging integration

* Easily extendable architecture


## 📁 Project Structure

```text
.
compose.yaml
prometheus.yml
loki-config.yaml
promtail-config.yml
├── web/
│   └── index.html
|   └── images
├── screenshots/

```

## ⚡ QuickStart

1. Clone the repository

```
git clone https://github.com/Ismaelggc/monitoring.git
cd monitoring
```


2. Start the stack

```
docker compose up -d
```


3. Verify services are running

```
docker compose ps
```

All containers should be in Up state.


4. Access services

|Service|URL|
|-------|---|
|Grafana|http://localhost:3000|
|Nginx|http://localhost:8080|
|Prometheus|http://localhost:9090|


5. Grafana login
Username: admin
Password: admin

You will be prompted to change the password on first login.

<p align="center">
  <img src="stack-monitoring/screenshots/Login-change.png" width="400"/>
</p>


6. Configure data sources in Grafana

Inside Grafana:

  - Go to Connections → Data Sources

  - Add:

    * Prometheus URL: http://prometheus:9090

    * Loki URL: http://loki:3100

<p align="center">
  <img src="stack-monitoring/screenshots/DataSourceProm.png" width="800"/>
</p>

7. Importing a Dashboard in Grafana

  - Instead of creating dashboards from scratch, you can import pre-built ones.

  - Go to Grafana → Dashboards

  - Click New → Import

<p align="center">
  <img src="stack-monitoring/screenshots/Importdashboards.png" width="800"/>
</p>

  - Go to Grafana Dashboard Gallery

  - Select Nede Exporter Full

<p align="center">
  <img src="stack-monitoring/screenshots/Dashboard-pull.png" width="800"/>
</p>

  > This is a popular Node Exporter Full dashboard

  - Copy the dashboard ID

  - Click Load

  - Select your Prometheus data source

  - Click Import

<p align="center">
  <img src="stack-monitoring/screenshots/Dashborad.png" width="800"/>
</p>

8. Logs

  - Go to Drilldown

  - Click on Logs

<p align="center">
  <img src="stack-monitoring/screenshots/Logs.png" width="800"/>
</p>

# Use Cases

- Learning DevOps and observability fundamentals

- Monitoring local development environments

- Building a homelab setup

- Demonstrating skills for technical interviews

- Base architecture for production systems

## ⚠️ Notes

* Volumes are used for data persistence

* Do not commit sensitive data or credentials

Ensure ports are available before running

