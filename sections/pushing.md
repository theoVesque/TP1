# Partage et mise à jour

*Git* possède plus de 150 commandes différentes et, comme dit précédemment, la quasi-totalité d'entre elles agissent uniquement en local. Parmi les quelques commandes agissant en mode distant, on retrouve les plus utilisées :

* `push` : pousse les changements d'une branche sur le dépôt distant,
* `fetch` : récupère les commits, références de branches distantes et de tags poussés par d'autres utilisateurs sans mettre à jour les branches,
* `pull` : met à jour la branche sur laquelle vous vous trouvez. En réalité, cette commande est un raccourci utilisant par défaut `fetch` puis `merge` pour mettre à jour la branche actuelle.

Pour pouvoir pousser ou récupérer des références depuis un dépôt central, il est nécessaire de configurer le dépôt pour pointer vers le dépôt central en question. Vu que vous avez cloné ce projet depuis GitHub, cette configuration existe déjà.

> **Manipulation** : Pour voir la configuration vers le dépôt distant, exécutez la commande :
>
> ```bash
> $ git remote -v
> ```
>
> Supprimez cette configuration :
>
> ```bash
> $ git remote remove origin
> ```

## Création d'un dépôt distant

> **Manipulation** :
>Vous allez créer votre propre dépôt distant sur GitHub.
>
> 1. Vous aurez tout d'abord besoin de créer un compte.
> 2. Une fois créé, créez un nouveau dépôt sur GitHub du nom de votre choix.
> 3. Le dépôt créé, GitHub vous proposera de configurer votre dépôt local pour pointer vers le distant (nous utiliserons le protocole HTTPS pour pousser ou récupérer des commits).
>
> La commande se présentera sous la forme : `git remote add origin <une url>`.
>
> Vérifiez la bonne configuration avec un `git remote -v`.
>
> Exécutez la commande :
>
> ```bash
> $ git push origin master
> ```
>
> Pour vérifier que vos commits ont bien été poussés, vous pouvez aller consulter le dépôt central sur GitHub.

Toutes les branches que vous pousserez auront leur équivalence sur le dépôt central. En local, une référence vers une branche distante sera toujours nommée de la manière suivante : `*remote/branche*` où `remote` correspond à la configuration de votre dépôt pour pointer vers un dépôt central et `branche` correspond à votre nom de branche.

> **Information** : Notion de *remote tracking branch*
>
> Une branche poussée possède son équivalence sur le dépôt distant. Pour voir ce lien : `git remote show origin`.
>
> Cela indiquera comment les branches locales et distantes sont liées entre elles. Une branche locale qui ne tracke pas une branche distante ne pourra pas se mettre à jour et générera cette erreur :
>
> ```bash
> $ git pull
> There is no tracking information for the current branch.
> Please specify which branch you want to rebase against.
> See git-pull(1) for details.
>
>    git pull <remote> <branch>
>
> If you wish to set tracking information for this branch you can do so with:
>
>    git branch --set-upstream-to=origin/<branch> master
>
> ```

## En conclusion

Nous avons vu comment :

* pousser des modifications : `push`,
* lier un dépôt local et un dépôt distant : `remote`.

Toutes les commandes vues jusqu'à maintenant sont utiles et nécessaires pour versionner un projet dans le cadre d'un travail individuel. Néanmoins, plusieurs personnes peuvent être amenées à contribuer sur le même projet.

Il est donc nécessaire de connaître certaines actions et principes liés au travail en équipe.