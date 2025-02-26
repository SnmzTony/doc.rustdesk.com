---
title: Docker
weight: 6
---

### Docker

Install Docker with [this](https://docs.docker.com/engine/install) guide to ensure its the most up to date!

Run the following commands:
```bash
sudo docker image pull rustdesk/rustdesk-server-pro
sudo docker run --name hbbs -v `pwd`:/root -td --net=host --restart unless-stopped rustdesk/rustdesk-server-pro hbbs
sudo docker run --name hbbr -v `pwd`:/root -td --net=host --restart unless-stopped rustdesk/rustdesk-server-pro hbbr
```
{{% notice note %}}
The above example uses `sudo` and `--net=host`, this will not work on windows please remove these commands, if you remove `--net=host` please check below.
{{% /notice %}}

```bash
macaddrhbbs=$(echo -n A0-62-2F; dd bs=1 count=3 if=/dev/random 2>/dev/null |hexdump -v -e '/1 "-%02X"')
sudo docker image pull rustdesk/rustdesk-server-pro
sudo docker run --name hbbs -p 21114:21114 -p 21115:21115 -p 21116:21116 -p 21116:21116/udp -p 21118:21118 -v `pwd`:/root -td --mac-address="$macaddrhbbs" --restart unless-stopped rustdesk/rustdesk-server-pro hbbs
sudo docker run --name hbbr -p 21117:21117 -p 21119:21119 -v `pwd`:/root -td --restart unless-stopped rustdesk/rustdesk-server-pro hbbr
```

### Docker Compose

With Docker Compose you HAVE to use `network_mode: "host"`. Install Docker using [this](https://docs.docker.com/engine/install) guide to ensure its the most up to date!

Copy the below into docker-compose.yml

```yaml
version: '3'

services:
  hbbs:
    container_name: hbbs
    image: rustdesk/rustdesk-server-pro:latest
    command: hbbs
    volumes:
      - ./data:/root
    network_mode: "host"

    depends_on:
      - hbbr
    restart: unless-stopped


  hbbr:
    container_name: hbbr
    image: rustdesk/rustdesk-server-pro:latest
    command: hbbr
    volumes:
      - ./data:/root
    network_mode: "host"
    restart: unless-stopped
```

The run `docker compose up -d`