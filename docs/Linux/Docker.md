---
tags: docker setup
---

# Docker
## Installation
Follow this [link](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-22-04) instructions to install docker on your machine
```bash
sudo apt update

# Next, install a few prerequisite packages which let `apt` use packages over HTTPS:
sudo apt install apt-transport-https ca-certificates curl software-properties-common

# Then add the GPG key for the official Docker repository to your system:
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Add the Docker repository to APT sources:
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Update your existing list of packages again for the addition to be recognized:
sudo apt update

# Make sure you are about to install from the Docker repo instead of the default Ubuntu repo:
apt-cache policy docker-ce

# Finally, install Docker:
sudo apt install docker-ce

# Docker should now be installed, the daemon started, and the process enabled to start on boot. Check that it’s running:
sudo systemctl status docker
```

Add docker to groups so we don't need sudo
```bash
sudo usermod -aG docker ${USER}
```

Install `docker-compose` for later use
```bash
sudo apt-get install docker-compose
```

Restart your computer to apply changes

## Commands
List containers
```bash
docker ps [OPTIONS]
	--all # Show all containers (default shows just running)
```
Create volume
```bash
docker volume create
```
Display information on one or more volumes
```bash
docker volume inspect
```
List volumes
```bash
docker volume ls
```
Remove all unused local volumes
```bash
docker volume prune
```
Remove one or more volumes
```bash
docker volume rm
```
Start existing containers for a service
```bash
docker compose start
```
Builds, (re)creates, starts and attaches to containers for a service
```bash
docker compose up
```
Same as up, but starts the containers in the background and leaves them running
```bash
docker compose up -d
```
Stop the containers, but won't remove them
```bash
docker compose stop
```
Stop the container by name
```bash
docker stop [CONTAINER_NAME]
```
Stop the containers, remove the stopped containers as well as any networks that were created
```bash
docker compose down
```
Same as down, plus remove all volumes. This is great for a full blown reset of the environment
```bash
docker compose down -v
```
Restart container with name \[NAME]
```bash
docker restart [NAME]
```
Build docker image with an image name and tag
```bash
docker build -t networkcloudmanager/[IMAGE-NAME]:[TAG] .
```
Docker logs TODO
```bash
docker logs []
```
See stats about the docker containers with CPU usage, memory, etc
```bash
docker stats
```
Delete all docker images
```bash
docker image prune -a
```
TODO
```bash
docker rmi []
```

## Docker Hub
Push image to Docker Hub
```bash
# Build docker image with desired tag
docker build -t networkcloudmanager/[IMAGE-NAME]:[TAG] .

# Log in to Docker Hub
docker login

# Check if there are more than one images with the same tag with
docker images

# If not, go ahead and push it
docker push networkcloudmanager/[IMAGE-NAME]:[TAG]
```