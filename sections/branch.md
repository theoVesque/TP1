# Gestion des branches

## Explication

La force de *Git* vient de l'utilisation des branches. Les branches sont au coeur du système *Git*. Il est d'ailleurs recommandé en travaillant sous cet outil de créer des branches.

Une branche est une référence pointant sur un commit. Les branches trouvent leur utilité dans le fait qu'on peut isoler un travail (donc un ensemble de commits) en cours sans polluer la branche principale commune à tous les contributeurs.

A l'initialisation d'un dépôt (`init` ou `clone`), vous êtes automatiquement positionné sur la branche `master` (dans la première partie du TP, l'intégralité des manipulations réalisées se sont faites sur `master`).

Lorsque votre `HEAD` (c'est-à-dire, votre position dans l'historique) pointe sur l'étiquette d'une branche et que vous faites un commit :

1. le *commit* est créé,
2. le *commit* prend en tant que parent le *commit* pointé par la branche,
3. la branche se positionne sur le *commit* nouvellement créé (facilement vérifiable avec un `git log`).

C'est ce qui s'est passé tout à l'heure lorsque que vous avez créé votre premier commit sur `master`.

Grâce aux branches, on peut obtenir plusieurs historiques différents pour un même projet, et donc de travailler en parallèle sur une certaine version, que ce soit seul ou en équipe (comme nous le verrons plus tard). Et vu que *Git* est un *DVCS*, tous les commits que vous créerez sur ces branches seront locaux, jusqu'à ce que vos branches soient poussées.

## Utilisation des branches

Grâce au dépôt `git-init` que vous avez cloné en début de TP, nous allons manipuler les branches et utiliser les commandes associées.

> **Manipulation** : Pour connaître vos branches locales sur un projet, exécutez la commande :
>
> ```bash
> $ git branch
>```
> Vous devriez n'avoir que la branche `master`. Créez une branche à l'aide de la commande suivante :
>
> ```bash
> $ git branch creation-branches
> ```
>
> En listant à nouveau les branches locales, vous devriez cette fois-ci avoir deux branches : `master` et `creation-branches`.
>
> Pour se mettre à travailler sur cette branche, exécutez la commande :
>
> ```bash
> $ git checkout creation-branches
> ```
>
> Cette commande sert à positionner votre `HEAD` sur la référence de la branche `creation-branches`. Faites un ou deux commits sur cette branche et affichez l'historique. Vous constaterez que la branche `master` n'a pas bougé (ces fichiers n'ont pas changé), par contre, la `creation-branches` a intégré vos commits nouvellement créés. 
>
> **Vous avez isolé votre travail de la branche `master`**.

Dans l'optique d'une branche de travail temporaire (juste pour réaliser un travail spécifique), vous serez amené à fusionner les commits de votre branche avec la branche principale (ou tout autre branche). Cela permet d'appliquer les modifications d'une branche vers une autre.

> **Manipulation** : Au vu des manipulations réalisées précédemment, vous devez vous trouver sur votre branche `creation-branches` avec un ou plusieurs commits liés uniquement à cette branche.
>
> **Nous allons fusionner nos branches**.
>
> Repositionnez-vous sur la branche `master`, et exécutez la commande :
>
> ```bash
> $ git merge creation-branches
> ```
>
> Cette commande ramène les changements de la branche `creation-branches` sur la branche où vous vous trouvez (donc `master`).
>
> La fusion que vous venez de faire est censé s'etre bien passée. Les modifications que vous avez fait sur votre branche `creation-branches` ont été appliquées sur `master`. Si vous affichez l'historique du dépôt, vous verrez que `master` s'est mise à jour avec les nouveaux commits.
>
> **Avertissement** : Néanmoins, tout ne se passe pas toujours aussi simplement lors d'une fusion de branches. Des conflits peuvent survenir lorsqu'on fusionne deux branches divergentes (et c'est normal). Cela passe par une phase de **résolution de conflits**. La résolution d'un conflit peut être quelque chose de difficle à appréhender au premier abord, une section y est consacrée dans la suite du TP.

La branche `creation-branches` a été utilisé pour isoler un travail et a été fusionné sur `master`. Cette dernière étape faite, nous n'avons plus besoin de la branche `creation-branches`. Celle-ci peut être supprimée.

> **Manipulation** : Supprimez la branche `creation-branches` :
>
> ```bash
> $ git branch -d creation-branches
> ```

## En conclusion

Nous avons vu comment :

* créer une branche : `branch <ma branche>`,
* se positionner sur une branche : `checkout <ma branche>`,
* fusionner une branche : `merge <ma branche>`,
* supprimer une branche : `branch -d <ma branche>`.
