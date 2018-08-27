# Cas d'utilisation n°2

> Création d'une nouvelle fonctionnalité `FT_0005`, lorsqu'une autre fonctionnalité `FT_0001` est développée en parallèle et partagée sur le dépôt distant en premier.
>
> Il est nécessaire de récupérer les modifications faites par la fonctionnalité `FT_0001` sur la branch `DEV` pour pouvoir valider la demande de fusion associée à `FT_0005`.

![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/UseCase2.png)

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/GitLab.png) Sous GitLab

### ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/MergeS.png) Créer la branche de fonctionnalité
- Aller sur le menu Dépôt
- Cliquer sur Branches
- Cliquer sur le bouton "Nouvelle Branche"
- Nommer la branche de fonctionnalité `7200.0/ft/FT_0005`
- Sélectionner la branche de base `7200.0/dev`

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/GitBash.png) Sous Git Bash

### ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Repo.png) Si on a déjà un dépôt local associé au dépôt distant
Se positionner dans le dossier du dépôt local
```sh
$ git fetch
```

### Sinon, dans un dossier vierge
```sh
$ git clone url_projet
```

### Puis dans tous les cas

```sh
$ git checkout 7200.0/ft/FT_0005
# Développer la fonctionnalité
$ git add [fichiers]
$ git commit -m "FT_0005_description du commit"
$ git rebase -i origin/7200.0/dev
# pick / squash / delete commits + résoudre conflits
$ git rebase --continue (ou --abort)
$ git push
```

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/GitLab.png) Sous GitLab
- Aller sur le menu "Demande de fusion"
- Cliquer sur "New merge request"
- Sélectionner la branche `7200.0/ft/FT_0005` en tant que source
- Sélectionner la branche `7200.0/dev` en tant que cible
- Cliquer sur "Comparer branche et continuer"
- Donner un titre
- Assigner une personne devant valider la merge request
- Cocher la case "Remove source branch when merge request is accepted"
- Cocher la case "Squash commits when merge request is accepted"

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/GitLab.png) Sous GitLab
Le valideur de la merge request confirmera ou refusera la demande de fusion
La fusion ne pourra pas se faire en fast-forward, il faudra alors faire un rebase en local comme indiqué [ici](https://github.com/HIMBER/FormationGit#-faire-un-rebase-pour-conserver-un-historique-propre).

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/GitBash.png) Sous Git Bash

```sh
$ git clone <url_projet> 
$ git checkout -b 7200.0/ft/FT_0005 origin/7200.0/ft/FT_0005 
$ git rebase -i origin/7200.0/dev
# pick / squash / delete commits + résoudre conflits
$ git rebase --continue (ou --abort)
$ git checkout -b 7200.0/dev origin/7200.0/dev 
$ git merge 7200.0/ft/FT_0005 # c’est un fast forward 
$ git push
```

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/GitLab.png) Sous GitLab
La fusion pourra alors se faire en fast-forward et pourra être validée

![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Licence.png) License
----

GNU General Public License v3.0
