# Task Manager

This guide explains how to set up a system activity monitoring stack using Prometheus, Node Exporter, and Grafana.

---

# File Structure
```
.
├── README.md
├── Recording.mp4
├── Report.pdf
├── Screenshot.png
└── model.json
```

## Prerequisites

- Ensure Docker is installed on your system. If not, download and install it from [Docker Desktop](https://www.docker.com/products/docker-desktop).

---

## Step 1: Download and Run Prometheus and Node Exporter

### 1.1 Download Prometheus
1. Visit the [Prometheus download page](https://prometheus.io/download/).
2. Download the latest version of Prometheus for your operating system.
3. Extract the downloaded tarball:
   ```bash
   tar -xvf prometheus-*.tar.gz
   mv prometheus-* prometheus
   ```

### 1.2 Download Node Exporter
1. Visit the [Node Exporter download page](https://prometheus.io/download/).
2. Download the latest version of Node Exporter for your operating system.
3. Extract the downloaded tarball:
   ```bash
   tar -xvf node_exporter-*.tar.gz
   mv node_exporter-* prometheus
   ```

### 1.3 Configure Prometheus
1. Open the `prometheus.yml` file in the `prometheus` folder.
2. Add the following job configuration to scrape metrics from Node Exporter:
   ```yaml
   - job_name: "node"
     static_configs:
       - targets: ["localhost:9100"]
     scrape_interval: 1s
   ```

### 1.4 Run Prometheus
1. Navigate to the `prometheus` folder:
   ```bash
   cd prometheus
   ```
2. Start Prometheus with the provided `prometheus.yml` configuration:
   ```bash
   ./prometheus --config.file=prometheus.yml
   ```

### 1.5 Run Node Exporter
1. Open a separate terminal and navigate to the `prometheus` folder:
   ```bash
   cd prometheus
   ```
2. Start Node Exporter:
   ```bash
   ./node_exporter
   ```

---

## Step 2: Install and Run Grafana via Docker

### 2.1 Pull the Grafana Docker Image
Run the following command to pull the Grafana Docker image:
```bash
docker pull grafana/grafana
```

### 2.2 Run the Grafana Container
Start the Grafana container using the following command:
```bash
docker run -d -p 3000:3000 --name=grafana grafana/grafana
```

---

## Step 3: Import the Activity Monitor Dashboard

1. Access Grafana at `http://localhost:3000`.
2. Log in with the default credentials:
   - **Username**: `admin`
   - **Password**: `admin`
3. Import the dashboard:
   - Go to **Dashboards** > **Import**.
   - Upload the `model.json` file or paste its JSON content.
   - Click **Import**.

---

## Conclusion

Once all the steps are completed, Prometheus, Node Exporter, and Grafana will be set up and ready to use with the imported Activity Monitor dashboard. You can now monitor your system's activity in real-time.
