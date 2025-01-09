## 2. Let's go
### 🌞 Afficher la quantité d'espace disque disponible
```bash
[rock-bji@node1 ~]$ df -h | grep "dev/mapper" | tr -s ' ' | cut -d ' ' -f2
6.2G
```
### 🌞 Afficher combien de fichiers il est possible de créer
```bash
[rock-bji@node1 ~]$ df -i | grep "dev/mapper" | tr -s ' ' | cut -d ' ' -f2
3248128
```
### 🌞 Afficher l'heure et la date
```bash
[rock-bji@node1 ~]$ date +"%d/%m/%y %H:%M:%S"
09/12/24 17:24:04
```
### 🌞 Afficher la version de l'OS précise
```bash
[rock-bji@node1 ~]$  cat source /etc/os-release
[rock-bji@node1 ~]$ echo $PRETTY_NAME
Rocky Linux 9.5 (Blue Onyx)
```
### 🌞 Afficher la version du kernel en cours d'utilisation précise
```bash
[rock-bji@node1 ~]$ uname -r
5.14.0-503.14.1.el9_5.x86_64
```
### 🌞 Afficher le chemin vers la commande python3
```bash
[rock-bji@node1 ~]$ which python3
/usr/bin/python3
```
### 🌞 Afficher l'utilisateur actuellement connecté
```bash
[rock-bji@node1 ~]$ echo $USER
rock-bji
```
### 🌞 Afficher le shell par défaut de votre utilisateur actuellement connecté
```bash
[rock-bji@node1 ~]$ cat /etc/passwd | grep $USER | cut -d: -f7
/bin/bash
```
### 🌞 Afficher le nombre de paquets installés
```bash
[rock-bji@node1 ~]$ rpm -qa | wc -l
359
```
### 🌞 Afficher le nombre de ports en écoute
```bash
[rock-bji@node1 ~]$ ss -tuln | wc -l
5
```
