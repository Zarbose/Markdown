# Git
Page de [Documentation](https://git-scm.com/doc)

### Identité
```bash
git config --global user.name "Simon Pieto"
git config --global user.email "simonpieto.pieto@gmail.com"
```

### Créarion d'un nouveaux repository
```bash
echo "# Titre" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:Zarbose/<nom-repertoire>.git
git push -u origin main
```

### Push un repository déjà existant
```bash
git remote add origin git@github.com:Zarbose/<nom-repertoire>.git
git branch -M main
git push -u origin main
```

### Commandes de base
#### Git inti
Cette commande est utilisée pour créer un nouveau dépôt GIT.
```bash
git init
```

#### Git add
La commande git add peut être utilisée pour ajouter des fichiers à l’index. Par exemple, la commande suivante ajoutera un fichier nommé temp.txt dans le répertoire local de l’index: 
```bash
git add temp.txt
```

#### Git clone
La commande git clone est utilisée pour clonner un dépot :
```bash
git clone alex@93.188.160.58:/chemin/vers/dépôt
```

#### Git commit
La commande git commit permet de valider les modifications apportées au HEAD. Notez que tout commit ne se fera pas dans le dépôt distant. 
```bash
git commit –m “Description du commit”
```

#### Git status
La commande git status affiche la liste des fichiers modifiés ainsi que les fichiers qui doivent encore être ajoutés ou validés. Usage: 
```bash
git status
```

#### Git push
Git push est une autre commandes GIT de base. Un simple push envoie les modifications locales apportées à la branche principale associée : 
```bash
git push origin master
```

#### Git checkout
La commande git checkout peut être utilisée pour créer des branches ou pour basculer entre elles. Par exemple nous allons créer une branche: 
```bash
git checkout -b <nom-branche>
```
Pour passer simplement d’une branche à une autre, utilisez: 
```bash
git checkout <nom-branche>
```

#### Git remote
Cette commande permet à l’utilisateur de connecter le dépôt local à un serveur distant:
```bash
git remote add origin git@github.com:Zarbose/Info_cmd.git
```

#### Branche git
La commande git branch peut être utilisée pour répertorier, créer ou supprimer des branches. Pour répertorier toutes les branches présentes dans le dépôt, utilisez: 
```bash
git branch
```
Pour supprimer une branche: 
```bash
git branch –d <nom-branche>
```

#### Git pull
Pour fusionner toutes les modifications présentes sur le dépôt distant dans le répertoire de travail local, la commande pull est utilisée. Usage: 
```bash
git pull
```

#### Git merge
La commande git merge est utilisée pour fusionner une branche dans la branche active. Usage: 
```bash
git merge <nom-branche>
```

#### Git diff
La commande git diff permet de lister les conflits. Pour visualiser les conflits d’un fichier, utilisez 
```bash
git diff --base <nom-fichier>
```
La commande suivante est utilisée pour afficher les conflits entre les branches à fusionner avant de les fusionner: 
```bash
git diff <branche-source> <branche-cible>
```
Pour simplement énumérer tous les conflits actuels, utilisez: 
```bash
git diff
```

#### Git tag
Le marquage est utilisé pour marquer des commits spécifiques avec des poignées simples. Un exemple peut être:
```bash
git tag 1.1.0 <insert-commitID-here>
```

#### Git log
L’ exécution de cette commande génère le log d’une branche. Un exemple de sortie : 
```bash
commit 15f4b6c44b3c8344caasdac9e4be13246e21sadw 
Author: Alex Hunter <alexh@gmail.com> 
Date: Mon Oct 1 12:56:29 2016 -0600
```

#### Git reset
Pour réinitialiser l’index et le répertoire de travail à l’état du dernier commit, la commande git reset est utilisée : 
```bash
git reset --hard HEAD
```

#### Git rm
Git rm peut être utilisé pour supprimer des fichiers de l’index et du répertoire de travail. Usage: 
```bash
git rm nomfichier.txt
```

#### Git stash
L’une des moins connues, git stash aide à enregistrer les changements qui ne doivent pas être commit immédiatement. C’est un commit temporaire. Usage:
```bash
git stash
``` 

#### Git show
Pour afficher des informations sur tout fichier git, utilisez la commande git show . Par exemple: 
```bash
git show
``` 

#### Git fetch
Git fetch permet à un utilisateur d’extraire tous les fichiers du dépôt distant qui ne sont pas actuellement dans le répertoire de travail local. Exemple d’utilisation: 
```bash
git fetch origin
``` 

#### Git gc
Pour optimiser le dépôt en supprimant les fichiers inutiles et les optimiser, utilisez:
```bash
git gc
``` 

#### Git archive
La commande git archive permet à un utilisateur de créer un fichier zip ou tar contenant les composants d’un arbre du dépôt. Par exemple: 
```bash
git archive --format=tar master
``` 

#### Git rebase
La commande git rebase est utilisée pour la réapplication des commits sur une autre branche. Par exemple: 
```bash
git rebase master
``` 

### Alias
```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
```
