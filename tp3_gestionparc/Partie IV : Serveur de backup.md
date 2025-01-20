### 🌞 Partitionner le disque dur
```bash

[rock-bji@backup ~]$ lsblk
NAME             MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda                8:0    0    8G  0 disk
├─sda1             8:1    0    1G  0 part /boot
└─sda2             8:2    0    7G  0 part
  ├─rl_vbox-root 253:0    0  6.2G  0 lvm  /
  └─rl_vbox-swap 253:1    0  820M  0 lvm  [SWAP]
sdb                8:16   0  500M  0 disk
sdc                8:32   0    5G  0 disk
└─sdc1             8:33   0    5G  0 part
sr0               11:0    1 1024M  0 rom
```
### 🌞 Formater la partition créée
```bash
[rock-bji@backup ~]$ sudo mkfs.ext4 /dev/sdc1
mke2fs 1.46.5 (30-Dec-2021)
Creating filesystem with 1310464 4k blocks and 327680 inodes
Filesystem UUID: 661a2719-14a0-4775-8dce-6474511e8ee5
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912, 819200, 884736

Allocating group tables: done
Writing inode tables: done
Creating journal (16384 blocks): done
Writing superblocks and filesystem accounting information: done
```
### 🌞 Monter la partition
```bash
[rock-bji@backup ~]$ sudo mkdir -p /mnt/backup
[rock-bji@backup ~]$ sudo mount /dev/sdc1 /mnt/backup
```
### 🌞 Configurer un montage automatique de la partition
```bash
[rock-bji@backup ~]$ echo '/dev/sdc1 /mnt/backup ext4 defaults 0 0' | sudo tee
 -a /etc/fstab
/dev/sdc1 /mnt/backup ext4 defaults 0 0
```
### 🌞 Installer et configurer un service NFS
```bash
[rock-bji@music ~]$ sudo dnf install nfs-utils
Last metadata expiration check: 0:21:02 ago on Mon 20 Jan 2025 05:04:56 PM CET.
Dependencies resolved.
============================================================================
 Package               Arch        Version                Repository   Size
============================================================================
Installing:
 nfs-utils             x86_64      1:2.5.4-27.el9         baseos      431 k
Upgrading:
 libsss_certmap        x86_64      2.9.5-4.el9_5.4        baseos       90 k
 libsss_idmap          x86_64      2.9.5-4.el9_5.4        baseos       41 k
 libsss_nss_idmap      x86_64      2.9.5-4.el9_5.4        baseos       45 k
 libsss_sudo           x86_64      2.9.5-4.el9_5.4        baseos       35 k
 sssd-client           x86_64      2.9.5-4.el9_5.4        baseos      161 k
 sssd-common           x86_64      2.9.5-4.el9_5.4        baseos      1.6 M
 sssd-kcm              x86_64      2.9.5-4.el9_5.4        baseos      109 k
Installing dependencies:
 gssproxy              x86_64      0.8.4-7.el9            baseos      108 k
 libev                 x86_64      4.33-5.el9.0.1         baseos       51 k
 libnfsidmap           x86_64      1:2.5.4-27.el9         baseos       59 k
 libtirpc              x86_64      1.3.3-9.el9            baseos       93 k
 libverto-libev        x86_64      0.3.2-3.el9            baseos       13 k
 python3-pyyaml        x86_64      5.4.1-6.el9            baseos      191 k
 quota                 x86_64      1:4.09-2.el9           baseos      190 k
 quota-nls             noarch      1:4.09-2.el9           baseos       76 k
 rpcbind               x86_64      1.2.6-7.el9            baseos       56 k
 sssd-nfs-idmap        x86_64      2.9.5-4.el9_5.4        baseos       39 k

Transaction Summary
============================================================================
Install  11 Packages
Upgrade   7 Packages

Total download size: 3.3 M
Is this ok [y/N]: y
Downloading Packages:
(1/18): libverto-libev-0.3.2-3.el9.x86_64.r  67 kB/s |  13 kB     00:00
(2/18): quota-nls-4.09-2.el9.noarch.rpm     317 kB/s |  76 kB     00:00
(3/18): libtirpc-1.3.3-9.el9.x86_64.rpm     298 kB/s |  93 kB     00:00
(4/18): quota-4.09-2.el9.x86_64.rpm         361 kB/s | 190 kB     00:00
(5/18): rpcbind-1.2.6-7.el9.x86_64.rpm      244 kB/s |  56 kB     00:00
(6/18): libev-4.33-5.el9.0.1.x86_64.rpm     233 kB/s |  51 kB     00:00
(7/18): python3-pyyaml-5.4.1-6.el9.x86_64.r 339 kB/s | 191 kB     00:00
(8/18): gssproxy-0.8.4-7.el9.x86_64.rpm     689 kB/s | 108 kB     00:00
(9/18): sssd-nfs-idmap-2.9.5-4.el9_5.4.x86_ 162 kB/s |  39 kB     00:00
(10/18): libnfsidmap-2.5.4-27.el9.x86_64.rp 544 kB/s |  59 kB     00:00
(11/18): sssd-kcm-2.9.5-4.el9_5.4.x86_64.rp 443 kB/s | 109 kB     00:00
(12/18): nfs-utils-2.5.4-27.el9.x86_64.rpm  712 kB/s | 431 kB     00:00
(13/18): libsss_sudo-2.9.5-4.el9_5.4.x86_64 524 kB/s |  35 kB     00:00
(14/18): libsss_nss_idmap-2.9.5-4.el9_5.4.x 262 kB/s |  45 kB     00:00
(15/18): sssd-client-2.9.5-4.el9_5.4.x86_64 389 kB/s | 161 kB     00:00
(16/18): libsss_idmap-2.9.5-4.el9_5.4.x86_6 442 kB/s |  41 kB     00:00
(17/18): libsss_certmap-2.9.5-4.el9_5.4.x86 461 kB/s |  90 kB     00:00
(18/18): sssd-common-2.9.5-4.el9_5.4.x86_64 1.5 MB/s | 1.6 MB     00:01
----------------------------------------------------------------------------
Total                                       1.3 MB/s | 3.3 MB     00:02
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                    1/1
  Installing       : libtirpc-1.3.3-9.el9.x86_64                       1/25
  Upgrading        : libsss_idmap-2.9.5-4.el9_5.4.x86_64               2/25
  Installing       : libnfsidmap-1:2.5.4-27.el9.x86_64                 3/25
  Installing       : sssd-nfs-idmap-2.9.5-4.el9_5.4.x86_64             4/25
  Running scriptlet: rpcbind-1.2.6-7.el9.x86_64                        5/25
  Installing       : rpcbind-1.2.6-7.el9.x86_64                        5/25
  Running scriptlet: rpcbind-1.2.6-7.el9.x86_64                        5/25
Created symlink /etc/systemd/system/multi-user.target.wants/rpcbind.service → /usr/lib/systemd/system/rpcbind.service.
Created symlink /etc/systemd/system/sockets.target.wants/rpcbind.socket → /usr/lib/systemd/system/rpcbind.socket.

  Upgrading        : libsss_certmap-2.9.5-4.el9_5.4.x86_64             6/25
  Upgrading        : libsss_nss_idmap-2.9.5-4.el9_5.4.x86_64           7/25
  Upgrading        : sssd-client-2.9.5-4.el9_5.4.x86_64                8/25
  Running scriptlet: sssd-client-2.9.5-4.el9_5.4.x86_64                8/25
  Upgrading        : libsss_sudo-2.9.5-4.el9_5.4.x86_64                9/25
  Running scriptlet: sssd-common-2.9.5-4.el9_5.4.x86_64               10/25
  Upgrading        : sssd-common-2.9.5-4.el9_5.4.x86_64               10/25
  Running scriptlet: sssd-common-2.9.5-4.el9_5.4.x86_64               10/25
  Installing       : libev-4.33-5.el9.0.1.x86_64                      11/25
  Installing       : libverto-libev-0.3.2-3.el9.x86_64                12/25
  Installing       : gssproxy-0.8.4-7.el9.x86_64                      13/25
  Running scriptlet: gssproxy-0.8.4-7.el9.x86_64                      13/25
  Installing       : python3-pyyaml-5.4.1-6.el9.x86_64                14/25
  Installing       : quota-nls-1:4.09-2.el9.noarch                    15/25
  Installing       : quota-1:4.09-2.el9.x86_64                        16/25
  Running scriptlet: nfs-utils-1:2.5.4-27.el9.x86_64                  17/25
  Installing       : nfs-utils-1:2.5.4-27.el9.x86_64                  17/25
  Running scriptlet: nfs-utils-1:2.5.4-27.el9.x86_64                  17/25
  Upgrading        : sssd-kcm-2.9.5-4.el9_5.4.x86_64                  18/25
  Running scriptlet: sssd-kcm-2.9.5-4.el9_5.4.x86_64                  18/25
  Running scriptlet: sssd-kcm-2.9.5-4.el9_5.1.x86_64                  19/25
  Cleanup          : sssd-kcm-2.9.5-4.el9_5.1.x86_64                  19/25
  Running scriptlet: sssd-kcm-2.9.5-4.el9_5.1.x86_64                  19/25
  Running scriptlet: sssd-common-2.9.5-4.el9_5.1.x86_64               20/25
  Cleanup          : sssd-common-2.9.5-4.el9_5.1.x86_64               20/25
  Running scriptlet: sssd-common-2.9.5-4.el9_5.1.x86_64               20/25
  Running scriptlet: sssd-client-2.9.5-4.el9_5.1.x86_64               21/25
  Cleanup          : sssd-client-2.9.5-4.el9_5.1.x86_64               21/25
  Cleanup          : libsss_idmap-2.9.5-4.el9_5.1.x86_64              22/25
  Cleanup          : libsss_nss_idmap-2.9.5-4.el9_5.1.x86_64          23/25
  Cleanup          : libsss_sudo-2.9.5-4.el9_5.1.x86_64               24/25
  Cleanup          : libsss_certmap-2.9.5-4.el9_5.1.x86_64            25/25
  Running scriptlet: sssd-common-2.9.5-4.el9_5.4.x86_64               25/25
  Running scriptlet: libsss_certmap-2.9.5-4.el9_5.1.x86_64            25/25
  Verifying        : libverto-libev-0.3.2-3.el9.x86_64                 1/25
  Verifying        : quota-1:4.09-2.el9.x86_64                         2/25
  Verifying        : quota-nls-1:4.09-2.el9.noarch                     3/25
  Verifying        : libtirpc-1.3.3-9.el9.x86_64                       4/25
  Verifying        : python3-pyyaml-5.4.1-6.el9.x86_64                 5/25
  Verifying        : rpcbind-1.2.6-7.el9.x86_64                        6/25
  Verifying        : libev-4.33-5.el9.0.1.x86_64                       7/25
  Verifying        : sssd-nfs-idmap-2.9.5-4.el9_5.4.x86_64             8/25
  Verifying        : gssproxy-0.8.4-7.el9.x86_64                       9/25
  Verifying        : nfs-utils-1:2.5.4-27.el9.x86_64                  10/25
  Verifying        : libnfsidmap-1:2.5.4-27.el9.x86_64                11/25
  Verifying        : sssd-kcm-2.9.5-4.el9_5.4.x86_64                  12/25
  Verifying        : sssd-kcm-2.9.5-4.el9_5.1.x86_64                  13/25
  Verifying        : sssd-common-2.9.5-4.el9_5.4.x86_64               14/25
  Verifying        : sssd-common-2.9.5-4.el9_5.1.x86_64               15/25
  Verifying        : sssd-client-2.9.5-4.el9_5.4.x86_64               16/25
  Verifying        : sssd-client-2.9.5-4.el9_5.1.x86_64               17/25
  Verifying        : libsss_sudo-2.9.5-4.el9_5.4.x86_64               18/25
  Verifying        : libsss_sudo-2.9.5-4.el9_5.1.x86_64               19/25
  Verifying        : libsss_nss_idmap-2.9.5-4.el9_5.4.x86_64          20/25
  Verifying        : libsss_nss_idmap-2.9.5-4.el9_5.1.x86_64          21/25
  Verifying        : libsss_idmap-2.9.5-4.el9_5.4.x86_64              22/25
  Verifying        : libsss_idmap-2.9.5-4.el9_5.1.x86_64              23/25
  Verifying        : libsss_certmap-2.9.5-4.el9_5.4.x86_64            24/25
  Verifying        : libsss_certmap-2.9.5-4.el9_5.1.x86_64            25/25

Upgraded:
  libsss_certmap-2.9.5-4.el9_5.4.x86_64
  libsss_idmap-2.9.5-4.el9_5.4.x86_64
  libsss_nss_idmap-2.9.5-4.el9_5.4.x86_64
  libsss_sudo-2.9.5-4.el9_5.4.x86_64
  sssd-client-2.9.5-4.el9_5.4.x86_64
  sssd-common-2.9.5-4.el9_5.4.x86_64
  sssd-kcm-2.9.5-4.el9_5.4.x86_64
Installed:
  gssproxy-0.8.4-7.el9.x86_64             libev-4.33-5.el9.0.1.x86_64
  libnfsidmap-1:2.5.4-27.el9.x86_64       libtirpc-1.3.3-9.el9.x86_64
  libverto-libev-0.3.2-3.el9.x86_64       nfs-utils-1:2.5.4-27.el9.x86_64
  python3-pyyaml-5.4.1-6.el9.x86_64       quota-1:4.09-2.el9.x86_64
  quota-nls-1:4.09-2.el9.noarch           rpcbind-1.2.6-7.el9.x86_64
  sssd-nfs-idmap-2.9.5-4.el9_5.4.x86_64

Complete!
```
### 🌞 Essayer d'accéder au dossier partagé
```bash
[rock-bji@backup ~]$ sudo mkdir -p /mnt/music_backup

[rock-bji@backup ~]$ sudo mount backup.tp3.b1:/mnt/backup /mnt/music_backup
[sudo] password for rock-bji:
mount: (hint) your fstab has been modified, but systemd still uses
       the old version; use 'systemctl daemon-reload' to reload.
[rock-bji@backup ~]$ sudo systemctl daemon-reload
[rock-bji@backup ~]$ df -h /mnt/music_backup
Filesystem                 Size  Used Avail Use% Mounted on
backup.tp3.b1:/mnt/backup  4.9G     0  4.6G   0% /mnt/music_backup
```
### 🌞 Configurer un montage automatique
```bash
[rock-bji@backup ~]$ echo 'backup.tp3.b1:/mnt/backup /mnt/music_backup nfs defaults 0 0' | sudo tee -a /etc/fstab
[sudo] password for rock-bji:
backup.tp3.b1:/mnt/backup /mnt/music_backup nfs defaults 0 0
```
### 🌞 Script backup.sh
```bash
[rock-bji@music ~]$ cat /opt/backup.sh
#!/bin/bash

DATE=$(date +%y%m%d_%H%M%S)
BACKUP_DIR="/mnt/music_backup"
SOURCE_DIR="/var/lib/jellyfin/music"

tar -czf $BACKUP_DIR/music_$DATE.tar.gz $SOURCE_DIR

if [ $? -eq 0 ]; then
    echo "Backup successful: music_$DATE.tar.gz"
else
    echo "Backup failed"
fi

[rock-bji@music ~]$ sudo /opt/backup.sh
tar: Removing leading `/' from member names
Backup successful: music_250120_180458.tar.gz
```
### B. Sauvegarde à intervalles réguliers
### 🌞 Créer un nouveau service backup.service
```bash
[rock-bji@music ~]$ cat /etc/systemd/system/backup.service
[Unit]
Description=Backup service for Jellyfin music

[Service]
Type=oneshot
ExecStart=/opt/backup.sh

[Install]
WantedBy=multi-user.target
```
### ### 🌞 Indiquer au système qu'on a ajouté un nouveau service
```bash
[rock-bji@music ~]$ sudo systemctl daemon-reload
```
### 🌞 Utiliser et tester le nouveau service
### 🌞 Faire un test et prouvez que ça a fonctionné
```bash
[rock-bji@music ~]$ systemctl status backup
○ backup.service - Backup service for Jellyfin music
     Loaded: loaded (/etc/systemd/system/backup.service; enabled; preset: d>
     Active: inactive (dead)

Jan 20 18:13:19 music.tp3.b3 systemd[1]: Starting Backup service for Jellyf>
Jan 20 18:13:19 music.tp3.b3 backup.sh[3494]: tar: Removing leading `/' fro>
Jan 20 18:13:19 music.tp3.b3 backup.sh[3492]: Backup successful: music_2501>
Jan 20 18:13:19 music.tp3.b3 systemd[1]: backup.service: Deactivated succes>
Jan 20 18:13:19 music.tp3.b3 systemd[1]: Finished Backup service for Jellyf>
Jan 20 18:19:57 music.tp3.b3 systemd[1]: Starting Backup service for Jellyf>
Jan 20 18:19:57 music.tp3.b3 backup.sh[3511]: tar: Removing leading `/' fro>
Jan 20 18:19:57 music.tp3.b3 backup.sh[3509]: Backup successful: music_2501>
Jan 20 18:19:57 music.tp3.b3 systemd[1]: backup.service: Deactivated succes>
Jan 20 18:19:57 music.tp3.b3 systemd[1]: Finished Backup service for Jellyf>
lines 1-14/14 (END)
```
### 🌞 Configurer un lancement automatique du service à intervalles réguliers
```bash
[rock-bji@music ~]$ cat /etc/systemd/system/backup.timer
[Unit]
Description=Run backup service every hour

[Timer]
OnCalendar=hourly
Persistent=true

[Install]
WantedBy=timers.target

[rock-bji@music ~]$ sudo systemctl list-timers
NEXT                        LEFT          LAST                        PASSE>
Mon 2025-01-20 18:58:51 CET 31min left    Mon 2025-01-20 17:03:34 CET 1h 24>
Mon 2025-01-20 19:00:00 CET 32min left    -                           -    >
Tue 2025-01-21 00:00:00 CET 5h 32min left Mon 2025-01-20 00:00:11 CET 18h a>
Tue 2025-01-21 16:15:34 CET 21h left      Mon 2025-01-20 16:15:34 CET 2h 12>

4 timers listed.
Pass --all to see loaded but inactive timers, too.
lines 1-8/8 (END)
```
