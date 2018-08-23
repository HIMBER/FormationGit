# Formation à Git

![logo git](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/git.jpg)

Ce dépôt contient quelques ressources pour configurer son environnement de travail

## Création d'une nouvelle clé SSH compatible avec GitLab

### Lancer GitBash et saisir cette commande

```sh
$ ssh-keygen -t rsa -C "monadressemail@masociété.com" -b 4096
```

Saisir ou non un mot de passe (il faudra alors le saisir à chaque ouverture de Git Bash s'il est défini)

### Afficher le contenu de la clé publique

```sh
$ cat ~/.ssh/id_rsa.pub
```

Copier cette clé vers le presse papier

### Associer cette clé publique avec le dépôt GitLab

- Aller sur GitLab
- Menu Settings
- Onglet SSH Keys
- Coller la clé dans le champ prévu à cet effet
- Donner un titre clair à cette clé
- Cliquer sur Add Key pour valider

## Utilisation de cette clé dans les nouvelles sessions Git Bash

### Editer (ou créer) le fichier %userprofile%/.bashrc

```sh
#!/bin/bash
eval `ssh-agent -s`
ssh-add
```

## Configurer WinMerge en tant qu'outil de fusion par défaut

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
License
----

GNU General Public License v3.0
