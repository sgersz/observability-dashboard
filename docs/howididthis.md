✅ 1. Deploy Prometheus
	•	Installed Prometheus via Unraid’s Community Applications
	•	Mapped /mnt/user/appdata/prometheus/ as config folder
	•	Exposed port 9090
	•	Created a custom prometheus.yml:

global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'node_exporter'
    static_configs:
      - targets: ['<UNRAID_IP>:9100']

  - job_name: 'cadvisor'
    static_configs:
      - targets: ['<UNRAID_IP>:8080']
(Replace <UNRAID_IP> with actual IP)

✅ This config tells Prometheus to scrape metrics every 15 seconds from node_exporter and cAdvisor.
✅ 2. Deploy node_exporter
	•	Installed node_exporter as a Docker container via Community Apps
	•	Exposed port 9100
	•	Confirmed it was reachable at http://<UNRAID_IP>:9100/metrics

👉 This exporter collects host metrics (CPU, memory, disk, etc.)

⸻

✅ 3. Deploy cAdvisor
	•	Installed cAdvisor as a Docker container
	•	Exposed port 8080
	•	Confirmed it was reachable at http://<UNRAID_IP>:8080/metrics

👉 This exporter collects Docker container metrics for all containers running on Unraid.

⸻

✅ 4. Deploy Grafana
	•	Installed Grafana via Community Applications
	•	Exposed port 3000
	•	Mapped /mnt/user/appdata/grafana/ as config folder
	•	Logged into Grafana (admin/admin by default)

Added Prometheus as a data source (URL: http://<UNRAID_IP>:9090)

⸻

✅ 5. Import Dashboards

Imported existing Grafana dashboards from Grafana Labs:
	•	Node Exporter Full (ID 1860)
	•	Docker Containers Overview (ID 14282)

✅ Dashboards auto-populated with metrics from Prometheus.

🔍 What This Setup Monitors:
	•	Host metrics: CPU, memory, disk, network for Unraid server
	•	Docker container metrics: per-container CPU, memory, network I/O
	•	Uptime and container statuses
	•	Optional: Can be extended with alerting or logging integrations
