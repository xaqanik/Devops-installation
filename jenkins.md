# How to Install Jenkins on Debian/Ubuntu

## 1. Install Java

Jenkins requires Java to run. We will install OpenJDK 17, the latest LTS version:

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
```
Verify the installation:
```bash
java -version
```

## 2. Add the Jenkins Repository

Add the Jenkins GPG key and repository to your system:

```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
```

```bash
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
```

## 3. Install Jenkins

Update your package lists again and install Jenkins:

```bash
sudo apt update
sudo apt install jenkins -y
```

## 4. Start Jenkins

Start and enable the Jenkins service:

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

## 5. Unlock Jenkins

To get the initial administrator password, run:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Open your browser and navigate to `http://<your_server_ip>:8080`. Use the password to unlock Jenkins and complete the setup.

```