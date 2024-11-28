## 2. Analyser un service existant
### 🌞 S'assurer que le service ssh est démarré
```bash
bj-is@tpos:~$ systemctl status ssh
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; enabled; preset: >
     Active: active (running) since Wed 2024-11-27 20:19:35 EST; 1h 30min a>
 Invocation: 52314a12534c4b479622d62b6fd69069
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 742 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCC>
   Main PID: 746 (sshd)
      Tasks: 1 (limit: 4619)
     Memory: 7.4M (peak: 24.4M)
        CPU: 291ms
     CGroup: /system.slice/ssh.service
             └─746 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"

Warning: some journal files were not opened due to insufficient permissions.
lines 1-15/15 (END)
```
### 🌞 Isolez la ligne qui indique le nom du programme lancé
```bash
bj-is@tpos:~$ systemctl status ssh | grep "Main PID"
   Main PID: 746 (sshd)
```
### 🌞 Déterminer le port sur lequel écoute le service SSH
```bash
bj-is@tpos:~$ sudo ss -lnpt | grep sshd
[sudo] password for bj-is:
LISTEN 0      128          0.0.0.0:22        0.0.0.0:*    users:(("sshd",pid=746,fd=7))
LISTEN 0      128             [::]:22           [::]:*    users:(("sshd",pid=746,fd=8))
```
### 🌞 Consulter les logs du service SSH
```bash
bj-is@tpos:~$ sudo journalctl -u ssh
Nov 06 05:49:34 tpos systemd[1]: Starting ssh.service - OpenBSD Secure Shel>
Nov 06 05:49:34 tpos sshd[548]: Server listening on 0.0.0.0 port 22.
Nov 06 05:49:34 tpos sshd[548]: Server listening on :: port 22.
Nov 06 05:49:34 tpos systemd[1]: Started ssh.service - OpenBSD Secure Shell>
-- Boot 181bcbb39ee8466dba86a1d6704706b4 --
Nov 06 06:14:14 tpos systemd[1]: Starting ssh.service - OpenBSD Secure Shel>
Nov 06 06:14:14 tpos sshd[543]: Server listening on 0.0.0.0 port 22.
Nov 06 06:14:14 tpos sshd[543]: Server listening on :: port 22.
Nov 06 06:14:14 tpos systemd[1]: Started ssh.service - OpenBSD Secure Shell>
-- Boot 649dac07ca25408089737db360c9704d --
Nov 06 10:58:26 tpos systemd[1]: Starting ssh.service - OpenBSD Secure Shel>
Nov 06 10:58:26 tpos sshd[632]: Server listening on 0.0.0.0 port 22.
Nov 06 10:58:26 tpos sshd[632]: Server listening on :: port 22.
Nov 06 10:58:26 tpos systemd[1]: Started ssh.service - OpenBSD Secure Shell>
Nov 07 03:17:14 tpos sshd[8339]: Accepted password for bj-is from 192.168.2>
Nov 07 03:17:14 tpos sshd[8339]: pam_unix(sshd:session): session opened for>
Nov 07 03:17:14 tpos sshd[8339]: pam_env(sshd:session): deprecated reading >
Nov 09 07:30:34 tpos sshd[10115]: Invalid user bji-is from 192.168.20.1 por>
lines 1-18
```
## 3. Modification du service
## A. Configuration du service SSH
### 🌞 Identifier le fichier de configuration du serveur SSH
```bash
bj-is@tpos:~$ ls -l /etc/ssh/sshd_config
-rw-r--r-- 1 exroot root 3222 Nov 23 07:29 /etc/ssh/sshd_config
```
### 🌞 Modifier le fichier de conf
```bash
bj-is@tpos:~$ echo $RANDOM
21898

bj-is@tpos:~$ cat /etc/ssh/sshd_config | grep "Port"
Port 21898
#GatewayPorts no
```
### 🌞 Redémarrer le service
```bash
bj-is@tpos:~$ sudo systemctl restart ssh
```
### 🌞 Effectuer une connexion SSH sur le nouveau port
```bash
PS C:\Users\jerem> ssh bj-is@192.168.20.3
ssh: connect to host 192.168.20.3 port 22: Connection refused
```
