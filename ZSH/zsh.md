# Oh My Zsh

### Installation
```bash
sudo apt install zsh
zsh --version
chsh -s $(which zsh)
```
Redémarer l'ordinateur
```bash
echo $SHELL
git clone http://github.com/robbyrussell/oh-my-zsh ~/.oh-my-zsh

mv -b \
~/.oh-my-zsh/templates/zshrc.zsh-template \
~/.zshrc
```

### Thémes
Dans le fichier ```.zshrc``` il faut changer la valeur de la variable ```ZSH_THEME``` par le nom du théme voulue (```agnoster```)

### Pluggins
Dans le fichier ```.zshrc``` il faut rajouter entre les parenthéses le nom des pluggins voulue exemple : 
```bash
plugins=(rails git ruby)
```

Pour plus d'information voir la [documentation](https://github.com/ohmyzsh/ohmyzsh/wiki)
