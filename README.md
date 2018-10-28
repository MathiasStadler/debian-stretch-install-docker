# debian-stretch-install-docker

## install docker-ce on stretch copy and paste method

```bash
INSTALL_DOCKER_CE="install-docker-cd.sh"
cat <<EOF >"$INSTALL_DOCKER_CE"
#!/bin/bash
set -e
sudo apt-get -y remove docker docker-engine docker.io
sudo apt-get -y update
sudo apt-get install -y apt-transport-https ca-certificates wget software-properties-common
wget https://download.docker.com/linux/debian/gpg
sudo apt-key add gpg
echo "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee -a /etc/apt/sources.list.d/docker.list
sudo apt-get update
sudo apt-cache policy docker-ce
sudo apt-get -y install docker-ce
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker vagrant
echo "please reboot this instance"
echo "run than for simple test: docker run hello-world"
echo "thx!!!"
EOF
chmod +x $INSTALL_DOCKER_CE
```

## execute script

```bash
./$INSTALL_DOCKER_CE
```