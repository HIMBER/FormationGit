# Formation à Git

![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/git.jpg)

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

#### Sous Git Bash :

```sh
$ git mergetool
```

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Compte.png) Configurer son compte

#### Sous Git Bash :

```sh
$ git config --global user.name "Prénom NOM"
$ git config --global user.email "prénom.nom@masociété.com"
```

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Https.png) Désactiver les erreurs de certificat HTTPs

#### Sous Git Bash :

```sh
$ git config --global http.sslVerify false
```

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Alias.png) Créer quelques alias utiles

#### Sous Git Bash :

```sh
$ git config --global alias.lg log --graph --oneline --decorate
$ git config --global alias.cm commit -m
$ git config --global alias.st status
```

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Alias.png) Utiliser ces alias

#### Sous Git Bash :

```sh
$ git lg
$ git cm "mon message de description de commit"
$ git st
```

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Merge.png) Configurer l'utilisation de l'option rebase lors de l'appel à pull

#### Sous Git Bash :

```sh
git config --global pull.rebase preserve
```

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Merge.png) Faire un rebase pour conserver un historique propre

Par exemple, pour fusionner la `branche de développement` avec une `branche de fonctionnalité`

#### Sous Windows :

Sur son poste local, créer un sous-dossier pour héberger les sources

#### Sous Git Bash :

```sh
$ git clone <url_projet> 
$ git checkout -b <source_branch> origin/<source_branch> 
$ git rebase -i origin/<target_branch>
# pick / squash / delete commits + résoudre conflits
$ git rebase --continue (ou --abort)
$ git checkout -b <target_branch> origin/<target_branch> 
$ git merge <source branch> # c’est un fast forward 
$ git push
```

- La **branche source** est celle dont les commits vont être rejoués (ex : `branche de fonctionnalité`)
- La **branche cible** est celle dont le dernier commit va servir de nouveau parent à la branche source (ex : `branche de développement`)

![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Licence.png) License
----

GNU General Public License v3.0
