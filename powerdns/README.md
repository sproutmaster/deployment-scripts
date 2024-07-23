# POWERDNS with PowerDNS Admin & TLS

## Install Docker

```bash
curl -sSL https://get.docker.com/ | sudo sh
sudo usermod -aG docker $(whoami) # allows docker to run privileged
newgrp docker
sudo systemctl enable docker && sudo systemctl start docker
```

## Disable systemd-resolved

We need to disable systemd-resolved listener to free up port 53

```bash
sudo nano /etc/systemd/resolved.conf 
```

Change the following

```diff
- #DNS=
+ DNS=1.1.1.1

- #DNSStubListener=yes
+ DNSStubListener=no
```
Restart the service

```bash
sudo systemctl restart systemd-resolved.service
sudo ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf
```

## Change Docker DNS

Docker by default queries localhost:53 for dns but we just tured that off. So we have to set a replacement

```bash
sudo nano /etc/default/docker
```

Change the following

```diff
- #DOCKER_OPTS="--dns 8.8.8.8 --dns 8.8.4.4"
+ DOCKER_OPTS="--dns 8.8.8.8 --dns 8.8.4.4"
```

Restart Docker
```bash
sudo systemctl restart docker
```

## Spin up Containers

Make a directory for powerdns and change into it

```
mkdir powerdns
cd !!*
```

Copy master or slave compose file depending on what you need

After that, just run 

```bash
docker compose up -d -f <file.yaml>
```

For troubleshooting, see the logs

```bash
docker logs <container id>
```
