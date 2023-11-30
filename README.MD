# Installing Docker Engine on Ubuntu by Three distinct methods
Welcome to this comprehensive guide on installing Docker Engine on Ubuntu 22.04! In this demo, we'll explore three distinct methods to set up Docker on linux system: using Docker's apt repository, installing from packages, and employing the convenient script provided by Docker.

## Install using the apt repository
Set up Docker's apt repository:

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

```bash
# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

## To install the latest version, run:
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## Verify that the Docker Engine installation is successful by running the hello-world image.
```bash
sudo docker run hello-world
```

[Demo video](https://youtu.be/-pQJVu7LP-c)

## To install a specific version of Docker Engine, start by listing the available versions in the repository:

###  List the available versions:
```bash
apt-cache madison docker-ce | awk '{ print $3 }'
```

### Select the desired version and install:

```bash
VERSION_STRING=5:24.0.0-1~ubuntu.22.04~jammy
sudo apt-get install docker-ce=$VERSION_STRING docker-ce-cli=$VERSION_STRING containerd.io docker-buildx-plugin docker-compose-plugin
```

[Watch Demo](https://youtu.be/7XVfXTtJzkM)

## Installing Docker from packages:
### Removing the old installation
```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

Go to https://download.docker.com/linux/ubuntu/dists/

Select your Ubuntu version in the list.

Go to pool/stable/ and select the applicable architecture (amd64, armhf, arm64, or s390x).

Download the following deb files for the Docker Engine, CLI, containerd, and Docker Compose packages:

```bash
wget https://download.docker.com/linux/ubuntu/dists/jammy/pool/stable/amd64/docker-ce_23.0.0-1~ubuntu.22.04~jammy_amd64.deb
 wget https://download.docker.com/linux/ubuntu/dists/jammy/pool/stable/amd64/docker-ce-cli_23.0.0-1~ubuntu.22.04~jammy_amd64.deb
 wget https://download.docker.com/linux/ubuntu/dists/jammy/pool/stable/amd64/docker-buildx-plugin_0.10.2-1~ubuntu.22.04~jammy_amd64.deb
 wget https://download.docker.com/linux/ubuntu/dists/jammy/pool/stable/amd64/docker-compose-plugin_2.15.1-1~ubuntu.22.04~jammy_amd64.deb
wget https://download.docker.com/linux/ubuntu/dists/jammy/pool/stable/amd64/containerd.io_1.6.25-1_amd64.deb
```
```bash
sudo dpkg -i ./containerd.io_1.6.25-1_amd64.deb ./docker-buildx-plugin_0.10.2-1~ubuntu.22.04~jammy_amd64.deb ./docker-ce_23.0.0-1~ubuntu.22.04~jammy_amd64.deb ./docker-ce-cli_23.0.0-1~ubuntu.22.04~jammy_amd64.deb ./docker-compose-plugin_2.15.1-1~ubuntu.22.04~jammy_amd64.deb 
sudo service docker start
sudo usermod -aG docker $USER
```
```bash
docker run hello-world
```
[Watch Demo](https://youtu.be/AYTJzcmn3mI)

## Install using the convenience script

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh 
```

### Upgrade to the latest using apt
```bash
for package in docker-ce docker-ce-cli containerd.io docker-buildx-plugindocker-compose-plugin; do
	sudo apt upgrade $package
done
```
[Demo video](https://youtu.be/6BL536j9i68)


