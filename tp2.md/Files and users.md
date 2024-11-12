## 🌞 Trouver le chemin du fichier de configuration du serveur SSH
```bash
PS C:\Users\jerem> ssh bj-is@192.168.20.3
bj-is@192.168.20.3's password:
bj-is@tpos:~$ /etc/passwd
-bash: /etc/passwd: Permission denied
bj-is@tpos:~$ nano /etc/passwd
bj-is@tpos:~$ pwd
/home/bj-is
bj-is@tpos:~$ ls -l
total 36
drwxr-xr-x 2 bj-is bj-is 4096 Nov  6 06:02 Desktop
drwxr-xr-x 2 bj-is bj-is 4096 Nov  6 06:02 Documents
drwxr-xr-x 2 bj-is bj-is 4096 Nov  6 06:02 Downloads
drwxr-xr-x 5 bj-is bj-is 4096 Nov 11 14:51 gameshell
drwxr-xr-x 2 bj-is bj-is 4096 Nov  6 06:02 Music
drwxr-xr-x 2 bj-is bj-is 4096 Nov  6 06:02 Pictures
drwxr-xr-x 2 bj-is bj-is 4096 Nov  6 06:02 Public
drwxr-xr-x 2 bj-is bj-is 4096 Nov  6 06:02 Templates
drwxr-xr-x 2 bj-is bj-is 4096 Nov  6 06:02 Videos
bj-is@tpos:~$ ls -l /home/bj-is
total 36
drwxr-xr-x 2 bj-is bj-is 4096 Nov  6 06:02 Desktop
drwxr-xr-x 2 bj-is bj-is 4096 Nov  6 06:02 Documents
drwxr-xr-x 2 bj-is bj-is 4096 Nov  6 06:02 Downloads
drwxr-xr-x 5 bj-is bj-is 4096 Nov 11 14:51 gameshell
drwxr-xr-x 2 bj-is bj-is 4096 Nov  6 06:02 Music
drwxr-xr-x 2 bj-is bj-is 4096 Nov  6 06:02 Pictures
drwxr-xr-x 2 bj-is bj-is 4096 Nov  6 06:02 Public
drwxr-xr-x 2 bj-is bj-is 4096 Nov  6 06:02 Templates
drwxr-xr-x 2 bj-is bj-is 4096 Nov  6 06:02 Videos
bj-is@tpos:~$ f
factor        fc-list       fgrep         firefox       free
faillog       fc-match      fi            firefox-esr   function
fallocate     fc-pattern    file          flock         funzip
false         fc-query      file2brl      fmt           fuser
fc            fc-scan       fincore       fold          fusermount
fc-cache      fc-validate   find          fonttosfnt    fusermount3
fc-cat        fg            findaffix     foomatic-rip
fc-conflist   fgconsole     findmnt       for
root@tpos:~# exit
logout
```

## 🌞 Trouver le chemin du fichier de configuration du serveur SSH
```bash
bj-is@tpos:~$ su - root
Password:
root@tpos:~# find sshd_config -name
find: missing argument to `-name'
root@tpos:~# find -iname "ssh_config"
root@tpos:~# find / -iname "ssh_config"
/etc/ssh/ssh_config
root@tpos:~# exit
logout
```

## 2. Users
## A. Nouveau user
### 🌞 Créer un nouvel utilisateur
```bash
bj-is@tpos:~$ su - root
Password:
root@tpos:~# useradd -m -d /home/papier_alu/ marmotte
root@tpos:~# passwd marmotte
New password:
Retype new password:
passwd: password updated successfully
root@tpos:~# exit
logout
bj-is@tpos:~$ su - marmotte
Password:
$
```

## 🌞 Prouver que cet utilisateur a été créé
```bash
bj-is@tpos:~$ cat /etc/passwd | grep marmotte
marmotte:x:1001:1001::/home/papier_alu/:/bin/sh
```

## 🌞 Déterminer le hash du password de l'utilisateur marmotte
```bash
bj-is@tpos:~$ su - root
root@tpos:~# cat /etc/shadow | grep marmotte
marmotte:$y$j9T$GKF8sAPrcP.USMc8z7gt80$E7YiwTCEwMfvL0NRhCBaV1rPPlexDFLnuep9rFKCbAC:20039:0:99999:7:::
```

## 🌞 Assurez-vous que vous pouvez vous connecter en tant que l'utilisateur marmotte
```bash
bj-is@tpos:~$ logout
Connection to 192.168.20.3 closed.
```
## 🌞 Assurez-vous que vous pouvez vous connecter en tant que l'utilisateur marmotte
```bash
PS C:\Users\jerem> ssh bj-is@192.168.20.3
bj-is@192.168.20.3's password:
Linux tpos 6.1.0-26-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.1.112-1 (2024-09-30) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Tue Nov 12 06:00:46 2024 from 192.168.20.1
bj-is@tpos:~$ su - marmotte
Password:
$ ls /home/bj-is
ls: cannot open directory '/home/bj-is': Permission denied
```
