# How to Install Maven on Debian/Ubuntu

## 1. Update Package Lists

First, update your package lists:

```bash
sudo apt update
```

## 2. Install Maven

Install Maven using the following command:

```bash
sudo apt install maven -y
```

## 3. Verify the Installation

You can verify that Maven has been installed correctly by checking its version:

```bash
mvn -version
```

## 4. Configure Environment Variables (Optional)

In some cases, you may need to set the `JAVA_HOME` environment variable. You can do this by adding the following line to your `/etc/environment` file:

```bash
JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"
```

Reload the file to apply the changes:

```bash
source /etc/environment
```
