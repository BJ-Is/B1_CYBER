## 1. Jouer avec la commande ps
### 🌞 Affichez les processus bash
```bash
bj-is@tpos:~$ ps -ef | grep bash
bj-is        890     886  0 20:20 pts/0    00:00:00 -bash
bj-is        942     890  0 20:21 pts/0    00:00:00 grep bash
```
### 🌞 Affichez tous les processus lancés par votre utilisateur
```bash
bj-is@tpos:~$ ps -f -u bj-is
UID          PID    PPID  C STIME TTY          TIME CMD
bj-is        741       1  0 20:19 ?        00:00:00 /usr/bin/python3 -m http
bj-is        864       1  0 20:20 ?        00:00:00 /usr/lib/systemd/systemd
bj-is        865     864  0 20:20 ?        00:00:00 (sd-pam)
bj-is        881     864  0 20:20 ?        00:00:00 /usr/bin/pulseaudio --da
bj-is        886     860  0 20:20 ?        00:00:00 sshd-session: bj-is@pts/
bj-is        890     886  0 20:20 pts/0    00:00:00 -bash
bj-is        940     864  0 20:20 ?        00:00:00 /usr/bin/dbus-daemon --s
bj-is        948     890 99 20:26 pts/0    00:00:00 ps -f -u bj-is
```
### 🌞 Affichez le top 5 des processus qui utilisent le plus de RAM
```bash
bj-is@tpos:~$ top -o %MEM
top - 20:44:29 up 24 min,  1 user,  load average: 0.00, 0.00, 0.00
Tasks: 105 total,   1 running, 104 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0. MiB Mem :   3915.3 total,   3411.7 free,    445.4 used,    272.4 buff/cache MiB Swap:    975.0 total,    975.0 free,      0.0 used.   3469.8 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+
    801 lightdm   20   0  752020 110048  76868 S   0.3   2.7   0:01.90          761 exroot    20   0  352096  76036  57160 S   0.0   1.9   0:01.02          610 exroot    20   0  334952  19944  15224 S   0.0   0.5   0:00.22          241 exroot    20   0   49812  18116  14876 S   0.0   0.5   0:00.20
    741 bj-is     20   0   29472  17896   8712 S   0.0   0.4   0:00.65 
```
### 🌞 Affichez le PID du processus du service SSH
```bash
bj-is@tpos:~$ pidof sshd
746
```
### 🌞 Affichez le nom du processus avec l'identifiant le plus petit
```bash
bj-is@tpos:~$ ps -eo pid,comm --sort=pid | awk 'NR==2'
      1 systemd
```
## 2. Parent, enfant, et meurtre
### 🌞 Déterminer le PID de votre shell actuel
```bash
bj-is@tpos:~$ ps -p $$
    PID TTY          TIME CMD
    890 pts/0    00:00:00 bash
```
### 🌞 Déterminer le PPID de votre shell actuel
```bash
bj-is@tpos:~$ echo $PPID
886
```
### 🌞 Déterminer le nom de ce processus
```bash
bj-is@tpos:~$ ps -p 886
    PID TTY          TIME CMD
    886 ?        00:00:00 sshd-session
```
### 🌞 Lancer un processus sleep 9999 en tâche de fond
```bash
bj-is@tpos:~$ sleep 9999 &
[1] 1048

bj-is@tpos:~$ pidof sleep
1048

bj-is@tpos:~$ ps -eo pid,ppid,comm | grep "sleep"
   1048     890 sleep
```
### 🌞 Fermez votre session SSH
```bash
bj-is@tpos:~$ exit
logout
Connection to 192.168.20.3 closed.
PS C:\Users\jerem> ssh bj-is@192.168.20.3
bj-is@192.168.20.3's password:
Linux tpos 6.1.0-27-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.1.115-1 (2024-11-01) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Wed Nov 27 20:20:12 2024 from 192.168.20.1
bj-is@tpos:~$ ps aux | grep "sleep 9999"
bj-is       1048  0.0  0.0   5568  1068 ?        S    21:35   0:00 sleep 9999
bj-is       1073 50.0  0.0   6436  2188 pts/1    S+   21:46   0:00 grep sleep 9999
```
