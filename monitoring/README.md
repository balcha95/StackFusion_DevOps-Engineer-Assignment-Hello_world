# Monitoring with Prometheus and Grafana

This guide explains the steps to install and configure Prometheus and Grafana for monitoring purposes.

## Install Prometheus

1. Go to the [Prometheus download page](https://prometheus.io/download/) and copy the link for the Linux version of Prometheus.
2. SSH into your server and execute the following commands:

```bash
wget <prometheus-linux-download-link>
tar -zxvf prometheus-2.38.0.linux-amd64.tar.gz
```

3. Create the Prometheus service file by executing the following command:

```bash
sudo vi /etc/systemd/system/prometheus.service
```

4. Copy and paste the following content into the file:

```plaintext
[Unit]
Description=Prometheus Server
Documentation=https://prometheus.io/docs/introduction/overview/
After=network-online.target

[Service]
User=root
Restart=on-failure
ExecStart=/root/prometheus-2.38.0.linux-amd64/prometheus --config.file=/root/prometheus-2.38.0.linux-amd64/prometheus.yml

[Install]
WantedBy=multi-user.target
```

5. Save the file and execute the following commands to start and enable Prometheus:

```bash
sudo systemctl daemon-reload
sudo systemctl start prometheus
sudo systemctl enable prometheus
```

6. Prometheus will now be running on port 9090. Access Prometheus by navigating to `<prometheus-external-ip>:9090` in a web browser.

## Install Grafana

1. Go to the [Grafana download page](https://grafana.com/grafana/download) and select the OSS Edition for Linux.
2. Copy the Linux distribution download link for Red Hat, CentOS, RHEL, and Fedora (64 Bit).
3. SSH into your server and execute the following commands:

```bash
wget <grafana-linux-download-link>
sudo yum install grafana-9.1.2-1.x86_64.rpm
```

4. Start and enable Grafana by executing the following commands:

```bash
sudo systemctl enable grafana-server.service
sudo systemctl start grafana-server.service
```

5. Grafana will now be running on port 3000. Access Grafana by navigating to `<grafana-external-ip>:3000` in a web browser. The default username and password are `admin`.

## Install Node Exporter

1. Go to the [Prometheus download page](https://prometheus.io/download/) and copy the link for the Linux version of Node Exporter.
2. SSH into the server you wish to monitor and execute the following commands:

```bash
wget <node-exporter-linux-download-link>
tar -zxvf node_exporter-1.4.0-rc.0.linux-amd64.tar.gz
```

3. Create the Node Exporter service file by executing the following command:

```bash
sudo vi /etc/systemd/system/node_exporter.service
```

4. Copy and paste the following content into the file:

```plaintext
[Unit]
Description=Prometheus Server
Documentation=https://prometheus.io/docs/introduction/overview/
After=network-online.target

[Service]
User=root
Restart=on-failure
ExecStart=/root/node_exporter-1.4.0-rc.0.linux-amd64/node_exporter

[Install]
WantedBy=multi-user.target
```

5. Save the file and execute the following commands to start and enable Node Exporter:

```bash
sudo systemctl daemon-reload
sudo systemctl start node_exporter
sudo systemctl enable node_exporter
```

6. Node Exporter will now be running, exposing metrics on port 9100.

## Configure Prometheus in Grafana

1. Access Grafana in a web browser using `<grafana-external-ip>:3000`.
2. Click on the "Settings" button, navigate to "Data Sources", and click on "Add Data Source".
3. Select Prometheus as the data source.
4. In the URL field, enter the Prometheus server URL with the port (e.g., `<prometheus-external-ip>:9090`).
5. Click on "Save & Test" to verify that the data source is working.
6. Back in the Grafana interface, you will now see the Prometheus data source created.
