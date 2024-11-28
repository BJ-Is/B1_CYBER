## 1. Liste des users
### 🌞 Afficher la ligne du fichier qui concerne votre utilisateur
```bash
bj-is@tpos:~$ cat /etc/passwd | grep bj-is
bj-is:x:1000:1000:BJ-Is,,,:/home/bj-is:/bin/bash
```
### 🌞 Afficher la ligne du fichier qui concerne votre utilisateur ET celle de root en même temps
```bash
bj-is@tpos:~$ cat /etc/passwd | grep -E -i '(bj-is|root)'
root:x:0:0:root:/root:/bin/bash
bj-is:x:1000:1000:BJ-Is,,,:/home/bj-is:/bin/bash
```
### 🌞 Afficher la liste des groupes d'utilisateurs de la machine
```bash
bj-is@tpos:~$ id -nG
bj-is cdrom floppy sudo audio dip video plugdev users netdev bluetooth lpadmin scanner
```
### 🌞 Afficher la ligne du fichier qui concerne votre utilisateur ET celle de root en même temps
```bash
bj-is@tpos:~$  cat /etc/passwd | grep -E '^(bj-is|root):'
root:x:0:0:root:/root:/bin/bash
bj-is:x:1000:1000:BJ-Is,,,:/home/bj-is:/bin/bash
```
## 2. Hash des passwords
### 🌞 Afficher la ligne qui contient le hash du mot de passe de votre utilisateur
```bash
bj-is@tpos:~$ sudo cat /etc/shadow | grep bj-is
bj-is:$y$j9T$Hj70UL20btwcNQO6sYD8P/$HGVpX8XHaJjpm6BiFVRHMQCkfl4nA8UBdyLWM9fnFIA:20033:0:99999:7:::
```
## 3. Sudo
### 🌞 Faites en sorte que votre utilisateur puisse taper n'importe quelle commande sudo
```bash
bj-is@tpos:~$ getent group group sudo
sudo:x:27:bj-is
bj-is@tpos:~$ sudo -l
[sudo] password for bj-is:
Matching Defaults entries for bj-is on tpos:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin,
    use_pty

User bj-is may run the following commands on tpos:
    (ALL : ALL) ALL
```
## B. Practice
### 🌞 Créer un groupe d'utilisateurs
```bash
bj-is@tpos:~$ sudo groupadd stronk_admins
```
### 🌞 Créer un utilisateur
```bash
bj-is@tpos:~$ sudo useradd imbob
bj-is@tpos:~$ sudo usermod -aG imbob,stronk_admins imbob
[sudo] password for bj-is:

bj-is@tpos:~$ sudo passwd imbob
New password:
Retype new password:
passwd: password updated successfully
```
### 🌞 Prouver que l'utilisateur imbob a un password défini
```bash
bj-is@tpos:~$ cat /etc/passwd | grep imbo
imbob:x:1002:1003::/home/imbob:/bin/sh
```
### 🌞 Prouver que l'utilisateur imbob a un password défini
```bash
bj-is@tpos:~$ sudo cat /etc/shadow | grep imbob
[sudo] password for bj-is:
imbob:$y$j9T$a7LatBSeId/6x1nwJPPBH.$kcnC670kRoPSWsXJcol8VDz.cLQV5uwDYXgQffnCXU3:20047:0:99999:7:::
```
### 🌞 Prouver que l'utilisateur imbob appartient au groupe stronk_admins
```bash
bj-is@tpos:~$ groups imbob
imbob : imbob stronk_admins
```
### 🌞 Créer un deuxième utilisateur
```bash
bj-is@tpos:~$ sudo useradd imnotbobsorry
bj-is@tpos:~$ sudo passwd imnotbobsorry
New password:
Retype new password:
passwd: password updated successfully
```
### 🌞 Modifier la configuration de sudo pour que 
```bash
bj-is@tpos:~$ sudo usermod -aG imnotbobsorry,stronk_admins imnotbobsorry
```
### 🌞 Modifier la configuration de sudo pour que
```bash
bj-is@tpos:~$ su imnotbobsorry
Password:
$ sudo -l
[sudo] password for imnotbobsorry:
Matching Defaults entries for imnotbobsorry on tpos:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin,
    use_pty

bj-is@tpos:~$ su imbob
Password:
$ sudo -l
[sudo] password for imbob:
Matching Defaults entries for imbob on tpos:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin,
    use_pty

User imbob may run the following commands on tpos:
    (root) /usr/bin/apt-get update
    (ALL : ALL) ALL
$

User imnotbobsorry may run the following commands on tpos:
    (root) /usr/bin/apt-get update
```
### 🌞 Créer le dossier /home/goodguy (avec une commande)
```bash
bj-is@tpos:~$ mkdir goodguy
```
### 🌞 Changer le répertoire personnel de imbob
```bash
bj-is@tpos:~$ sudo usermod -d /home/goodguy imbob

bj-is@tpos:~$ sudo cat /etc/passwd
exroot:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/run/ircd:/usr/sbin/nologin
_apt:x:42:65534::/nonexistent:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:998:998:systemd Network Management:/:/usr/sbin/nologin
systemd-timesync:x:997:997:systemd Time Synchronization:/:/usr/sbin/nologin
messagebus:x:100:107::/nonexistent:/usr/sbin/nologin
avahi-autoipd:x:101:110:Avahi autoip daemon,,,:/var/lib/avahi-autoipd:/usr/sbin/nologin
sshd:x:102:65534::/run/sshd:/usr/sbin/nologin
dnsmasq:x:103:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
avahi:x:104:112:Avahi mDNS daemon,,,:/run/avahi-daemon:/usr/sbin/nologin
speech-dispatcher:x:105:29:Speech Dispatcher,,,:/run/speech-dispatcher:/bin/false
pulse:x:106:114:PulseAudio daemon,,,:/run/pulse:/usr/sbin/nologin
saned:x:107:117::/var/lib/saned:/usr/sbin/nologin
lightdm:x:108:118:Light Display Manager:/var/lib/lightdm:/bin/false
polkitd:x:996:996:polkit:/nonexistent:/usr/sbin/nologin
rtkit:x:109:119:RealtimeKit,,,:/proc:/usr/sbin/nologin
colord:x:110:120:colord colour management daemon,,,:/var/lib/colord:/usr/sbin/nologin
bj-is:x:1000:1000:BJ-Is,,,:/home/bj-is:/bin/bash
marmotte:x:1001:1001::/home/papier_alu/:/bin/sh
imbob:x:1002:1003::/home/goodguy:/bin/sh
imnotbobsorry:x:1003:1004::/home/imnotbobsorry:/bin/sh
```
### 🌞 Créer le dossier /home/badguy
```bash
bj-is@tpos:~$ mkdir badguy
```
### 🌞 Changer le répertoire personnel de imnotbobsorry
```bash
bj-is@tpos:~$ sudo usermod -d /home/badguy imnotbobsorry
bj-is@tpos:~$ sudo cat /etc/passwd
exroot:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/run/ircd:/usr/sbin/nologin
_apt:x:42:65534::/nonexistent:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:998:998:systemd Network Management:/:/usr/sbin/nologin
systemd-timesync:x:997:997:systemd Time Synchronization:/:/usr/sbin/nologin
messagebus:x:100:107::/nonexistent:/usr/sbin/nologin
avahi-autoipd:x:101:110:Avahi autoip daemon,,,:/var/lib/avahi-autoipd:/usr/sbin/nologin
sshd:x:102:65534::/run/sshd:/usr/sbin/nologin
dnsmasq:x:103:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
avahi:x:104:112:Avahi mDNS daemon,,,:/run/avahi-daemon:/usr/sbin/nologin
speech-dispatcher:x:105:29:Speech Dispatcher,,,:/run/speech-dispatcher:/bin/false
pulse:x:106:114:PulseAudio daemon,,,:/run/pulse:/usr/sbin/nologin
saned:x:107:117::/var/lib/saned:/usr/sbin/nologin
lightdm:x:108:118:Light Display Manager:/var/lib/lightdm:/bin/false
polkitd:x:996:996:polkit:/nonexistent:/usr/sbin/nologin
rtkit:x:109:119:RealtimeKit,,,:/proc:/usr/sbin/nologin
colord:x:110:120:colord colour management daemon,,,:/var/lib/colord:/usr/sbin/nologin
bj-is:x:1000:1000:BJ-Is,,,:/home/bj-is:/bin/bash
marmotte:x:1001:1001::/home/papier_alu/:/bin/sh
imbob:x:1002:1003::/home/goodguy:/bin/sh
imnotbobsorry:x:1003:1004::/home/badguy:/bin/sh
```
### 🌞 Prouver que les permissions du dossier /home/gooduy sont incohérentes
```bash
bj-is@tpos:~$ su - imbob
Password:
su: warning: cannot change directory to /home/goodguy: No such file or directory
$ pwd
/home/bj-is
```
### 🌞 Modifier les permissions de /home/goodguy
```bash
bj-is@tpos:~$ sudo chown -R imbob goodguy
```
### 🌞 Modifier les permissions de /home/badguy
```bash
bj-is@tpos:~$ sudo chown -R imnotbobsorry badguy
```
### 🌞 Connectez-vous sur l'utilisateur imbob
```bash
bj-is@tpos:~$ su - imbob
Password:
```
### 🌞 Connectez-vous sur l'utilisateur imnotbobsorry
```bash

```
