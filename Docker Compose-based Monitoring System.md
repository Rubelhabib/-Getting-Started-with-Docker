# 🖥️ Docker-Based Monitoring Stack (Prometheus + Grafana + Node Exporter)

This project offers a complete monitoring system that runs easily with **Docker Compose**. It mainly includes 3 core components:

* **Prometheus** – Collects time-based metrics
* **Node Exporter** – Collects system metrics from the host machine
* **Grafana** – Visualizes data collected by Prometheus

---

| Service           | Functionality                                                                                                                      | Access Port                    |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------- | ------------------------------ |
| **Prometheus**    | Collects and stores metrics from exporters.<br>Fetches data from Node Exporter.<br>Provides capabilities for storage and analysis. | `http://localhost:9090`        |
| **Node Exporter** | Provides host system metrics like CPU, RAM, DISK, Network, etc.                                                                    | **internally** on port `9100`  |
| **Grafana**       | Displays Prometheus data visually.<br>Presents data in interactive dashboards.                                                     | `http://localhost` (80 → 3000) |

---

## 📟 File Overview

### 📂 `docker-compose.yaml`

Defines 3 services:

* **node-exporter** – Collects host system data
* **prometheus** – Collects and stores that data
* **grafana** – Visualizes that data

Also creates:

* A custom network (`monitoring`)
* A volume (`prometheus_data`) for Prometheus

### 📂 `prometheus.yml`

Prometheus configuration includes:

* ⏩ Scrape data every 5 seconds
* Target: `node-exporter:9100`

---

## 🚀 Getting Started

### 1. 🐳 docker-compose.yaml Explanation (line-by-line in English)

#### 🔗 Create Network:

```yaml
networks:
  monitoring:
    driver: bridge
```

▶️ Creates a custom bridge network named `monitoring` so all containers can identify each other using DNS.

#### 💾 Create Volume:

```yaml
volumes:
  prometheus_data: {}
```

▶️ Creates a Docker volume named `prometheus_data` to persist Prometheus data.

### 🔧 Services: node-exporter, prometheus, grafana

#### 🔹 node-exporter Service:

```yaml
  node-exporter:
```

▶️ Collects metrics from the host system.

```yaml
    image: prom/node-exporter:latest
```

▶️ Uses Prometheus official node-exporter image.

```yaml
    container_name: node-exporter
```

▶️ Names the container as node-exporter.

```yaml
    restart: unless-stopped
```

▶️ Auto-restarts unless manually stopped.

```yaml
    volumes:
      - /proc:/host/proc:ro
      - /sys:/host/sys:ro
      - /:/rootfs:ro
```

▶️ Mounts host's `/proc`, `/sys`, and `/` filesystem as read-only into the container.

```yaml
    command:
      - '--path.procfs=/host/proc'
      - '--path.rootfs=/rootfs'
      - '--path.sysfs=/host/sys'
      - '--collector.filesystem.mount-points-exclude=^/(sys|proc|dev|host|etc)($$|/)'
```

▶️ Sets collection paths and exclusions for the exporter.

```yaml
    expose:
      - 9100
```

▶️ Opens internal port 9100 (Prometheus will scrape from here).

```yaml
    networks:
      - monitoring
```

▶️ Joins the monitoring network.

---

#### 🔹 prometheus Service:

```yaml
  prometheus:
```

▶️ Prometheus server that collects and stores metrics.

```yaml
    image: prom/prometheus:latest
```

▶️ Uses the official Prometheus image.

```yaml
    container_name: prometheus
```

▶️ Names the container as prometheus.

```yaml
    restart: unless-stopped
```

▶️ Automatically restarts unless manually stopped.

```yaml
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
      - prometheus_data:/prometheus
```

▶️ Mounts the Prometheus config file and uses a Docker volume for persistent storage.

```yaml
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'
      - '--web.console.libraries=/etc/prometheus/console_libraries'
      - '--web.console.templates=/etc/prometheus/consoles'
      - '--web.enable-lifecycle'
```

▶️ Passes flags to set config path, storage location, enable web interface, etc.

```yaml
    expose:
      - 9090
```

▶️ Opens internal port 9090 for Prometheus UI/API.

```yaml
    networks:
      - monitoring
```

▶️ Joins the monitoring network.

---

#### 🔹 grafana Service:

```yaml
  grafana:
```

▶️ Grafana visualizes Prometheus metrics in dashboards.

```yaml
    image: grafana/grafana
```

▶️ Uses the official Grafana image.

```yaml
    container_name: grafana
```

▶️ Names the container as grafana.

```yaml
    restart: unless-stopped
```

▶️ Auto-restarts unless manually stopped.

```yaml
    networks:
      - monitoring
```

▶️ Joins the monitoring network.

```yaml
    ports:
      - 80:3000
```

▶️ Maps host port 80 to container's 3000 (default Grafana port).

---

## 📄 prometheus.yml Explanation

```yaml
global:
  scrape_interval: 5s
```

▶️ Prometheus scrapes data every 5 seconds.

```yaml
scrape_configs:
```

▶️ List of sources Prometheus will collect data from.

```yaml
  - job_name: 'node'
```

▶️ Names this job 'node' (you will see this in Grafana).

```yaml
    static_configs:
      - targets: ['node-exporter:9100']
```

▶️ Prometheus collects metrics from node-exporter on port 9100.

---

| Service           | Role                                   |
| ----------------- | -------------------------------------- |
| **Node Exporter** | Collects host metrics (CPU, RAM, Disk) |
| **Prometheus**    | Stores and manages collected metrics   |
| **Grafana**       | Visualizes those metrics in dashboard  |
