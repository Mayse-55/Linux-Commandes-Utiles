# Guide de référence Linux multi-distribution

Documentation complète des commandes essentielles pour l'administration système Linux, compatible Debian, Ubuntu, Fedora, CentOS, RHEL et Arch Linux.

---

## Navigation rapide par distribution

**Cliquez sur votre distribution pour accéder aux commandes spécifiques :**

- [Debian / Ubuntu / Proxmox](#debian--ubuntu--proxmox)
- [Fedora / RHEL / CentOS](#fedora--rhel--centos)
- [Arch Linux / Manjaro](#arch-linux--manjaro)
- [Commandes universelles](#commandes-universelles)

---

## Table des matières

1. [Gestion des paquets](#gestion-des-paquets)
2. [Commandes de base](#commandes-de-base)
3. [Gestion des fichiers](#gestion-des-fichiers)
4. [Recherche et filtrage](#recherche-et-filtrage)
5. [Gestion des disques](#gestion-des-disques)
6. [Configuration réseau](#configuration-réseau)
7. [Gestion des processus](#gestion-des-processus)
8. [Permissions et utilisateurs](#permissions-et-utilisateurs)
9. [Gestion des services](#gestion-des-services)
10. [Surveillance système](#surveillance-système)
11. [Personnalisation du shell](#personnalisation-du-shell)
12. [Commandes avancées](#commandes-avancées)

---

## Gestion des paquets

### Debian / Ubuntu / Proxmox

```bash
# Mise à jour des dépôts
apt update

# Mise à jour du système
apt upgrade
apt full-upgrade

# Installation de paquets
apt install htop nginx
apt install -y vim        # Sans confirmation

# Recherche de paquets
apt search nginx
apt-cache search apache

# Informations sur un paquet
apt show nginx
apt-cache policy docker

# Suppression de paquets
apt remove apache2
apt purge apache2         # Supprime avec les fichiers de config
apt autoremove            # Nettoie les dépendances inutiles

# Gestion des paquets .deb
dpkg -i paquet.deb
dpkg -l                   # Liste tous les paquets installés
dpkg -L nginx             # Liste les fichiers d'un paquet
dpkg -r paquet            # Supprime un paquet
```

### Fedora / RHEL / CentOS

```bash
# DNF (Fedora 22+, RHEL 8+, CentOS 8+)
dnf update
dnf upgrade
dnf install htop nginx
dnf search nginx
dnf info nginx
dnf remove apache2
dnf autoremove
dnf clean all

# YUM (anciennes versions)
yum update
yum install httpd
yum search vim
yum info nginx
yum remove package
yum clean all

# Gestion des paquets .rpm
rpm -ivh paquet.rpm       # Installer
rpm -Uvh paquet.rpm       # Mettre à jour
rpm -qa                   # Liste des paquets installés
rpm -ql nginx             # Liste les fichiers d'un paquet
rpm -e paquet             # Désinstaller
```

### Arch Linux / Manjaro

```bash
# Pacman
pacman -Syu               # Mise à jour complète du système
pacman -S htop nginx      # Installation
pacman -Ss nginx          # Recherche
pacman -Si nginx          # Informations
pacman -R package         # Suppression
pacman -Rs package        # Suppression avec dépendances
pacman -Rns package       # Suppression complète
pacman -Sc                # Nettoyer le cache
pacman -Q                 # Liste des paquets installés
pacman -Ql nginx          # Liste les fichiers d'un paquet

# AUR avec yay (helper)
yay -S package
yay -Syu
```

---

## Commandes de base

### Navigation et manipulation de répertoires

```bash
# Navigation
pwd                       # Affiche le répertoire courant
cd /etc                   # Aller dans /etc
cd ~                      # Aller dans le répertoire personnel
cd -                      # Retour au répertoire précédent
cd ..                     # Remonter d'un niveau
cd ../..                  # Remonter de deux niveaux

# Listage
ls                        # Liste les fichiers
ls -l                     # Format long
ls -a                     # Fichiers cachés inclus
ls -lh                    # Tailles lisibles
ls -lha                   # Combinaison complète
ls -lt                    # Tri par date
ls -lS                    # Tri par taille
ls -lR                    # Récursif

# Création et suppression
mkdir projet              # Créer un répertoire
mkdir -p /a/b/c           # Créer une arborescence
rmdir repertoire          # Supprimer un répertoire vide
rm fichier                # Supprimer un fichier
rm -r repertoire          # Supprimer un répertoire et son contenu
rm -rf repertoire         # Forcer la suppression sans confirmation
rm -i fichier             # Demander confirmation

# Copie et déplacement
cp source destination
cp -r rep1 rep2           # Copie récursive
cp -p fichier copie       # Préserve les attributs
cp -a source dest         # Archive (récursif + préserve tout)
mv source destination     # Déplacer ou renommer
mv fichier.txt new.txt    # Renommer
```

---

## Gestion des fichiers

### Création et lecture

```bash
# Création
touch fichier.txt         # Créer un fichier vide
touch -t 202601151200 f   # Créer avec date spécifique

# Lecture
cat fichier.txt           # Afficher le contenu complet
cat f1 f2 > f3            # Concaténer plusieurs fichiers
less fichier.txt          # Lecture page par page (q pour quitter)
more fichier.txt          # Lecture page par page (ancien)
head fichier.txt          # Afficher les 10 premières lignes
head -n 20 fichier.txt    # Afficher les 20 premières lignes
tail fichier.txt          # Afficher les 10 dernières lignes
tail -n 50 fichier.txt    # Afficher les 50 dernières lignes
tail -f /var/log/syslog   # Suivre un fichier en temps réel
```

### Édition de fichiers

```bash
# Éditeurs de texte
nano fichier.txt          # Éditeur simple
vim fichier.txt           # Éditeur avancé
vi fichier.txt            # Éditeur standard Unix

# Manipulation de contenu
wc fichier.txt            # Compter lignes, mots, caractères
wc -l fichier.txt         # Compter uniquement les lignes
sort fichier.txt          # Trier les lignes
sort -r fichier.txt       # Trier en ordre inverse
uniq fichier.txt          # Supprimer les doublons consécutifs
cut -d: -f1 /etc/passwd   # Extraire des colonnes
```

### Compression et archivage

```bash
# tar
tar -cvf archive.tar dossier/      # Créer une archive
tar -xvf archive.tar               # Extraire une archive
tar -tvf archive.tar               # Lister le contenu
tar -czvf archive.tar.gz dossier/  # Créer et compresser (gzip)
tar -xzvf archive.tar.gz           # Extraire et décompresser
tar -cjvf archive.tar.bz2 dossier/ # Compresser avec bzip2
tar -xjvf archive.tar.bz2          # Décompresser bzip2

# gzip
gzip fichier              # Compresser (remplace le fichier)
gzip -k fichier           # Compresser en gardant l'original
gunzip fichier.gz         # Décompresser
gzip -d fichier.gz        # Décompresser (alternative)

# zip
zip archive.zip fichier1 fichier2
zip -r archive.zip dossier/
unzip archive.zip
unzip -l archive.zip      # Lister le contenu
```

---

## Recherche et filtrage

### Recherche de fichiers

```bash
# find
find /chemin -name "*.txt"              # Recherche par nom
find / -name nginx.conf                 # Recherche depuis la racine
find . -type f                          # Trouver tous les fichiers
find . -type d                          # Trouver tous les répertoires
find . -size +100M                      # Fichiers > 100 Mo
find . -mtime -7                        # Modifiés dans les 7 derniers jours
find . -user root                       # Fichiers appartenant à root
find . -perm 755                        # Fichiers avec permission 755
find . -name "*.log" -delete            # Trouver et supprimer
find . -name "*.txt" -exec chmod 644 {} \;  # Exécuter une commande

# locate (plus rapide mais nécessite updatedb)
locate nginx.conf
locate -i fichier         # Insensible à la casse
updatedb                  # Mettre à jour la base de données
```

### Filtrage et recherche dans le contenu

```bash
# grep
grep "error" fichier.log              # Recherche simple
grep -i "error" fichier.log           # Insensible à la casse
grep -r "TODO" /projet                # Recherche récursive
grep -n "function" script.py          # Affiche les numéros de lignes
grep -v "debug" fichier.log           # Inverse (lignes ne contenant pas)
grep -c "error" fichier.log           # Compte les occurrences
grep -A 3 "error" log                 # Affiche 3 lignes après
grep -B 2 "error" log                 # Affiche 2 lignes avant
grep -C 2 "error" log                 # Affiche 2 lignes avant et après
grep -E "error|warning" log           # Expression régulière étendue
grep -l "pattern" *.txt               # Liste uniquement les fichiers

# Combinaisons avec pipes
cat fichier | grep "error"
ps aux | grep nginx
journalctl | grep -i fail
```

---

## Gestion des disques

### Visualisation

```bash
# Informations sur les disques
lsblk                     # Liste les périphériques de bloc
lsblk -f                  # Avec systèmes de fichiers
blkid                     # UUID et types de systèmes de fichiers
fdisk -l                  # Liste toutes les partitions
parted -l                 # Liste avec parted

# Espace disque
df -h                     # Espace disque lisible
df -i                     # Inodes
du -sh /var               # Taille d'un répertoire
du -h --max-depth=1 /     # Taille des sous-répertoires (1 niveau)
du -ah /var/log | sort -rh | head -20  # 20 plus gros fichiers
```

### Partitionnement

```bash
# fdisk
fdisk /dev/sdb            # Modifier les partitions (MBR)
# Commandes interactives: n (nouvelle), d (supprimer), p (afficher), w (écrire)

# parted
parted /dev/sdb           # Interface interactive (GPT/MBR)
parted /dev/sdb print
parted /dev/sdb mklabel gpt
parted /dev/sdb mkpart primary ext4 0% 100%

# gdisk (GPT)
gdisk /dev/sdb
```

### Systèmes de fichiers

```bash
# Création
mkfs.ext4 /dev/sdb1       # Créer un système de fichiers ext4
mkfs.xfs /dev/sdb1        # XFS
mkfs.btrfs /dev/sdb1      # Btrfs
mkfs.vfat /dev/sdb1       # FAT32

# Vérification et réparation
fsck /dev/sdb1            # Vérifier un système de fichiers
fsck.ext4 /dev/sdb1       # Vérification ext4
e2fsck -f /dev/sdb1       # Forcer la vérification ext4
xfs_repair /dev/sdb1      # Réparation XFS
```

### Montage

```bash
# Montage manuel
mount /dev/sdb1 /mnt/data
mount -t ext4 /dev/sdb1 /mnt/data
mount -o ro /dev/sdb1 /mnt/data       # Lecture seule
umount /mnt/data
umount -l /mnt/data                   # Démontage lazy

# Montage automatique via /etc/fstab
nano /etc/fstab

# Exemples d'entrées fstab:
UUID=xxxx-xxxx  /mnt/data  ext4  defaults  0  2
/dev/sdb1       /backup    xfs   defaults  0  0
//server/share  /mnt/smb   cifs  credentials=/root/.smbcreds  0  0

# Tester le fstab
mount -a                  # Monte tout ce qui est dans fstab
findmnt --verify          # Vérifier la syntaxe de fstab
```

### LVM (Logical Volume Manager)

```bash
# Volumes physiques
pvcreate /dev/sdb1
pvdisplay
pvs

# Groupes de volumes
vgcreate vg_data /dev/sdb1
vgextend vg_data /dev/sdc1
vgdisplay
vgs

# Volumes logiques
lvcreate -L 50G -n lv_storage vg_data
lvcreate -l 100%FREE -n lv_all vg_data
lvdisplay
lvs

# Redimensionnement
lvextend -L +10G /dev/vg_data/lv_storage
lvextend -l +100%FREE /dev/vg_data/lv_storage
resize2fs /dev/vg_data/lv_storage     # Étendre le système de fichiers ext4
xfs_growfs /mnt/storage               # Étendre XFS (doit être monté)
```

---

## Configuration réseau

### Informations réseau

```bash
# Interfaces
ip addr show              # Afficher toutes les interfaces
ip a                      # Version courte
ip link show              # État des interfaces
ifconfig                  # Commande legacy (si installée)

# Routes
ip route show             # Table de routage
ip r                      # Version courte
route -n                  # Commande legacy
ip route get 8.8.8.8      # Route vers une destination

# Connexions
ss -tulnp                 # Sockets en écoute (TCP/UDP)
ss -s                     # Statistiques
netstat -tulnp            # Legacy (si installé)
netstat -rn               # Table de routage

# Tests
ping 8.8.8.8              # Test de connectivité
ping -c 4 google.com      # 4 paquets seulement
traceroute google.com     # Tracer la route
mtr google.com            # Combinaison ping + traceroute
nslookup google.com       # Résolution DNS
dig google.com            # Requête DNS détaillée
host google.com           # Résolution simple
```

### Configuration Debian / Ubuntu

```bash
# Netplan (Ubuntu 18.04+)
nano /etc/netplan/01-netcfg.yaml

# Exemple de configuration:
network:
  version: 2
  ethernets:
    eth0:
      dhcp4: true
    eth1:
      addresses: [192.168.1.100/24]
      gateway4: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]

netplan apply             # Appliquer la configuration
netplan try               # Tester (annule après 120s)

# Interfaces classiques (Debian, anciennes Ubuntu)
nano /etc/network/interfaces

# Exemple:
auto eth0
iface eth0 inet static
  address 192.168.1.100
  netmask 255.255.255.0
  gateway 192.168.1.1
  dns-nameservers 8.8.8.8 1.1.1.1

ifdown eth0 && ifup eth0  # Redémarrer l'interface
systemctl restart networking
```

### Configuration Fedora / RHEL / CentOS

```bash
# NetworkManager (méthode moderne)
nmcli device status
nmcli connection show
nmcli connection up eth0
nmcli connection down eth0

# Configurer une IP statique
nmcli con mod eth0 ipv4.addresses 192.168.1.100/24
nmcli con mod eth0 ipv4.gateway 192.168.1.1
nmcli con mod eth0 ipv4.dns "8.8.8.8 1.1.1.1"
nmcli con mod eth0 ipv4.method manual
nmcli con up eth0

# Fichiers de configuration (anciennes méthodes)
nano /etc/sysconfig/network-scripts/ifcfg-eth0

# Exemple:
DEVICE=eth0
BOOTPROTO=static
ONBOOT=yes
IPADDR=192.168.1.100
NETMASK=255.255.255.0
GATEWAY=192.168.1.1
DNS1=8.8.8.8

systemctl restart NetworkManager
```

### Date et heure

```bash
# Vérifier l'heure actuelle
date
timedatectl
timedatectl status

# Lister les fuseaux horaires
timedatectl list-timezones
timedatectl list-timezones | grep Paris
timedatectl list-timezones | grep Europe

# Configurer le fuseau horaire
timedatectl set-timezone Europe/Paris      # France (UTC+1/+2)
timedatectl set-timezone Europe/Brussels   # Belgique
timedatectl set-timezone Europe/Zurich     # Suisse
timedatectl set-timezone America/New_York  # New York
timedatectl set-timezone Asia/Tokyo        # Tokyo

# Activer la synchronisation NTP automatique
timedatectl set-ntp true

# Désactiver NTP (si besoin de définir manuellement)
timedatectl set-ntp false

# Définir l'heure manuellement
timedatectl set-time "2026-01-29 14:30:00"
timedatectl set-time "14:30:00"            # Seulement l'heure
timedatectl set-time "2026-01-29"          # Seulement la date

# Synchronisation avec systemd-timesyncd
systemctl status systemd-timesyncd
systemctl restart systemd-timesyncd
systemctl enable systemd-timesyncd

# Méthode avec NTP (serveur dédié)
apt install ntp                            # Debian/Ubuntu
dnf install ntp                            # Fedora/RHEL
systemctl start ntp
systemctl enable ntp
ntpq -p                                    # Vérifier les serveurs NTP

# Synchronisation immédiate
apt install ntpdate                        # Si pas installé
ntpdate pool.ntp.org
ntpdate fr.pool.ntp.org
ntpdate time.google.com

# Horloge matérielle (BIOS)
hwclock                                    # Lire l'horloge matérielle
hwclock --systohc                          # Synchroniser système vers matériel
hwclock --hctosys                          # Synchroniser matériel vers système

# Méthode alternative (ancienne)
dpkg-reconfigure tzdata                    # Interface interactive
ln -sf /usr/share/zoneinfo/Europe/Paris /etc/localtime
```

### Pare-feu

```bash
# UFW (Ubuntu)
ufw status
ufw enable
ufw disable
ufw allow 22/tcp
ufw allow 80
ufw allow from 192.168.1.0/24
ufw deny 23
ufw delete allow 80
ufw reset

# Firewalld (Fedora/RHEL/CentOS)
firewall-cmd --state
firewall-cmd --list-all
firewall-cmd --permanent --add-service=http
firewall-cmd --permanent --add-port=8080/tcp
firewall-cmd --reload
firewall-cmd --permanent --remove-service=http

# iptables (méthode legacy)
iptables -L -n -v
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
iptables -A INPUT -s 192.168.1.0/24 -j ACCEPT
iptables -A INPUT -j DROP
iptables-save > /etc/iptables/rules.v4
```

---

## Gestion des processus

### Visualisation

```bash
# Processus en cours
ps aux                    # Tous les processus
ps aux | grep nginx       # Filtrer
ps -ef                    # Format alternatif
ps -u username            # Processus d'un utilisateur
pstree                    # Arbre des processus
pgrep nginx               # PID d'un processus par nom

# Surveillance en temps réel
top                       # Surveillance interactive
htop                      # Version améliorée (si installée)
atop                      # Surveillance avancée

# Commandes dans top/htop:
# M: tri par mémoire
# P: tri par CPU
# k: tuer un processus
# q: quitter
```

### Gestion

```bash
# Signaux
kill PID                  # Envoyer SIGTERM (arrêt propre)
kill -9 PID               # Envoyer SIGKILL (arrêt forcé)
kill -15 PID              # SIGTERM (équivalent à kill)
kill -HUP PID             # SIGHUP (reload config)
killall nginx             # Tuer tous les processus nginx
pkill -f "python script"  # Tuer par pattern

# Priorités
nice -n 10 commande       # Lancer avec priorité basse
renice -n 5 -p PID        # Changer la priorité

# Background / Foreground
commande &                # Lancer en arrière-plan
jobs                      # Liste des jobs
fg %1                     # Ramener job 1 au premier plan
bg %1                     # Reprendre job 1 en arrière-plan
nohup commande &          # Continuer après déconnexion
disown %1                 # Détacher un job du shell

# Screen / Tmux (sessions persistantes)
screen                    # Nouvelle session
screen -S nom             # Session nommée
screen -ls                # Liste des sessions
screen -r                 # Réattacher
# Ctrl+A puis D: détacher

tmux                      # Nouvelle session
tmux ls                   # Liste des sessions
tmux attach               # Réattacher
# Ctrl+B puis D: détacher
```

---

## Permissions et utilisateurs

### Permissions de fichiers

```bash
# Changement de permissions (chmod)
chmod 755 script.sh       # rwxr-xr-x
chmod 644 fichier.txt     # rw-r--r--
chmod 600 secret.key      # rw-------
chmod u+x script.sh       # Ajouter exécution pour user
chmod g-w fichier         # Retirer écriture pour group
chmod o+r fichier         # Ajouter lecture pour others
chmod a+x script          # Ajouter exécution pour all
chmod -R 755 dossier/     # Récursif

# Table complète des permissions numériques
# Calcul : r=4, w=2, x=1 (addition pour combiner)
#
# Propriétaire | Groupe | Autres | Usage typique
# -------------|--------|--------|------------------------------------------
chmod 777      # rwxrwxrwx | Tous les droits (dangereux, à éviter)
chmod 755      # rwxr-xr-x | Scripts, binaires, dossiers publics
chmod 750      # rwxr-x--- | Scripts/dossiers accessibles au groupe uniquement
chmod 700      # rwx------ | Fichiers/dossiers privés de l'utilisateur
chmod 666      # rw-rw-rw- | Fichiers modifiables par tous (rare)
chmod 664      # rw-rw-r-- | Fichiers partagés en groupe
chmod 644      # rw-r--r-- | Fichiers de configuration, documents
chmod 640      # rw-r----- | Logs, fichiers sensibles lisibles par groupe
chmod 600      # rw------- | Clés SSH, mots de passe, fichiers très sensibles
chmod 555      # r-xr-xr-x | Fichiers exécutables en lecture seule
chmod 444      # r--r--r-- | Fichiers en lecture seule pour tous
chmod 400      # r-------- | Fichiers confidentiels en lecture seule
chmod 000      # --------- | Aucun accès (même root peut y accéder)

# Détail du calcul
# r (read)    = 4
# w (write)   = 2
# x (execute) = 1
#
# Exemples de calcul :
# rwx = 4+2+1 = 7
# rw- = 4+2+0 = 6
# r-x = 4+0+1 = 5
# r-- = 4+0+0 = 4
# -wx = 0+2+1 = 3
# -w- = 0+2+0 = 2
# --x = 0+0+1 = 1
# --- = 0+0+0 = 0

# Changement de propriétaire (chown)
chown user fichier
chown user:group fichier
chown -R user:group dossier/
chown :group fichier      # Changer uniquement le groupe
chgrp group fichier       # Alternative pour groupe

# Permissions spéciales
chmod u+s fichier         # SetUID
chmod g+s dossier         # SetGID
chmod +t dossier          # Sticky bit
chmod 4755 fichier        # SetUID + 755
chmod 2755 dossier        # SetGID + 755
chmod 1777 /tmp           # Sticky + 777

# ACL (Access Control Lists)
setfacl -m u:user:rwx fichier
setfacl -m g:group:rx dossier
getfacl fichier
setfacl -b fichier        # Supprimer les ACL
```

### Gestion des utilisateurs

```bash
# Création
useradd username
useradd -m username       # Avec répertoire home
useradd -m -s /bin/bash username
useradd -m -G sudo,docker username

# Modification
usermod -aG sudo username # Ajouter à un groupe
usermod -s /bin/zsh user  # Changer le shell
usermod -L username       # Verrouiller le compte
usermod -U username       # Déverrouiller

# Suppression
userdel username
userdel -r username       # Avec répertoire home

# Mots de passe
passwd username
passwd -l username        # Verrouiller
passwd -u username        # Déverrouiller
passwd -e username        # Forcer le changement au prochain login
chage -l username         # Info sur l'expiration
chage -M 90 username      # Expiration tous les 90 jours

# Groupes
groupadd groupname
groupdel groupname
groups username           # Groupes d'un utilisateur
id username               # UID, GID et groupes
```

### Fichiers importants

```bash
# Utilisateurs et groupes
cat /etc/passwd           # Informations utilisateurs
cat /etc/shadow           # Mots de passe chiffrés (root only)
cat /etc/group            # Informations groupes
cat /etc/gshadow          # Mots de passe de groupes

# Connexions
last                      # Dernières connexions
lastb                     # Tentatives échouées (root only)
w                         # Utilisateurs connectés
who                       # Utilisateurs connectés
whoami                    # Utilisateur courant
id                        # UID et groupes de l'utilisateur courant
```

---

## Gestion des services

### Systemd (distributions modernes)

```bash
# État des services
systemctl status nginx
systemctl is-active nginx
systemctl is-enabled nginx
systemctl list-units --type=service
systemctl list-unit-files --type=service

# Contrôle
systemctl start nginx
systemctl stop nginx
systemctl restart nginx
systemctl reload nginx    # Recharger la config sans arrêter

# Démarrage automatique
systemctl enable nginx    # Activer au boot
systemctl disable nginx   # Désactiver au boot
systemctl enable --now nginx  # Activer et démarrer

# Masquage (empêche tout démarrage)
systemctl mask nginx
systemctl unmask nginx

# Logs
journalctl -u nginx       # Logs d'un service
journalctl -u nginx -f    # Suivre en temps réel
journalctl -u nginx --since today
journalctl -u nginx --since "2026-01-01"
journalctl -xe            # Dernières erreurs système
journalctl --vacuum-time=7d  # Nettoyer les logs > 7 jours
journalctl --disk-usage   # Espace utilisé par les logs

# Cibles (runlevels)
systemctl get-default
systemctl set-default multi-user.target
systemctl isolate rescue.target
systemctl poweroff
systemctl reboot
systemctl suspend
```

### SysVinit / Upstart (anciennes distributions)

```bash
# Debian/Ubuntu ancien
service nginx start
service nginx stop
service nginx restart
service nginx status
/etc/init.d/nginx start

# Activation au démarrage
update-rc.d nginx enable
update-rc.d nginx disable

# RHEL/CentOS 6
service httpd start
chkconfig httpd on
chkconfig --list
```

### Cron (tâches planifiées)

```bash
# Édition
crontab -e                # Éditer pour l'utilisateur courant
crontab -l                # Lister les tâches
crontab -r                # Supprimer toutes les tâches
crontab -u username -e    # Éditer pour un autre utilisateur

# Syntaxe: minute heure jour mois jour_semaine commande
# Exemples:
0 2 * * * /backup.sh              # Tous les jours à 2h00
*/15 * * * * /check.sh            # Toutes les 15 minutes
0 0 * * 0 /weekly.sh              # Tous les dimanches à minuit
0 3 1 * * /monthly.sh             # Le 1er de chaque mois à 3h00

# Fichiers système
nano /etc/crontab
ls /etc/cron.daily/
ls /etc/cron.weekly/
ls /etc/cron.monthly/
```

### Timers systemd (alternative moderne à cron)

```bash
# Lister les timers
systemctl list-timers
systemctl list-timers --all

# Créer un timer
nano /etc/systemd/system/backup.timer
nano /etc/systemd/system/backup.service

# Activer
systemctl enable backup.timer
systemctl start backup.timer
systemctl status backup.timer
```

---

## Surveillance système

### Informations système

```bash
# Système
uname -a                  # Informations kernel
uname -r                  # Version du kernel
hostname                  # Nom de la machine
hostnamectl               # Infos détaillées
uptime                    # Temps depuis le démarrage
date                      # Date et heure

# CPU
lscpu                     # Informations CPU
cat /proc/cpuinfo         # Détails CPU
nproc                     # Nombre de processeurs
```

### Mémoire

```bash
free -h                   # Mémoire libre/utilisée
free -m                   # En mégaoctets
cat /proc/meminfo         # Détails mémoire
vmstat                    # Statistiques mémoire virtuelle
vmstat 2 10               # Toutes les 2s, 10 fois
```

### Disques I/O

```bash
iostat                    # Statistiques I/O
iostat -x 2               # Détaillé, toutes les 2s
iotop                     # Top pour I/O (root)
```

### Réseau

```bash
iftop                     # Surveillance bande passante (root)
nethogs                   # Utilisation réseau par processus
vnstat                    # Statistiques réseau long terme
vnstat -l                 # En direct
```

### Monitoring complet

```bash
# htop (si installé)
htop                      # Interface interactive complète

# glances (si installé)
glances                   # Vue d'ensemble système

# dstat
dstat                     # Statistiques système
dstat -cdngy              # CPU, disque, réseau, système
```

### Logs système

```bash
# Journalctl (systemd)
journalctl                # Tous les logs
journalctl -b             # Depuis le dernier boot
journalctl -k             # Logs kernel
journalctl -p err         # Erreurs uniquement
journalctl --since "1 hour ago"
journalctl -f             # Suivre en temps réel

# Logs traditionnels
tail -f /var/log/syslog   # Debian/Ubuntu
tail -f /var/log/messages # RHEL/CentOS
tail -f /var/log/auth.log # Logs d'authentification
tail -f /var/log/nginx/access.log
tail -f /var/log/nginx/error.log

# Autres
dmesg                     # Messages du kernel
dmesg -T                  # Avec timestamps lisibles
dmesg -w                  # Suivre en temps réel
```

---

## Personnalisation du shell

### Bash

```bash
# Fichiers de configuration
nano ~/.bashrc            # Configuration utilisateur
nano /etc/bash.bashrc     # Configuration système
nano ~/.bash_profile      # Exécuté au login
nano ~/.bash_logout       # Exécuté à la déconnexion

# Recharger la configuration
source ~/.bashrc
. ~/.bashrc               # Alternative

# Alias utiles
alias l='ls -lha --color=auto'
alias ll='ls -lh --color=auto'
alias la='ls -A --color=auto'
alias ..='cd ..'
alias ...='cd ../..'
alias grep='grep --color=auto'
alias df='df -h'
alias du='du -h'
alias free='free -h'
alias update='apt update && apt upgrade'  # Debian/Ubuntu
alias update='dnf update'                 # Fedora

# Couleurs
export LS_OPTIONS='--color=auto'
export CLICOLOR=1
eval "$(dircolors)"

# Prompt personnalisé
export PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '

# Variables d'environnement
export EDITOR=vim
export VISUAL=vim
export PATH=$PATH:/mon/chemin

# Historique
export HISTSIZE=10000
export HISTFILESIZE=20000
export HISTCONTROL=ignoredups:erasedups
export HISTTIMEFORMAT='%F %T '
```

### Zsh (shell alternatif)

```bash
# Installation
apt install zsh          # Debian/Ubuntu
dnf install zsh          # Fedora
pacman -S zsh            # Arch

# Changer de shell
chsh -s /bin/zsh

# Oh My Zsh (framework)
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Configuration
nano ~/.zshrc
```

---

## Commandes avancées

### Redirection et pipes

```bash
# Redirections
commande > fichier        # Redirige stdout (écrase)
commande >> fichier       # Redirige stdout (ajoute)
commande 2> erreurs.log   # Redirige stderr
commande &> fichier       # Redirige stdout et stderr
commande 2>&1             # Redirige stderr vers stdout
commande < fichier        # Utilise fichier comme stdin
commande > /dev/null 2>&1 # Supprimer toute sortie

# Pipes
commande1 | commande2     # Sortie de 1 vers entrée de 2
ps aux | grep nginx | wc -l
cat fichier | sort | uniq | wc -l

# Tee (afficher et sauvegarder)
commande | tee fichier    # Affiche et sauvegarde
commande | tee -a fichier # Ajoute au fichier
```

### Manipulation de texte avancée

```bash
# sed (stream editor)
sed 's/ancien/nouveau/' fichier       # Remplacer (1ère occurrence)
sed 's/ancien/nouveau/g' fichier      # Remplacer (toutes)
sed -i 's/ancien/nouveau/g' fichier   # Modifier le fichier
sed -n '10,20p' fichier               # Afficher lignes 10 à 20
sed '5d' fichier                      # Supprimer ligne 5
sed '/pattern/d' fichier              # Supprimer lignes avec pattern

# awk (traitement de colonnes)
awk '{print $1}' fichier              # Afficher 1ère colonne
awk '{print $1, $3}' fichier          # Colonnes 1 et 3
awk -F: '{print $1}' /etc/passwd      # Délimiteur personnalisé
awk '$3 > 1000' fichier               # Filtrer sur colonne 3
awk '{sum+=$1} END {print sum}' f     # Somme de la colonne 1

# tr (translation de caractères)
echo "MAJUSCULES" | tr '[:upper:]' '[:lower:]'
cat fichier | tr -d '\r'              # Supprimer retours chariot
cat fichier | tr -s ' '               # Compresser les espaces
```

### Synchronisation et sauvegarde

```bash
# rsync (synchronisation)
rsync -av /source/ /destination/
rsync -av --delete /source/ /dest/    # Supprime fichiers en trop
rsync -avz /source/ user@host:/dest/  # Compression réseau
rsync -av --exclude="*.tmp" /src/ /dst/
rsync -av --progress /src/ /dst/      # Avec barre de progression
rsync -av -e ssh /src/ user@host:/dst/

# Exemples pratiques
rsync -av --delete /var/www/ /backup/www/
rsync -avz -e "ssh -p 2222" /data/ user@backup:/data/
```

### Commandes de débogage

```bash
# strace (trace appels système)
strace commande
strace -p PID             # Attacher à un processus
strace -e open,read ls    # Filtrer les appels

# lsof (fichiers ouverts)
lsof                      # Tous les fichiers ouverts
lsof -u user              # Par utilisateur
lsof -p PID               # Par processus
lsof -i :80               # Par port
lsof +D /var/log          # Dans un répertoire

# tcpdump (capture réseau)
tcpdump -i eth0           # Capturer sur eth0
tcpdump -i eth0 port 80
tcpdump -i any -w capture.pcap
tcpdump -r capture.pcap   # Lire une capture
```

### Surveillance continue

```bash
# watch (exécuter périodiquement)
watch -n 1 ls -lha        # Toutes les 1 seconde
watch -d df -h            # Mettre en évidence les différences
watch 'ps aux | grep nginx'

# yes (répéter indéfiniment)
yes | commande            # Répondre automatiquement "y"

# timeout (limiter le temps d'exécution)
timeout 10s commande      # Arrêter après 10 secondes
timeout 5m backup.sh      # Arrêter après 5 minutes
```

### Performance et benchmarks

```bash
# time (mesurer le temps d'exécution)
time commande
time ls -R /

# dd (tests I/O)
dd if=/dev/zero of=test bs=1M count=1000  # Test écriture
dd if=test of=/dev/null bs=1M             # Test lecture
```

### Autres commandes utiles

```bash
# xargs (construire et exécuter des commandes)
find . -name "*.txt" | xargs rm
find . -type f | xargs grep "pattern"
cat liste.txt | xargs -I {} mv {} /destination/

# expect (automatiser les interactions)
# Utile pour les scripts avec mots de passe

# screen / tmux (multiplexeur terminal)
# Déjà couvert dans "Gestion des processus"

# curl / wget (téléchargement)
curl https://example.com
curl -O https://site.com/fichier.tar.gz
wget https://site.com/fichier.tar.gz
wget -c https://site.com/fichier.tar.gz  # Reprendre téléchargement

# nc (netcat - outil réseau)
nc -zv host 80            # Test de port
nc -l -p 8080             # Écouter sur port 8080
```

---

## Commandes universelles

Ces commandes fonctionnent sur toutes les distributions Linux :

```bash
# Navigation
cd, pwd, ls, mkdir, rmdir

# Fichiers
cp, mv, rm, touch, cat, less, more, head, tail

# Recherche
find, grep, locate

# Processus
ps, top, kill, killall, pgrep, pkill

# Réseau
ping, traceroute, dig, host, ip, ss

# Système
uname, hostname, uptime, date, free, df, du

# Utilisateurs
who, w, whoami, id, su, sudo

# Permissions
chmod, chown, chgrp

# Compression
tar, gzip, gunzip, zip, unzip

# Texte
sed, awk, cut, sort, uniq, wc, tr

# Divers
echo, printf, man, which, whereis, type
```

---

## Raccourcis clavier Bash

```bash
# Déplacement
Ctrl + A              # Début de ligne
Ctrl + E              # Fin de ligne
Ctrl + B              # Caractère précédent
Ctrl + F              # Caractère suivant
Alt + B               # Mot précédent
Alt + F               # Mot suivant

# Suppression
Ctrl + D              # Supprimer caractère
Ctrl + H              # Backspace
Ctrl + W              # Supprimer mot précédent
Ctrl + U              # Supprimer jusqu'au début
Ctrl + K              # Supprimer jusqu'à la fin
Alt + D               # Supprimer mot suivant

# Historique
Ctrl + R              # Recherche dans l'historique
Ctrl + P              # Commande précédente
Ctrl + N              # Commande suivante
!!                    # Dernière commande
!$                    # Dernier argument
!*                    # Tous les arguments

# Contrôle
Ctrl + C              # Interrompre
Ctrl + Z              # Suspendre
Ctrl + D              # EOF / déconnexion
Ctrl + L              # Effacer l'écran (clear)
Ctrl + S              # Suspendre affichage
Ctrl + Q              # Reprendre affichage
```

---

## Ressources supplémentaires

### Documentation

```bash
man commande              # Manuel d'une commande
man -k mot-clé            # Rechercher dans les manuels
info commande             # Documentation info
commande --help           # Aide rapide
help commande             # Pour les commandes intégrées bash
```

### Sites web de référence

- Documentation officielle des distributions
- Linux Documentation Project (tldp.org)
- Arch Wiki (très complète, utile pour toutes distributions)
- Stack Exchange / Unix & Linux
- Man pages en ligne

---

## Licence

Cette documentation est sous licence [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/deed.fr).

Vous êtes libre de :
- Partager : copier, distribuer et communiquer le matériel
- Adapter : remixer, transformer et créer à partir du matériel pour toute utilisation, y compris commerciale

Selon les conditions suivantes :
- Attribution : Vous devez créditer l'œuvre, intégrer un lien vers la licence et indiquer si des modifications ont été effectuées

© 2026 Nathaël Polnecq
