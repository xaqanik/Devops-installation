# How to Install Docker on Debian/Ubuntu

## 1. Set Up the Repository

First, update your package lists and install the necessary packages to allow `apt` to use a repository over HTTPS:

```bash
sudo apt update
sudo apt install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release -y
```

Next, add Docker's official GPG key:

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Finally, set up the stable repository:

```bash
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## 2. Install Docker Engine

Update your package lists again and install Docker Engine:

```bash
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io -y
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