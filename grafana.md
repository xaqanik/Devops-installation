# How to Install Grafana on Debian/Ubuntu

## 1. Add the Grafana Repository

Install the required packages:

```bash
sudo apt-get install -y apt-transport-https
sudo apt-get install -y software-properties-common wget
```

Add the Grafana GPG key:

```bash
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
```

Add the Grafana repository:

```bash
echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

## 2. Install Grafana

Update your package lists and install Grafana:

```bash
sudo apt-get update
sudo apt-get install grafana -y
```

## 3. Start the Grafana Server

Start and enable the Grafana service:

```bash
sudo systemctl start grafana-server
sudo systemctl enable grafana-server
```

## 4. Access Grafana

Open your browser and navigate to `http://<your_server_ip>:3000`. The default username and password are `admin` and `admin`. You will be prompted to change the password on your first login.
