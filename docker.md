# How to Install Docker on Debian/Ubuntu

## 1. Set Up the Repository

First, update your package lists and install the necessary packages to allow `apt` to use a repository over HTTPS:

```bash
sudo apt-get update
sudo apt-get install -y ca-certificates curl
```

Next, add Docker's official GPG key:

```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

Finally, set up the stable repository:

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## 2. Install Docker Engine

Update your package lists again and install Docker Engine, along with the latest plugins:

```bash
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## 3. Verify the Installation

Verify that Docker Engine is installed correctly by running the `hello-world` image:

```bash
sudo docker run hello-world
```

## 4. Manage Docker as a Non-Root User (Optional)

To run Docker commands without `sudo`, add your user to the `docker` group:

```bash
sudo usermod -aG docker $USER
```

You will need to log out and log back in for this to take effect.

```