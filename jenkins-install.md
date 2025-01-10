# Jenkins Installation Guide on Ubuntu 24.04

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Step 1: Update the System](#step-1-update-the-system)
3. [Step 2: Install Java](#step-2-install-java)
4. [Step 3: Add Jenkins GPG Key and Repository](#step-3-add-jenkins-gpg-key-and-repository)
5. [Step 4: Install Jenkins](#step-4-install-jenkins)
6. [Step 5: Install Apache and Configure Reverse Proxy](#step-5-install-apache-and-configure-reverse-proxy)
7. [Step 6: Finalize Jenkins Installation](#step-6-finalize-jenkins-installation)

---

## Prerequisites

- A server running Ubuntu 24.04 OS
- Root or non-root user with `sudo` privileges
- At least 2 GB of RAM (recommended)

---

## Step 1: Update the System

Update the system to the latest package versions:

```bash
sudo apt update -y && sudo apt upgrade -y
```

---

## Step 2: Install Java

Jenkins requires Java. Install OpenJDK 21:

```bash
sudo apt install openjdk-21-jdk -y
```

Verify the installation:

```bash
java -version
```

Expected output:

```plaintext
openjdk version "21.0.3" 2024-04-16
OpenJDK Runtime Environment (build 21.0.3+9-Ubuntu-1ubuntu1)
OpenJDK 64-Bit Server VM (build 21.0.3+9-Ubuntu-1ubuntu1, mixed mode, sharing)
```

---

## Step 3: Add Jenkins GPG Key and Repository

Add the Jenkins GPG key:

```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
```

Add the Jenkins repository:

```bash
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```

Update the package list:

```bash
sudo apt update -y
```

---

## Step 4: Install Jenkins

Install Jenkins:

```bash
sudo apt install jenkins -y
```

Start and enable the Jenkins service:

```bash
sudo systemctl start jenkins && sudo systemctl enable jenkins
```

Check the service status:

```bash
sudo systemctl status jenkins
```

Expected output:

```plaintext
● jenkins.service - Jenkins Continuous Integration Server
     Active: active (running)
```

---

## Step 5: Install Apache and Configure Reverse Proxy

Install Apache:

```bash
sudo apt install apache2 -y
```

Start and enable Apache:

```bash
sudo systemctl start apache2 && sudo systemctl enable apache2
```

Check the Apache status:

```bash
sudo systemctl status apache2
```

Create an Apache configuration file:

```bash
touch /etc/apache2/sites-available/jenkins.conf
```

Edit the file and add the following:

```apache
<VirtualHost *:80>
    ServerName yourdomain.com
    ProxyRequests Off
    ProxyPreserveHost On
    AllowEncodedSlashes NoDecode

    <Proxy http://localhost:8080/*>
      Order deny,allow
      Allow from all
    </Proxy>

    ProxyPass / http://localhost:8080/ nocanon
    ProxyPassReverse / http://localhost:8080/
    ProxyPassReverse / http://yourdomain.com/
</VirtualHost>
```

Enable the configuration and required modules:

```bash
sudo a2ensite jenkins
sudo a2enmod headers
sudo a2enmod rewrite
sudo a2enmod proxy
sudo a2enmod proxy_http
sudo systemctl restart apache2
```

---

## Step 6: Finalize Jenkins Installation

Retrieve the initial admin password:

```bash
cat /var/lib/jenkins/secrets/initialAdminPassword
```

Use the password to unlock Jenkins at `http://yourdomain.com` and complete the setup.

---

## Additional Resources

For further details, visit the [official documentation](https://www.jenkins.io/).
