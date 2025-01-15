### script autoconfiguration
```bash
[rock-bji@vbox ~]$ cat /opt/autoconfig.sh
#!/bin/bash

log() {
    echo "$(date '+%H:%M:%S') [INFO] $1"
}

warn() {
    echo "$(date '+%H:%M:%S') [WARN] $1"
}

log "Le script d'autoconfiguration a démarré"

if [[ $(id -u) -ne 0 ]]; then
    warn "Le script doit être lancé en tant que root. Veuillez relancer avec sudo ou en root."
    exit 1
else
    log "Le script a bien été lancé en root."
fi

log "Vérification de l'état de SELinux..."
SELINUX_MODE=$(sestatus | grep "Current mode" | awk '{print $3}')
SELINUX_CONFIG=$(grep "^SELINUX=" /etc/selinux/config | cut -d= -f2)

if [[ "$SELINUX_MODE" != "permissive" ]]; then
    warn "SELinux est toujours activé !"
    log "Désactivation de SELinux temporaire (setenforce)"
    setenforce 0
fi

if [[ "$SELINUX_CONFIG" != "permissive" ]]; then
    log "Désactivation de SELinux définitive (fichier de config)"
    sed -i 's/^SELINUX=.*/SELINUX=permissive/' /etc/selinux/config
fi

log "Vérification de l'état du firewall"
if ! systemctl is-active --quiet firewalld; then
    warn "Le service firewalld n'est pas activé."
    exit 1
else
    log "Service de firewalling firewalld est activé."
fi

log "Vérification du port SSH"
SSH_PORT=$(grep "^Port" /etc/ssh/sshd_config | awk '{print $2}')

if [[ "$SSH_PORT" == "22" || -z "$SSH_PORT" ]]; then
    warn "Le service SSH tourne toujours sur le port 22/TCP."
    NEW_PORT=$((RANDOM % 64512 + 1024))
    log "Modification du fichier de configuration SSH pour écouter sur le port $NEW_PORT/TCP"
    sed -i "s/^#*Port .*/Port $NEW_PORT/" /etc/ssh/sshd_config
    log "Redémarrage du service SSH"
    systemctl restart sshd
    log "Ouverture du port $NEW_PORT/TCP dans firewalld"
    firewall-cmd --permanent --add-port=$NEW_PORT/tcp > /dev/null
    firewall-cmd --permanent --remove-service=ssh > /dev/null
    firewall-cmd --reload > /dev/null
    log "Ouverture du port $NEW_PORT/TCP dans firewalld..."
else
    log "Le service SSH ne tourne pas sur le port 22/TCP. Port actuel : $SSH_PORT."
fi

if [[ -z "$1" ]]; then
    warn "Aucun nom de machine n'a été fourni en argument."
    exit 1
fi

NEW_HOSTNAME="$1"
CURRENT_HOSTNAME=$(hostnamectl status --static)

if [[ "$CURRENT_HOSTNAME" != "$NEW_HOSTNAME" ]]; then
    warn "La machine s'appelle toujours $CURRENT_HOSTNAME !"
    log "Changement du nom pour $NEW_HOSTNAME..."
    hostnamectl set-hostname "$NEW_HOSTNAME"
else
    log "La machine s'appelle déjà $NEW_HOSTNAME."
fi

USER_NAME="rock-bji"
log "Vérification de l'utilisateur $USER_NAME..."
if ! id -nG "$USER_NAME" | grep -qw "wheel"; then
    warn "L'utilisateur $USER_NAME n'est pas dans le groupe wheel !"
    log "Ajout de l'utilisateur $USER_NAME au groupe wheel..."
    usermod -aG wheel "$USER_NAME"
else
    log "L'utilisateur $USER_NAME est déjà dans le groupe wheel."
fi

log "Le script d'autoconfiguration s'est correctement déroulé."
[rock-bji@vbox ~]$
```
```bash
[rock-bji@vbox ~]$ sudo /opt/autoconfig.sh music.tp3.b1
[sudo] password for rock-bji:
21:39:05 [INFO] Le script d'autoconfiguration a démarré
21:39:05 [INFO] Le script a bien été lancé en root.
21:39:05 [INFO] Vérification de l'état de SELinux...
21:39:05 [INFO] Vérification de l'état du firewall
21:39:05 [INFO] Service de firewalling firewalld est activé.
21:39:05 [INFO] Vérification du port SSH
21:39:05 [INFO] Le service SSH ne tourne pas sur le port 22/TCP. Port actuel : 33672.
21:39:05 [INFO] La machine s'appelle déjà music.tp3.b1.
21:39:05 [INFO] Vérification de l'utilisateur rock-bji...
21:39:05 [INFO] L'utilisateur rock-bji est déjà dans le groupe wheel.
21:39:05 [INFO] Le script d'autoconfiguration s'est correctement déroulé.
[rock-bji@vbox ~]$
```
