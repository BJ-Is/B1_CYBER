## II. Ptits challenges de cracking
### 🌞 Avec une commande apt search, déterminez si le paquet ghidra est disponible
```bash
```
### 🌞 Ajouter l'URL des dépôts Kali à vos dépôts existants
```bash
bj-is@tpos:~$ sudo nano /etc/apt/sources.list
[sudo] password for bj-is:
```
### 🌞 Ajoutez la clé publique des gars de chez Kali
```bash
bj-is@tpos:~$ sudo wget https://archive.kali.org/archive-key.asc -O /etc/apt
/trusted.gpg.d/kali-archive-keyring.asc
--2024-11-19 10:06:52--  https://archive.kali.org/archive-key.asc
Resolving archive.kali.org (archive.kali.org)... 192.99.45.140, 2607:5300:60:508c::
Connecting to archive.kali.org (archive.kali.org)|192.99.45.140|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3155 (3.1K) [application/octet-stream]
Saving to: ‘/etc/apt/trusted.gpg.d/kali-archive-keyring.asc’

/etc/apt/trusted.g 100%[================>]   3.08K  --.-KB/s    in 0s

2024-11-19 10:06:53 (31.8 MB/s) - ‘/etc/apt/trusted.gpg.d/kali-archive-keyring.asc’ saved [3155/3155]
```
### 🌞 Mettez à jour la liste des dépôts que votre OS connaît actuellement
```bash
bj-is@tpos:~$ sudo apt update -y
Hit:1 http://security.debian.org/debian-security bookworm-security InRelease
Hit:2 http://deb.debian.org/debian bookworm InRelease
Get:3 http://deb.debian.org/debian bookworm-updates InRelease [55.4 kB]
Get:4 http://kali.download/kali kali-rolling InRelease [41.5 kB]
Get:5 http://kali.download/kali kali-rolling/main amd64 Packages [20.3 MB]
Get:6 http://kali.download/kali kali-rolling/contrib amd64 Packages [112 kB]
Get:7 http://kali.download/kali kali-rolling/non-free amd64 Packages [197 kB]
Get:8 http://kali.download/kali kali-rolling/non-free-firmware amd64 Packages [10.6 kB]
Fetched 20.7 MB in 11s (1,882 kB/s)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
1225 packages can be upgraded. Run 'apt list --upgradable' to see them.
```
### 🌞 Avec une commande apt search, déterminez si le paquet ghidra est disponible
```bash
bj-is@tpos:~$ apt search ghidra
Sorting... Done
Full Text Search... Done
ghidra/kali-rolling 11.0+ds-0kali1 amd64
  Software Reverse Engineering Framework

ghidra-data/kali-rolling 10.5-0kali1 all
  FID databases for Ghidra

ghidra-dbgsym/kali-rolling 11.0+ds-0kali1 amd64
  debug symbols for ghidra

quark-engine/kali-rolling 23.9.1-0kali2 all
  Android Malware (Analysis | Scoring System)

rz-ghidra/kali-rolling 0.7.0-0kali1+b1 amd64
  ghidra decompiler and sleigh disassembler for rizin

rz-ghidra-dbgsym/kali-rolling 0.7.0-0kali1+b1 amd64
  debug symbols for rz-ghidra
```
### 🌞 Installez le paquet ghidra
```bash
```
### 2. Patch manuel programme simple
### 🌞 Récupérez le code de password_2.c sur la machine Linux et compilez-le
```bash
bj-is@tpos:~/work$ ./password_2.exe cdfvf
Access granted! Spawning shell...
$  
```
### 4. Ptit chall maison
### 🌞 Récupérer le flag du programme kaddate_challenge
```bash
```
