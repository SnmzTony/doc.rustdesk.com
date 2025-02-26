---
title: RustDesk Server Pro
weight: 200
pre: "<b>2.2. </b>"
---

RustDesk Server Pro has more features compared to the open source version.

- OIDC, LDAP, 2FA (email verification)
- Address book
- Rename
- Log management
- Device management
- Settings sync
- Permission control
- Multiple relay servers (automatically selects your closest relay)

{{% notice note %}}
RustDesk client >= 1.2.0 required
{{% /notice %}}

## Download

[https://github.com/rustdesk/rustdesk-server-pro/releases/latest](https://github.com/rustdesk/rustdesk-server-pro/releases/latest)

## Installation

### Simple Install

To make life easy, we have developed scripts which take care of everything (install/upgrade/convert from open source) [Simple Install Script](https://rustdesk.com/docs/en/self-host/rustdesk-server-pro/installscript/).

{{% notice note %}}
Don't forget to get your license from [https://rustdesk.com/pricing.html](https://rustdesk.com/pricing.html), check [license](/docs/en/self-host/rustdesk-server-pro/license) page for more details.
{{% /notice %}}

### Manual Installation

Almost the same as [the open source version](/docs/en/self-host/install/), but you do not need to run hbbs/hbbr with any arguments, these can be set later in web console.

- `-k _` is set by default
- `-r <server:host>` is not needed any more if the relay server runs on the same machine with hbbs, and you can set multiple relay servers in the web console

### Ports Required

You need port 21114-21119 TCP and 21116 UDP open, please ensure these ports are setup when you set firewall rules and docker port mapping. 

{{% notice note %}}
You should use a proxy like nginx to deliver this over HTTPS requiring port 443 to be opened.
{{% /notice %}}
