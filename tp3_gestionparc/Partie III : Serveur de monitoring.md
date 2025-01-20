### 🌞 Dérouler le script autoconfig.sh développé à la partie I
```bash 
[rock-bji@monitoring netdata]$ sudo /home/rock-bji/autoconfig.sh monitoring.tp3.b1
17:02:21 [INFO] Le script d'autoconfiguration a démarré
17:02:21 [INFO] Le script a bien été lancé en root.
17:02:21 [INFO] Vérification de l'état de SELinux...
17:02:21 [INFO] Vérification de l'état du firewall
17:02:21 [INFO] Service de firewalling firewalld est activé.
17:02:21 [INFO] Vérification du port SSH
17:02:21 [INFO] Le service SSH ne tourne pas sur le port 22/TCP. Port actuel : 12473.
17:02:21 [INFO] La machine s'appelle déjà monitoring.tp3.b1.
17:02:21 [INFO] Vérification de l'utilisateur rock-bji...
17:02:21 [INFO] L'utilisateur rock-bji est déjà dans le groupe wheel.
17:02:21 [INFO] Le script d'autoconfiguration s'est correctement déroulé.
```
### 🌞 Installer Netdata
```bash
[rock-bji@monitoring netdata]$ systemctl status netdata
● netdata.service - Real time performance monitoring
     Loaded: loaded (/usr/lib/systemd/system/netdata.service; enabled; pres>
     Active: active (running) since Mon 2025-01-20 16:40:49 CET; 10min ago
    Process: 4551 ExecStartPre=/bin/mkdir -p /var/cache/netdata (code=exite>
    Process: 4553 ExecStartPre=/bin/chown -R netdata /var/cache/netdata (co>
    Process: 4554 ExecStartPre=/bin/mkdir -p /run/netdata (code=exited, sta>
    Process: 4555 ExecStartPre=/bin/chown -R netdata /run/netdata (code=exi>
   Main PID: 4556 (netdata)
      Tasks: 98 (limit: 10776)
     Memory: 147.1M
        CPU: 16.393s
     CGroup: /system.slice/netdata.service
             ├─4556 /usr/sbin/netdata -P /run/netdata/netdata.pid -D
             ├─4557 "spawn-plugins    " "  " "                        " "  "
             ├─4728 bash /usr/libexec/netdata/plugins.d/tc-qos-helper.sh 1
             ├─4748 /usr/libexec/netdata/plugins.d/apps.plugin 1
             ├─4750 /usr/libexec/netdata/plugins.d/debugfs.plugin 1
             ├─4751 /usr/libexec/netdata/plugins.d/ebpf.plugin 1
lines 1-18
```
### 🌞 Ajouter un check TCP
```bash
jobs:
  - name: jellyfin_tcp
    host: 10.3.1.11
    ports:
      - 8096
```
### 🌞 Ajout d'une alerte Discord
```bash
# Configuration des notifications Discord
DISCORD_WEBHOOK_URL="https://discord.com/api/webhooks/1330923941484560457/xYlTX7mEmMfdYydzaziqycQJZQ0-FgL7ZBA7Zvgp7RsT44ccYigLneAPiH_rXCrHNLD-"
SEND_DISCORD="YES"
DEFAULT_RECIPIENT_DISCORD="alarms"
```
