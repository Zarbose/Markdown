# Git

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
git remote add origin git@github.com:Zarbose/<A changer>.git
git push -u origin main
```

### Push un repository déjà existant
```bash
git remote add origin git@github.com:Zarbose/<A changer>.git
git branch -M main
git push -u origin main
```

### Alias
```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
```
