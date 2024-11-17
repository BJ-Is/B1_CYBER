### 🌞 Récupérer le fichier meow
```bash
bj-is@tpos:~$ wget https://gitlab.com/it4lik/b1-os/-/raw/main/tp/2/meow
--2024-11-14 10:04:12--  https://gitlab.com/it4lik/b1-os/-/raw/main/tp/2/meow
Resolving gitlab.com (gitlab.com)... 172.65.251.78, 2606:4700:90:0:f22e:fbec:5bed:a9b9
Connecting to gitlab.com (gitlab.com)|172.65.251.78|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 18016947 (17M) [application/octet-stream]
Saving to: ‘meow’

meow               100%[================>]  17.18M  20.0MB/s    in 0.9s

2024-11-14 10:04:13 (20.0 MB/s) - ‘meow’ saved [18016947/18016947]
```
### 🌞 Trouver le dossier dawa/

```bash
bj-is@tpos:~$ file meow
meow: Zip archive data, at least v2.0 to extract, compression method=deflate
```
```bash
bj-is@tpos:~$ mv meow meow.zip
```
### 🌞 Dans le dossier dawa/, déterminer le chemin vers
```bash
bj-is@tpos:~$ mv meow meow.zip
```
```bash
bj-is@tpos:~$ unzip "*meow.zip"
Archive:  meow.zip
  inflating: meow
bj-is@tpos:~$ mv meow meow.xz
bj-is@tpos:~$ xz -dk meow.xz
bj-is@tpos:~$ mv meow meow.bz2
bj-is@tpos:~$ bzip2 -dk meow.bz2
bj-is@tpos:~$ unrar-free meow.rar

unrar-free 0.1.3  Copyright (C) 2004  Ben Asselstine, Jeroen Dekkers


Extracting from /home/bj-is/meow.rar

Extracting  meow                                                      OK

All OK
bj-is@tpos:~$ mv meow meow.gz
bj-is@tpos:~$ gzip -dk meow.gz
bj-is@tpos:~$ mv meow meow.tar
bj-is@tpos:~$ tar xvf  meow.tar
```
- le seul fichier de 15Mo
```bash
bj-is@tpos:~$ find dawa -size 15M
dawa/folder31/19/file39
```
- le seul fichier qui ne contient que des 7
```bash
bj-is@tpos:~$  grep -r "7" /home/bj-is/dawa
```
- le seul fichier qui est nommé cookie
```bash
bj-is@tpos:~$  grep -r -i -l "cookie" /home/bj-is/dawa
```
- le seul fichier caché (un fichier caché c'est juste un fichier dont le nom commence par un .)
```bash
bj-is@tpos:~$ find /home/bj-is/dawa/ -name ".*" -ls
   529878      4 -rw-r--r--   1 bj-is    bj-is          11 Jan 21  2024 /home/bj-is/dawa/folder32/14/.hidden_file
```
- le seul fichier qui date de 2014
```bash
bj-is@tpos:~$ find dawa -mtime +2014
dawa/folder36/40/file43
```
