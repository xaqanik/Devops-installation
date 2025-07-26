# How to Install Nexus on Debian/Ubuntu

## 1. Install Java

Nexus requires Java to run. Install the OpenJDK package:

```bash
sudo apt update
sudo apt install openjdk-8-jdk -y
```

## 2. Download and Install Nexus

Download the latest version of Nexus from the official website. You can check the latest version here: https://www.sonatype.com/nexus/repository-oss/download

```bash
wget https://download.sonatype.com/nexus/3/latest-unix.tar.gz
```

Extract the downloaded archive:

```bash
tar -xvf latest-unix.tar.gz
```

Move the extracted files to a suitable location, for example, `/opt`:

```bash
sudo mv nexus-3* /opt/nexus
```

## 3. Create a Nexus User

For security purposes, we'll create a dedicated user to run Nexus:

```bash
sudo adduser nexus
```

## 4. Configure Nexus

Change the ownership of the Nexus files to the `nexus` user:

```bash
sudo chown -R nexus:nexus /opt/nexus
```

Open the `nexus.rc` file and uncomment the `run_as_user` option:

```bash
sudo nano /opt/nexus/bin/nexus.rc
```

And set it to:

```
run_as_user="nexus"
```

## 5. Create a systemd Service

Create a systemd service file for Nexus:

```bash
sudo tee /etc/systemd/system/nexus.service > /dev/null <<'EOF'
[Unit]
Description=nexus service
After=network.target

[Service]
Type=forking
LimitNOFILE=65536
ExecStart=/opt/nexus/bin/nexus start
ExecStop=/opt/nexus/bin/nexus stop
User=nexus
Restart=on-abort

[Install]
WantedBy=multi-user.target
EOF
```

## 6. Start Nexus

Reload systemd and start the Nexus service:

```bash
sudo systemctl daemon-reload
sudo systemctl start nexus
sudo systemctl enable nexus
```

Nexus will now be running on port 8081.
