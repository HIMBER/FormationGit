# Cas d'utilisation n°4

> Livraison d'une nouvelle version vers le Front Office avec une demande de lock

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/GitLab.png) Sous GitLab

### ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/MergeS.png) Si elle n'existe pas déjà, créer la branche de lock du Front Office
- Aller sur le menu Dépôt
- Cliquer sur Branches
- Cliquer sur le bouton "Nouvelle Branche"
- Nommer la branche `7200.0/fo.lock/01`
- Sélectionner la branche de base `7200.0/rel`

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Jenkins.png) Sous Jenkins
- Exécuter le job de récupération des fichiers lockés
- Un nouveau commit est fait dans la branche `7200.0/fo.lock/01`

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/GitLab.png) Sous GitLab

### ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Fusion.png) Demander la fusion de la branche de développement vers la branche de release
- Aller sur le menu "Demande de fusion"
- Cliquer sur "New merge request"
- Sélectionner la branche `7200.0/dev` en tant que source
- Sélectionner la branche `7200.0/rel` en tant que cible
- Cliquer sur "Comparer branche et continuer"
- Donner un titre
- Assigner une personne devant valider la merge request

### ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Fusion.png) Valider la demande de fusion
Le responsable valide la fusion vers la branche de release lorsque tout est OK

### ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/MergeS.png) Créer la branche de livraison
- Aller sur le menu Dépôt
- Cliquer sur Branches
- Cliquer sur le bouton "Nouvelle Branche"
- Nommer la branche `7200.0/liv/01`
- Sélectionner la branche de base `7200.0/rel`

### ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Fusion.png) Demander la fusion la branche de lock vers la branche de livraison
- Aller sur le menu "Demande de fusion"
- Cliquer sur "New merge request"
- Sélectionner la branche `7200.0/fo.lock/01` en tant que source
- Sélectionner la branche `7200.0/liv/01` en tant que cible
- Cliquer sur "Comparer branche et continuer"
- Donner un titre
- Assigner une personne devant valider la merge request

### ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Fusion.png) Valider la demande de fusion
Le responsable valide la fusion vers la branche de livraison lorsque tout est OK
Il peut ainsi lister les fichiers réellement modifiés et les conflits de fusion s'il y en a

## ![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/GitBash.png) Sous Git Bash
```sh
$ git fetch
$ git checkout 7200.0/liv/01
$ git merge
```

Les fichiers fusionnés sont disponibles dans le dossier de travail et prêts à être envoyés au Front Office

![](https://github.com/HIMBER/FormationGit/blob/master/Private/Images/Licence.png) License
----

GNU General Public License v3.0
