# Linux – Commandes utiles

---

## Personnalisation du shell (couleurs, alias, raccourcis)

Tu peux modifier ton environnement avec :

```bash
nano /root/.bashrc
```

Exemples d’alias pratiques :

```bash
alias l='ls -lha --color=auto'
alias ll='ls -lh --color=auto'
alias la='ls -A --color=auto'
```

Active la couleur automatique :

```bash
export LS_OPTIONS='--color=auto'
export CLICOLOR=1
eval "$(dircolors)"
```

Recharge sans redémarrer :

```bash
source /root/.bashrc
```

---

## Commandes de base

```bash
pwd          # Affiche le dossier courant
ls           # Liste les fichiers
l            # (alias) ls -lha
cd /etc      # Aller dans /etc
cd ..        # Revenir en arrière
mkdir test   # Créer un dossier
rm fichier   # Supprimer un fichier
rm -r test   # Supprimer un dossier
cp a b       # Copier
mv a b       # Déplacer / renommer
```

---

## Gestion des fichiers

```bash
touch file.txt       # Créer un fichier
cat file.txt         # Lire un fichier
less file.txt        # Lire page par page
head file.txt        # Début du fichier
tail -f log.txt      # Suivre un log en direct
```

---

## Recherche

```bash
find / -name test.txt
locate nginx.conf
grep "erreur" /var/log/syslog
```

---

## Gestion des paquets (Debian/Proxmox)

```bash
apt update
apt upgrade
apt install htop
apt remove apache2
```

---

## Disques & montages

```bash
lsblk
blkid
mount /dev/sdb1 /mnt/data
umount /mnt/data
mount -a
```

---

## /etc/fstab

Éditer fstab :

```bash
nano /etc/fstab
```

Exemple :

```bash
UUID=xxxx-xxxx  /mnt/data  ext4  defaults  0  2
```

Tester :

```bash
mount -a
```

---

## Réseau

```bash
ip a
ip r
ping 8.8.8.8
ss -tulnp
```

---

## Processus

```bash
top
htop
ps aux
kill 1234
```

---

## Permissions

```bash
chmod 755 script.sh
chown user:user file.txt
```

---

## Services (systemd)

```bash
systemctl status ssh
systemctl restart nginx
systemctl enable lsyncd
systemctl disable apache2
```

---

## Avancé

```bash
journalctl -xe
strace -p 1234
rsync -av --delete /src/ /dst/
watch -n 1 ls -lha
```
---

## Licence

Cette documentation est sous licence [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/deed.fr).

Vous êtes libre de :
- Partager — copier, distribuer et communiquer le matériel
- Adapter — remixer, transformer et créer à partir du matériel pour toute utilisation, y compris commerciale

Selon les conditions suivantes :
- Attribution — Vous devez créditer l'œuvre, intégrer un lien vers la licence et indiquer si des modifications ont été effectuées.

© 2026 Nathaël Polnecq
