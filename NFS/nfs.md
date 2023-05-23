# NFS

### Outils à installer
Sur le serveur : 
```bash
sudo apt install nfs-kernel-server
```
Sur le client :
```bash
sudo apt install nfs-common
```

### Les fichier de configuration
**Serveur**
- exports : permet de définir les répertoires que l’on souhaite rendre accessible au travers d’NFS, ainsi que la liste des IP pouvant monter ces répertoires (et donc accéder aux fichiers). On peut également spécifier des options de montages. 
- hosts.allow : définit la liste des hôtes autorisés à accéder aux services spécifiés. 
- hosts.deny : définit la liste des hôtes explicitement non autorisés à accéder aux services spécifiés.

**Client**
- fstab : permet de définir des règles de montages permanentes pour les espaces de stockage

### Configuration de fstab
Le fichier ```/etc/fstab``` est un fichier qui va monter au démarrage ce qui lui est donné.
Par exemple si on souhaite mount le dossier ```/media/NFS``` on doit rajouter côté client la ligne suivante dans le fichier (en changeant l’ip si besoin) : 
```bash
# 10.0.0.10 -> le serveur
10.0.0.10:/tmp/NFS /media/NFS nfs defaults,bg 0 0 
```
On peut utiliser la commande mount -a pour mount ce qui est présent dans fstab.

### Configuration de exports
Format d’une ligne dans ```/etc/exports``` :
```bash
<dossier partagé> <hôte>(<options>)
```

Explication des options de partage dans ```/etc/exports``` : 
- rw : permet la lecture et l'écriture sur un partage pour l'hôte défini (par défaut, les partages sont en mode ro; c'est-à-dire en lecture seule).
- async : permet au serveur NFS de violer le protocole NFS et de répondre aux requêtes avant que les changements effectués par la requête aient été appliqués sur l'unité de stockage. Cette option améliore les performances mais a un coût au niveau de l'intégrité des données (données corrompues ou perdues) en cas de redémarrage non-propre (par exemple en cas de crash système).
- sync : est le contraire de async. Le serveur NFS respecte le protocole NFS.
- root_squash : force le mapping de l'utilisateur root vers l'utilisateur anonyme (option par défaut).
- no_root_squash : n'effectue pas de mapping pour l'utilisateur root.
- all_squash : force le mapping de tous les utilisateurs vers l'utilisateur anonyme.
- anonuid : indique au serveur NFS l'UID de l'utilisateur anonyme (considéré comme tel dans les précédentes options de mapping).
- anongid : indique au serveur NFS le GID de l'utilisateur anonyme (considéré comme tel dans les précédentes options de mapping).
- subtree_check : Si un sous-répertoire dans un système de fichiers est partagé, mais que le système de fichiers ne l'est pas, alors chaque fois qu'une requête NFS arrive, le serveur doit non seulement vérifier que le fichier accédé est dans le système de fichiers approprié (ce qui est facile), mais aussi qu'il est dans l'arborescence partagée (ce qui est plus compliqué). Cette vérification s'appelle subtree_check.
- no_subtree_check : Cette option neutralise la vérification de sous-répertoires, ce qui a des subtiles implications au niveau de la sécurité, mais peut améliorer la fiabilité dans certains cas.

### Exemple
**Serveur**

Dans le fichier ```/etc/exports``` : 
```
/tmp/NFS 127.0.0.1(rw)
```
Pour start le service cotée serveur : 
```systemctl start nfs-kernel-server.service```

Pour stop le service cotée serveur : 
```systemctl stop nfs-kernel-server.service```

**Client**

Pour mount : 
```bash
sudo mount -t nfs 127.0.0.1:/tmp/NFS /media/NFS
```

Si on a une erreur du type :  ```mount.nfs4: access denied by server while mounting```
- Tester de faire un chmod 777 sur le dossier à partager.
- Ajouter un sync dans /etc/exports si le chmod ne résout pas le problème.

Si le fichier ```/etc/fstab``` est correctement configuré il suffit de taper ```mount -a```

***Avant de stop le serveur ne pas oublier de unmount sur le client***
```bash
sudo umount -t nfs 127.0.0.1:/tmp/NFS /media/NFS
```

### La commande showmount 
Si on tape la commande : 
```bash
showmount -e
```
On obtient la liste des informations des mount pour les serveurs NFS connectés au réseau.

Si on tape la commande : 
```bash
showmount -e 127.0.0.1
```
On obtient les informations des mount pour le serveur NFS 127.0.0.1.

### La commande exportfs

Si on tape la commande cotée serveur on obtient la liste des fichier NFS exporter : 
```bash
sudo exportfs
```

Résultat de la commande : 
```
/tmp/NFS     <IP_client>
```
