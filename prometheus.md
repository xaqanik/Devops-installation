# How to Install Prometheus on Debian/Ubuntu

## 1. Create a System User

For security purposes, we'll create a dedicated system user for Prometheus:

```bash
sudo useradd --no-create-home --shell /bin/false prometheus
```

## 2. Download and Install Prometheus

Download the latest version of Prometheus from the official website. You can check the latest version here: https://prometheus.io/download/

```bash
curl -LO https://github.com/prometheus/prometheus/releases/download/v2.37.0/prometheus-2.37.0.linux-amd64.tar.gz
```

Extract the downloaded archive:

```bash
tar xvf prometheus-2.37.0.linux-amd64.tar.gz
```

Move the binaries to `/usr/local/bin`:

```bash
sudo mv prometheus-2.37.0.linux-amd64/prometheus /usr/local/bin/
sudo mv prometheus-2.37.0.linux-amd64/promtool /usr/local/bin/
```

## 3. Configure Prometheus

Create a directory for the Prometheus configuration files:

```bash
sudo mkdir /etc/prometheus
```

Move the configuration file to the new directory:

```bash
sudo mv prometheus-2.37.0.linux-amd64/prometheus.yml /etc/prometheus/
```

## 4. Create a systemd Service

Create a systemd service file for Prometheus:

```bash
sudo tee /etc/systemd/system/prometheus.service > /dev/null <<'EOF'
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
    --config.file /etc/prometheus/prometheus.yml \
    --storage.tsdb.path /var/lib/prometheus/ \
    --web.console.templates=/etc/prometheus/consoles \
    --web.console.libraries=/etc/prometheus/console_libraries

[Install]
WantedBy=multi-user.target
EOF
```

## 5. Start Prometheus

Reload systemd and start the Prometheus service:

```bash
sudo systemctl daemon-reload
sudo systemctl start prometheus
sudo systemctl enable prometheus
```

Prometheus will now be running on port 9090.

```