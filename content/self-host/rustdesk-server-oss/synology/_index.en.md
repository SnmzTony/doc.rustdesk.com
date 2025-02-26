---
title: Synology
weight: 22
---

> An alterative up-to-date tutorial from third-party is [here](https://mariushosting.com/how-to-install-rustdesk-on-your-synology-nas/)

This tutorial is based on latest DSM v6 and v7.

### Install Docker

Open package manager and install docker

|    |    |
| -- | -- |
| ![](images/package-manager.png) | ![](images/docker.png) |


### Install RustDesk Server

| Search rustdesk-server in Docker's registry and install by double click | Installed rustdesk-server image, double click to create rustdesk-server container |
| -- | -- |
| ![](images/pull-rustdesk-server.png) | ![](images/rustdesk-server-installed.png) |


### Create hbbs container

As mentioned above, double click on rustdesk-server image to create new container, set it name to `hbbs`.
![](images/hbbs.png)

Click on above "Advanced Settings".

- Enable auto-restart
![](images/auto-restart.png)

- Enable "Use the same network as Docker host", for more about host net, please [check](install/#net-host)
![](images/host-net.png)

- Mount a host directory (e.g. `/home/rustdesk/`) to `/root`, hbbs will generate some files (database and `key` files) in this directory which need to be persistent over reboots.
| Mount | Files generated in the host directory |
| -- | -- |
| ![](images/mount.png?width=500px) | ![](images/mounted-dir.png?width=300px) |

- Set command
{{% notice note %}}
Synology's OS is Debian based, so host net (--net=host) works fine, we do not need to map ports with `-p` option.

`192.168.16.98` is an internal IP used here for demonstration only, please set it to a public IP when you deploy (or you can use your DDNS address if you have configured one in Control Panel - Connectivity - DDNS) and don't forget to open ports on your router and your synology firewall if this is enabled (Control Panel - Connectivity - Firewall)!

{{% /notice %}}

![](images/hbbs-cmd.png?v2)

- Done

![](images/hbbs-config.png)

### Create hbbr container

Please repeat above `hbbs` steps, but name the container `hbbr` and command (for Set Command Step) should be `hbbr -k _`.

![](images/hbbr-config.png)

### hbbr/hbbs containers

![](images/containers.png?width=500px)


| Double click on container and check log | Double confirm hbbs/hbbr using host network |
| -- | -- |
| ![](images/log.png?width=500px) | ![](images/network-types.png?width=500px) |

### Retrieve your Key

Browse to the folder setup before using File Station, download id_ed25519.pub and open with a text editor to via your key.
