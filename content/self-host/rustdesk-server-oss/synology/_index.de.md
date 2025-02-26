---
title: Synology
weight: 22
---

Diese Anleitung basiert auf dem aktuellen DSM v6.

### Docker installieren

Paketmanager öffnen und Docker installieren

|    |    |
| -- | -- |
| ![](/docs/en/self-host/rustdesk-server-oss/synology/images/package-manager.png) | ![](/docs/en/self-host/rustdesk-server-oss/synology/images/docker.png) |


### RustDesk-Server installieren

| RustDesk-Server im Docker-Register suchen und per Doppelklick installieren | RustDesk-Server-Image ist installiert, Doppelklick zum Erstellen des RustDesk-Server-Containers |
| -- | -- |
| ![](/docs/en/self-host/rustdesk-server-oss/synology/images/pull-rustdesk-server.png) | ![](/docs/en/self-host/rustdesk-server-oss/synology/images/rustdesk-server-installed.png) |


### hbbs-Container erstellen

Wie oben erwähnt, doppelklicken Sie auf das RustDesk-Server-Image, um einen neuen Container zu erstellen, und geben Sie ihm den Namen `hbbs`.
![](/docs/en/self-host/rustdesk-server-oss/synology/images/hbbs.png)

Klicken Sie auf "Erweiterte Einstellungen".

- Automatischen Neustart aktivieren
![](/docs/en/self-host/rustdesk-server-oss/synology/images/auto-restart.png)

- Aktivieren Sie "Use the same network as Docker host". Mehr Infos über das Hostnetz siehe [hier](/docs/de/self-host/install/#net-host)
![](/docs/en/self-host/rustdesk-server-oss/synology/images/host-net.png)

- Binden Sie ein Host-Verzeichnis (z. B. `Shared/test/`) als `/root` ein, hbbs wird einige Dateien (einschließlich der `key`-Datei) in diesem Verzeichnis erzeugen
| Einbinden | Im Host-Verzeichnis erzeugte Dateien |
| -- | -- |
| ![](/docs/en/self-host/rustdesk-server-oss/synology/images/mount.png?width=500px) | ![](/docs/en/self-host/rustdesk-server-oss/synology/images/mounted-dir.png?width=300px) |

- Befehl einstellen
{{% notice note %}}
Das Betriebssystem von Synology basiert auf Debian, daher funktioniert das Hostnetz (--net=host) einwandfrei, wir müssen keine Ports mit der Option `-p` zuordnen.

`192.168.16.98` ist eine Intranet-IP, die hier nur zu Demonstrationszwecken verwendet wird. Bitte setzen Sie sie bei der Bereitstellung auf eine öffentliche IP.

{{% /notice %}}

![](/docs/en/self-host/rustdesk-server-oss/synology/images/hbbs-cmd.png?v2)

- Fertig

![](/docs/en/self-host/rustdesk-server-oss/synology/images/hbbs-config.png)

### hbbr-Container erstellen

Bitte wiederholen Sie die obigen Schritte für `hbbs`, ändern aber den Containernamen in `hbbr` und den Befehl in `hbbr`.

![](/docs/en/self-host/rustdesk-server-oss/synology/images/hbbr-config.png)

### hbbr/hbbs-Container

![](/docs/en/self-host/rustdesk-server-oss/synology/images/containers.png?width=500px)


| Doppelklicken Sie auf den Container und prüfen Sie das Protokoll | Bestätigen Sie hbbs/hbbr über das Host-Netzwerk doppelt |
| -- | -- |
| ![](/docs/en/self-host/rustdesk-server-oss/synology/images/log.png?width=500px) | ![](/docs/en/self-host/rustdesk-server-oss/synology/images/network-types.png?width=500px) |
