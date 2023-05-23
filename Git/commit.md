# Git

### Bien nommer ses commits

#### Format du commit
```
<type>(<portée>): <sujet>

<description>

<footer>
```

#### Type du commit

- ```build``` : changements qui affectent le système de build ou des dépendances externes (npm, make…)
- ```ci``` : changements concernant les fichiers et scripts d’intégration ou de configuration (Travis, Ansible, BrowserStack…)
- ```feat``` : ajout d’une nouvelle fonctionnalité
- ```fix``` : correction d’un bug
- ```perf``` : amélioration des performances
- ```refactor``` : modification qui n’apporte ni nouvelle fonctionalité ni d’amélioration de performances
- ```style``` : changement qui n’apporte aucune alteration fonctionnelle ou sémantique (indentation, mise en forme, ajout d’espace, renommante d’une variable…)
- ```docs``` : rédaction ou mise à jour de documentation
- ```test``` : ajout ou modification de tests

À cela s’ajoute ```revert```. Ce dernier permet comme son nom l’indique, d’annuler un précédent commit. Dans ce cas, le message prend la forme suivante :
```
revert sujet du commit annulé hash du commit annulé
```

#### Exemple
```bash
feat(ci): add ci to build and push on amd64 and arm64 
```

