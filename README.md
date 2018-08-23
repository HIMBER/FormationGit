# Formation � Git

![logo git](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/git.jpg)

Ce d�p�t contient quelques ressources pour configurer son environnement de travail

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/GitBash.png) Installer Git Bash
- T�l�charger l'installeur depuis https://gitforwindows.org/
- Ex�cuter cet installeur sur son poste
 
## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/GitBash.png) Ouvrir Git Bash dans un dossier
Un menu contextuel sera � pr�sent disponible dans l'explorateur Windows :
- Git Bash Here
- Git GUI Here

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/SSH.png) Cr�ation d'une nouvelle cl� SSH compatible avec GitLab

### Lancer Git Bash et saisir cette commande

```sh
$ ssh-keygen -t rsa -C "monadressemail@masoci�t�.com" -b 4096
```

Saisir ou non un mot de passe (il faudra alors le saisir � chaque ouverture de Git Bash s'il est d�fini)

### Afficher le contenu de la cl� publique

```sh
$ cat ~/.ssh/id_rsa.pub
```

Copier cette cl� vers le presse papier

### ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/GitLab.png) Associer cette cl� publique avec le d�p�t GitLab

- Aller sur GitLab
- Menu Settings
- Onglet SSH Keys
- Coller la cl� dans le champ pr�vu � cet effet
- Donner un titre clair � cette cl�
- Cliquer sur Add Key pour valider

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/GitBash.png) Utilisation de cette cl� dans les nouvelles sessions Git Bash

### Editer (ou cr�er) le fichier %userprofile%/.bashrc

```sh
#!/bin/bash
eval `ssh-agent -s`
ssh-add ~/.ssh/id_rsa.pub
```

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/WinMerge.png) Configurer WinMerge en tant qu'outil de fusion par d�faut

### T�l�charger WinMerge depuis http://winmerge.org/downloads/?lang=fr

L'installer dans le dossier par d�faut (sinon il faudra adapter le chemin dans le code ci dessous)

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

### Utiliser WinMerge pour r�soudre un conflit de fusion

Sous Git Bash :

```sh
$ git mergetool
```

## Cr�er quelques alias utiles

Sous Git Bash :

```sh
$ git config --global alias.lg log --graph --oneline --decorate
$ git config --global alias.cm commit -m
$ git config --global alias.st status
```

License
----

GNU General Public License v3.0
