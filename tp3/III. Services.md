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
bj-is@tpos:~$ echo $((RANDOM % 65535 + 1))
16038

bj-is@tpos:~$ cat /etc/ssh/sshd_config | grep "Port"
Port 16038
#GatewayPorts no
```
### 🌞 Redémarrer le service
```bash
bj-is@tpos:~$ sudo systemctl restart ssh
```
### 🌞 Effectuer une connexion SSH sur le nouveau port
```bash
bj-is@tpos:~$ exit
logout
Connection to 192.168.20.3 closed.
PS C:\Users\jerem> ssh -p 16038 bj-is@192.168.20.3
bj-is@192.168.20.3's password:
Linux tpos 6.1.0-27-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.1.115-1 (2024-11-01) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Thu Nov 28 09:00:08 2024 from 192.168.20.1

```
## B. Le service en lui-même
### 🌞 Trouver le fichier ssh.service
```bash
bj-is@tpos:~$ sudo find / -iname ssh.service
[sudo] password for bj-is:
/sys/fs/cgroup/system.slice/ssh.service
/var/lib/systemd/deb-systemd-helper-enabled/multi-user.target.wants/ssh.service
/etc/systemd/system/multi-user.target.wants/ssh.service
/usr/lib/systemd/system/ssh.service
/usr/share/doc/avahi-daemon/examples/ssh.service
```
### 🌞 Déterminer quel est le programme lancé
```bash
bj-is@tpos:~$ sudo cat /usr/lib/systemd/system/ssh.service | grep ExecStart=
ExecStart=/usr/sbin/sshd -D $SSHD_OPTS
```
## 4. Créez votre propre service
### 🌞 Déterminer le dossier qui contient la commande python3
```bash
bj-is@tpos:~$ which python3
/usr/bin/python3
```
### 🌞 Créez un fichier /etc/systemd/system/meow_web.service
### 🌞 Indiquez à l'OS que vous avez modifié les services
```bash
bj-is@tpos:~$ systemctl daemon-reload
==== AUTHENTICATING FOR org.freedesktop.systemd1.reload-daemon ====
Authentication is required to reload the systemd state.
Authenticating as: BJ-Is,,, (bj-is)
Password:
==== AUTHENTICATION COMPLETE ====
```
### 🌞 Démarrez votre service
```bash
bj-is@tpos:~$ systemctl status meow_web.service
● meow_web.service - Super serveur web MEOW
     Loaded: loaded (/etc/systemd/system/meow_web.service; enabled; preset:>
     Active: active (running) since Thu 2024-11-28 08:58:06 EST; 41min ago
 Invocation: 9b5c7dec21c1496e8ddf6587a04c20e3
   Main PID: 742 (python3)
      Tasks: 1 (limit: 4619)
     Memory: 17.4M (peak: 19.4M)
        CPU: 511ms
     CGroup: /system.slice/meow_web.service
             └─742 /usr/bin/python3 -m http.server 8888

Nov 28 08:58:06 tpos python3[742]: Serving HTTP on 0.0.0.0 port 8888 (http:>
Warning: journal has been rotated since unit was started and some journal f>
lines 1-13/13 (END)
```
### 🌞 Déterminer le PID du processus Python en cours d'exécution
```bash
bj-is@tpos:~$ ps -ef | grep python3
bj-is        742       1  0 08:58 ?        00:00:00 /usr/bin/python3 -m http.server 8888
bj-is       1050     897  0 08:58 ?        00:00:00 /usr/bin/python3 /usr/share/system-config-printer/applet.py
bj-is       2300    2129  0 09:40 pts/1    00:00:00 grep python3
```
### 🌞 Prouvez que le programme écoute derrière le port 8888
```bash
bj-is@tpos:~$ sudo ss -tuln | grep 8888
[sudo] password for bj-is:
tcp   LISTEN 0      5            0.0.0.0:8888       0.0.0.0:*
```
### 🌞 Faire en sote que le service se lance automatiquement au démarrage de la machine
```bash
bj-is@tpos:~$ sudo systemctl enable meow_web.service
```
