# Formation à Git

![logo git](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/git.jpg)

Ce dépôt contient quelques ressources pour configurer son environnement de travail

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/GitBash.png) Installer Git Bash
- Télécharger l'installeur depuis https://gitforwindows.org/
- Exécuter cet installeur sur son poste
 
## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/GitBash.png) Ouvrir Git Bash dans un dossier
Un menu contextuel sera à présent disponible dans l'explorateur Windows :
- Git Bash Here
- Git GUI Here

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/SSH.png) Création d'une nouvelle clé SSH compatible avec GitLab

### Lancer Git Bash et saisir cette commande

```sh
$ ssh-keygen -t rsa -C "monadressemail@masociété.com" -b 4096
```

Saisir ou non un mot de passe (il faudra alors le saisir à chaque ouverture de Git Bash s'il est défini)

### Afficher le contenu de la clé publique

```sh
$ cat ~/.ssh/id_rsa.pub
```

Copier cette clé vers le presse papier

### ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/GitLab.png) Associer cette clé publique avec le dépôt GitLab

- Aller sur GitLab
- Menu Settings
- Onglet SSH Keys
- Coller la clé dans le champ prévu à cet effet
- Donner un titre clair à cette clé
- Cliquer sur Add Key pour valider

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/GitBash.png) Utilisation de cette clé dans les nouvelles sessions Git Bash

### Editer (ou créer) le fichier %userprofile%/.bashrc

```sh
#!/bin/bash
eval `ssh-agent -s`
ssh-add ~/.ssh/id_rsa.pub
```

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/WinMerge.png) Configurer WinMerge en tant qu'outil de fusion par défaut

### Télécharger WinMerge depuis http://winmerge.org/downloads/?lang=fr

L'installer dans le dossier par défaut (sinon il faudra adapter le chemin dans le code ci dessous)

### Editer le fichier ~/.gitconfig

Coller cette configuration

```sh
[mergetool]
    prompt = false
    keepBackup = false
    keepTemporaries = false

[merge]
    tool = winmerge

[mergetool "winmerge"]
    name = WinMerge
    trustExitCode = true
    cmd = "/c/Program\\ Files\\ \\(x86\\)/WinMerge/WinMergeU.exe" -u -e -dl \"Local\" -dr \"Remote\" $LOCAL $REMOTE $MERGED

[diff]
    tool = winmerge

[difftool "winmerge"]
    name = WinMerge
    trustExitCode = true
    cmd = "/c/Program\\ Files\\ \\(x86\\)/WinMerge/WinMergeU.exe" -u -e $LOCAL $REMOTE
```

### Utiliser WinMerge pour résoudre un conflit de fusion

Sous Git Bash :

```sh
$ git mergetool
```

## Créer quelques alias utiles

Sous Git Bash :

```sh
$ git config --global alias.lg log --graph --oneline --decorate
$ git config --global alias.cm commit -m
$ git config --global alias.st status
```

License
----

GNU General Public License v3.0
