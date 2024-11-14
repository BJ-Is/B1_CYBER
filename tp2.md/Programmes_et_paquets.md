## 1 Programmes et paquets
## A. Run then kill
### 🌞 Lancer un processus sleep
```bash
bj-is@tpos:~$ ps -ef |grep sleep
bj-is       2089    1916  0 03:22 pts/2    00:00:00 grep sleep
```

### 🌞 Terminez le processus sleep depuis le deuxième terminal
```bash
bj-is@tpos:~$ kill 1916
```
### 🌞 Lancer un nouveau processus sleep, mais en tâche de fondbj-is@tpos:~$ sleep 40&
```bash
bj-is@tpos:~$ sleep 1000 &
[1] 2147
bj-is@tpos:~$
```
### 🌞 Visualisez la commande en tâche de fond
```bash
bj-is@tpos:~$ ps -ef |grep sleep
bj-is       2147    1916  0 04:12 pts/2    00:00:00 sleep 1000
bj-is       2149    1916  0 04:13 pts/2    00:00:00 grep sleep
bj-is@tpos:~$
```
### 🌞 Trouver le chemin où est stocké le programme sleep 
### avec une commande find
```bash
bj-is@tpos:~$ sudo find / -iname sleep
/usr/lib/klibc/bin/sleep
/usr/bin/sleep
```
### 🌞 Tant qu'on est à chercher des chemins : trouver les chemins vers tous les fichiers qui s'appellent .bashrc
```bash
bj-is@tpos:~$ sudo find / -iname .bashrc
/etc/skel/.bashrc
/home/bj-is/gameshell/gameshell.1/World/.bashrc
/home/bj-is/gameshell/gameshell/World/.bashrc
/home/bj-is/.bashrc
/home/papier_alu/.bashrc
/root/.bashrc
```
### 🌞 Vérifier que les commandes sleep, ssh, et ping sont bien des programmes stockés dans l'un des dossiers listés dans votre PATH
```bash
bj-is@tpos:~$ echo $PATH
/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games
bj-is@tpos:~$ which sleep
/usr/bin/sleep
bj-is@tpos:~$ which ssh
/usr/bin/ssh
bj-is@tpos:~$ which ping
/usr/bin/ping
```
### 🌞 Mais aussi déterminer l'adresse http ou https des serveurs où vous téléchargez des paquets
```bash
bj-is@tpos:~$ nano /etc/apt/sources.list
```
```bash
#deb cdrom:[Debian GNU/Linux 12.7.0 _Bookworm_ - Official amd64 NETINST with firmware 20240831-10:38]/ bookworm contrib>

deb http://deb.debian.org/debian/ bookworm main non-free-firmware
deb-src http://deb.debian.org/debian/ bookworm main non-free-firmware

deb http://security.debian.org/debian-security bookworm-security main non-free-firmware
deb-src http://security.debian.org/debian-security bookworm-security main non-free-firmware

# bookworm-updates, to get updates before a point release is made;
# see https://www.debian.org/doc/manuals/debian-reference/ch02.en.html#_updates_and_backports
deb http://deb.debian.org/debian/ bookworm-updates main non-free-firmware
deb-src http://deb.debian.org/debian/ bookworm-updates main non-free-firmware

# This system was installed using small removable media
# (e.g. netinst, live or single CD). The matching "deb cdrom"
# entries were disabled at the end of the installation process.
# For information about how to configure apt package sources,
# see the sources.list(5) manual.
```
