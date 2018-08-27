# Cas d'utilisation n°3

> Le Front Office fourni une nouvelle release de l'application.
>
> Il faut alors la prendre en compte dans les développements en cours.

![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/UseCase3.png)

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/GitLab.png) Sous GitLab

### ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/MergeS.png) Si elle n'existe pas déjà, créer la branche de release du Front Office
- Aller sur le menu Dépôt
- Cliquer sur Branches
- Cliquer sur le bouton "Nouvelle Branche"
- Nommer la branche `7200.0/fo.rel`
- Sélectionner la branche de base `master`

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Jenkins.png) Sous Jenkins
- Exécuter le job de récupération de la nouvelle release
- Un nouveau commit est fait dans la branche `7200.0/fo.rel`

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/GitLab.png) Sous GitLab

### ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Fusion.png) Demander la fusion de cette release du Front Office vers la branche de release
- Aller sur le menu "Demande de fusion"
- Cliquer sur "New merge request"
- Sélectionner la branche `7200.0/fo.rel` en tant que source
- Sélectionner la branche `7200.0/rel` en tant que cible
- Cliquer sur "Comparer branche et continuer"
- Donner un titre
- Assigner une personne devant valider la merge request

### ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Fusion.png) Demander la fusion de cette release du Front Office vers la branche de développement
- Aller sur le menu "Demande de fusion"
- Cliquer sur "New merge request"
- Sélectionner la branche `7200.0/fo.rel` en tant que source
- Sélectionner la branche `7200.0/dev` en tant que cible
- Cliquer sur "Comparer branche et continuer"
- Donner un titre
- Assigner une personne devant valider la merge request

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/GitLab.png) Sous GitLab
La fusion vers les branches de release et de développement devra se faire en **fast-forward** pour être validée, sinon il faudra faire un **rebase** en local en suivant la manipulation indiquée [ici](https://github.com/HIMBER/FormationGit/tree/master/UseCases/Cas02#-sous-git-bash-1)

**Si un développement de fonctionnalité est en cours (ex : `FT_0008`), il faudra prévenir les développeurs pour qu'ils récupèrent en local cette nouvelle version (ex : `DEV`) et rebasent leurs développements dessus :**
## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/GitBash.png) Sous Git Bash
```sh
$ git checkout 7200.0/ft/FT_0008
$ git fetch
$ git rebase -i origin/7200.0/dev
# pick / squash / delete commits + résoudre conflits
$ git rebase --continue (ou --abort)
```

![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Licence.png) License
----

GNU General Public License v3.0
