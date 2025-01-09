### 2. Premiers pas scripting
### 🌞 Ecrire un script qui produit exactement l'affichage demandé
```bash
[rock-bji@node1 ~]$ cat /opt/id.sh
#!/bin/bash
# script pour afficher les informations de connexion
# bji 08/12/2024
echo "Salue a toi ${USER}."
USER=$(whoami)
DATE=$(who | awk '{print $3" "$4"."}')
echo "Nouvelle connection ${DATE}"
SHELL=$( cat /etc/passwd | grep $USER | cut -d: -f7)
echo "Connecté avec le shell ${SHELL}"
OS=$(source /etc/os-release; echo $PRETTY_NAME)
KERNEL=$(uname -r)
echo "OS : ${OS} - KERNEL : ${KERNEL}"
echo "Ressources :"
RAM=$(free -mh | grep 'Mem:' | tr -s ' ' | cut -d' ' -f7)

echo "${RAM} RAM dispo"

DISK=$(df -h | grep "dev/mapper" | tr -s ' ' | cut -d ' ' -f2)
echo "${DISK} espace disque dispo"

INODE=$(df -i | grep "dev/mapper" | tr -s ' ' | cut -d ' ' -f2)
echo "${INODE} fichiers restants"

echo " Actuellement : "
PACKETS=$(rpm -qa | wc -l)
echo "${PACKETS} paquets installés"

PORTS=$(ss -tuln | wc -l)
echo "${PORTS} port(s) ouvert(s)"
PYTHON=$(which python3)
echo " Python est bien installé sur la machine au chemin : ${PYTHON}"
```
### 3. Amélioration du script
### 🌞 Le script id.sh affiche l'état du firewall
```bash
[rock-bji@node1 ~]$ cat /opt/id.sh
#!/bin/bash
# script pour afficher les informations de connexion
# bji 08/12/2024
echo "Salue a toi ${USER}."
USER=$(whoami)
DATE=$(who | awk '{print $3" "$4"."}')
echo "Nouvelle connection ${DATE}"
SHELL=$( cat /etc/passwd | grep $USER | cut -d: -f7)
echo "Connecté avec le shell ${SHELL}"
OS=$(source /etc/os-release; echo $PRETTY_NAME)
KERNEL=$(uname -r)
echo "OS : ${OS} - KERNEL : ${KERNEL}"
echo "Ressources :"
RAM=$(free -mh | grep 'Mem:' | tr -s ' ' | cut -d' ' -f7)

echo "${RAM} RAM dispo"

DISK=$(df -h | grep "dev/mapper" | tr -s ' ' | cut -d ' ' -f2)
echo "${DISK} espace disque dispo"

INODE=$(df -i | grep "dev/mapper" | tr -s ' ' | cut -d ' ' -f2)
echo "${INODE} fichiers restants"

echo " Actuellement : "
PACKETS=$(rpm -qa | wc -l)
echo "${PACKETS} paquets installés"

PORTS=$(ss -tuln | wc -l)
echo "${PORTS} port(s) ouvert(s)"
PYTHON=$(which python3)
echo " Python est bien installé sur la machine au chemin : ${PYTHON}"
# valeur a comprarer
statut=$(systemctl is-active firewalld)
#vérification
if [ "$statut" = "active" ]; then
        echo "Le firewall est actif."
else
        echo "Le firewall est inactif."
fi
```
### 🌞 Le script id.sh affiche l'URL vers une photo de chat random
```bash
[rock-bji@node1 ~]$ cat /opt/id.sh
#!/bin/bash
# script pour afficher les informations de connexion
# bji 08/12/2024
echo "Salue a toi ${USER}."
USER=$(whoami)
DATE=$(who | awk '{print $3" "$4"."}')
echo "Nouvelle connection ${DATE}"
SHELL=$( cat /etc/passwd | grep $USER | cut -d: -f7)
echo "Connecté avec le shell ${SHELL}"
OS=$(source /etc/os-release; echo $PRETTY_NAME)
KERNEL=$(uname -r)
echo "OS : ${OS} - KERNEL : ${KERNEL}"
echo "Ressources :"
RAM=$(free -mh | grep 'Mem:' | tr -s ' ' | cut -d' ' -f7)

echo "${RAM} RAM dispo"

DISK=$(df -h | grep "dev/mapper" | tr -s ' ' | cut -d ' ' -f2)
echo "${DISK} espace disque dispo"

INODE=$(df -i | grep "dev/mapper" | tr -s ' ' | cut -d ' ' -f2)
echo "${INODE} fichiers restants"

echo " Actuellement : "
PACKETS=$(rpm -qa | wc -l)
echo "${PACKETS} paquets installés"

PORTS=$(ss -tuln | wc -l)
echo "${PORTS} port(s) ouvert(s)"
PYTHON=$(which python3)
echo " Python est bien installé sur la machine au chemin : ${PYTHON}"
# valeur a comprarer
statut=$(systemctl is-active firewalld)
#vérification
if [ "$statut" = "active" ]; then
        echo "Le firewall est actif."
else
        echo "Le firewall est inactif."
fi

CHAT=$(curl https://api.thecatapi.com/v1/images/search | cut -d'"'  -f8)
echo "Voilà ta photo de chat : ${CHAT}"
```
### 4. Bannière
### 🌞 Stocker le fichier id.sh dans /opt
### 🌞 Prouvez que tout le monde peut exécuter le script
```bash
[rock-bji@node1 ~]$ ls -al /opt/id.sh
-rwxr-xr-x. 1 rock-bji rock-bji 1257 Dec 16 16:21 /opt/id.sh
```
### 🌞 Ajouter l'exécution au .bashrc de votre utilisateur
```bash
PS C:\Users\jerem> ssh rock-bji@192.168.20.10
rock-bji@192.168.20.10's password:
Last login: Mon Dec 16 16:49:19 2024 from 192.168.20.1
Salue a toi rock-bji.
Nouvelle connection 2024-12-16 16:55.
Connecté avec le shell /bin/bash
OS : Rocky Linux 9.5 (Blue Onyx) - KERNEL : 5.14.0-503.14.1.el9_5.x86_64
Ressources :
1.4Gi RAM dispo
6.2G espace disque dispo
3248128 fichiers restants
 Actuellement :
359 paquets installés
5 port(s) ouvert(s)
 Python est bien installé sur la machine au chemin : /usr/bin/python3
Le firewall est actif.
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--    100    90  100    90    0     0    217      0 --:--:-- --:--:-- --:--:--   218
Voilà ta photo de chat : https://cdn2.thecatapi.com/images/auq.jpg
```
