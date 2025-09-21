# Docker Installation and Setup Guide

## Installing and Setting Up Docker

Before installing Docker, make sure there isn’t a previous version installed:

```bash
sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

Also, remove related files:

```bash
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```

There are different ways to install Docker, but one common method is using a script:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
```

The above command downloads the required script. You can run it in one of two ways. Using `DRY_RUN=1` lets you display the various steps the script will perform:

```bash
DRY_RUN=1 sh ./get-docker.sh
```

or

```bash
sudo sh get-docker.sh
```

To grant user-level permissions for Docker, run the following commands to create a group and add the current user to it:

```bash
sudo groupadd docker
sudo usermod -aG docker $USER
```

Finally, reload settings and start the Docker service:

```bash
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
```

### Related Links

* [Install Docker Engine on Ubuntu | Docker Documentation](https://docs.docker.com/engine/install/ubuntu/)
* [Post-installation steps for Linux | Docker Documentation](https://docs.docker.com/engine/install/linux-postinstall/)

---

## Installing and Setting Up Docker-Compose

**Note 1:** In the new Docker version, there is a module called **docker compose plugin**, which is installed alongside Docker. It allows you to use the new version of Docker Compose with the command:

```bash
docker compose
```

**Note 2:** Changes in command behavior are inevitable and may change again in the future, so always refer to the official documentation as the primary source.

You can install previous versions using the following method:

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compo
```
