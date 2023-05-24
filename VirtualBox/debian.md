# Debian

### Redirection des ports
```bash
sudo apt-get install openssh-server
sudo service ssh status # Tester le service ssh
hostname -I # Obtenire son ip
```
Plus d'info sur :
- *<https://medium.com/platform-engineer/port-forwarding-for-ssh-http-on-virtualbox-459277a888be> (23.05.2023)*

Définir la connexion en mode ```pont permet``` de ne pas avoir a rediriger les ports.


### SSH
```bash
ssh-keygen # Génération de la clé
type $env:USERPROFILE\.ssh\id_rsa.pub | ssh <ip-destination> "cat >> .ssh/authorized_keys" # Copie de la clé depuis windows
ssh-copy-id -i ~/.ssh/mykey user@host # Copie de la clé depuis linux
ssh -i ~/.ssh/mykey user@host # Test de la clé
```

### Connexion
```bash
ssh -p 2200 "nom de lutilisateur sur la vm"@localhost
ssh -p 2200 simon@localhost
```
Si il y a un pb de type ```REMOTE HOST IDENTIFICATION HAS CHANGED``` taper la cmd suivante 
```bash
ssh-keygen -R [localhost]:2200 # Windows
```

### Montage d'un volume
Voicie quelque exemples :
```bash
mkdir /home/simon/partage # sur la vm
sudo mount -t vboxsf vm /home/simon/partage
sudo mount -t vboxsf XML /home/simon/partage
sudo mount -t vboxsf crypto /home/simon/partage
```

### Guest Aditions
```bash
su -
apt-get install linux-headers-$(uname -r)
apt-get install build-essential
```
Sur le menu de VirtualBox sélectionner Devices -> Insert Guest Aditions CD Image
```bash
su -
cd /media/cdrom
sh VBoxLinuxAdditions.run
/sbin/reboot
```

### Installer sudo
```bash
su -
apt-get install sudo -y
usermod -aG sudo mon_user
```

### Configuration final
```bash
sudo apt install tree
sudo apt install tldr
tldr -u
```
Les alias : 
```bash
touch .bash_aliases
nano .bash_aliases
alias ll='ls -alh'
alias cl='clear'
source .bashrc
```
