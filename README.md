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
ssh-add ~/.ssh/id_rsa
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
# Log des commits locaux et distants au format résumé et graphique
$ git config --global alias.lg "log --graph --oneline --decorate"

# Log des commits locaux uniquement au format résumé et graphique
$ git config --global alias.llg "log --oneline --graph --branches --not --remotes"

# Commit avec message
$ git config --global alias.cm "commit -m"

# Affichage du statut
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
$ git merge <source branch> --squash # c’est un fast forward 
$ git commit -m "descriptif du commit de synthèse"
$ git push
```

- La **branche source** est celle dont les commits vont être rejoués (ex : `branche de fonctionnalité`)
- La **branche cible** est celle dont le dernier commit va servir de nouveau parent à la branche source (ex : `branche de développement`)

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Back.png) Revenir en arrière sur une opération de fusion

Ceci permet d'annuler la dernière opération de type
- rebase
- merge
- pull avec rebase ou merge

sans avoir à retrouver le SHA1 du commit

#### Sous Git Bash :

```sh
git reset --merge ORIG_HEAD
```

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Back.png) Annuler une résolution de conflit de fichier

#### Sous Git Bash :

```sh
git checkout -m FILE
```

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Merge.png) Configurer l'affichage par défaut lors d'un conflit de fusion

#### Sous Git Bash :

```sh
git config --global merge.conflictstyle merge
```

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Merge.png) Configurer l'affichage de l'ancêtre commun à deux branches lors d'un conflit de fusion

#### Sous Git Bash :

```sh
git config --global merge.conflictstyle diff3
```

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Merge.png) Afficher le commit représentant l'ancêtre commun à deux branches 

#### Sous Git Bash :

```sh
git checkout ma_branche
git log -1 $(git merge-base --fork-point autre_branche)
```

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Merge.png) Afficher les fichiers modifiés dans les différents commits 

#### Sous Git Bash :

```sh
git whatchanged
```

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Back.png) Changer l'auteur de tous les commits sans modifier la date

#### Sous Git Bash :

```sh
git filter-branch -f --env-filter "
    GIT_AUTHOR_NAME='Newname'
    GIT_AUTHOR_EMAIL='new@email'
    GIT_COMMITTER_NAME='Newname'
    GIT_COMMITTER_EMAIL='new@email'
  " HEAD
```
## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Merge.png) Utiliser l'autosquash et le fixup

Ceci permet d'amender simplement un commit de l'historique local avec un nouveau commit via la commande de `rebase` interactif. Le message de commit n'est pas obligatoire. Celui du commit amendé sera repris par défaut, préfixé par "fixup!"

#### Sous Git Bash :

```sh
git commit --fixup=SHA1duCommitAvecQuiFusionner
git rebase -i origin/BRANCHE_COURANTE --autosquash
```

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Merge.png) Configurer l'autosquash par défaut

Cette option sera utilisée uniquement lors d'un rebase interactif et prendra en compte les commits typés `fixup`. Il n'y aura plus besoin de saisir le paramètre `--autosquash` dans la commande de `rebase` interactif

#### Sous Git Bash :

```sh
git config --global rebase.autosquash true
```

![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Licence.png) License
----

GNU General Public License v3.0
