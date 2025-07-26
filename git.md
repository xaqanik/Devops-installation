# How to Install Git on Debian/Ubuntu

## 1. Update Package Lists

First, update your package lists to ensure you get the latest version available from the repositories:

```bash
sudo apt update
```

## 2. Install Git

Install Git using the following command:

```bash
sudo apt install git -y
```

## 3. Verify the Installation

You can verify that Git has been installed correctly by checking its version:

```bash
git --version
```

## 4. Configure Git

After installing Git, you should configure it with your name and email address. This is important because every Git commit uses this information:

```bash
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
```
