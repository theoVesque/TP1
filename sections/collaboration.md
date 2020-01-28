# La collaboration sous Git

Jusqu'à maintenant, nous avons appris :

* à travailler avec les commandes de base de *Git* sur une unique branche,
* à manipuler les branches pour isoler notre travail, et le fusionner une fois celui-ci terminé.

Le second point est utile, même primordial dans le cadre d'une collaboration avec d'autres personnes d'un même dépôt. Pour le moment, nous avons appris à travailler seul, mais il est courant de travailler en équipe au sein d'un même projet, et qu'un dépôt *Git* ait donc plusieurs contributeurs.

Cette partie se concentrera principalement sur les commandes permettant le trvail en équipe, et notamment :

* la récupération des commits,
* la collaboration de plusieurs personnes sur une même branche de travail,
* la gestion de conflits lors d'une fusion de branches.

## Travailler à plusieurs sur une même branche

> **Information** : Cette section est uniquement à titre informatif, il n'y aura pas de manipulations à faire.

*Git* étant décentralisé, chacun possède l'ensemble de l'historique du dépôt sur son poste local et peut travailler et publier des changements comme il le souhaite. De ce fait, deux développeurs peuvent être amenés à travailler chacun sur une branche locale pointant sur une même branche distante. Ceci générera une divergence entre la branche locale et la réference de la branche distante.

Pour récupérer les commits, vous pourrez toujours exécuter un `git pull`. Mais le résultat sera comme celui-ci :

```bash
      A---B---C origin/master
     /         \
D---E---F---G---H master
```

Les commits `A`, `B` et `C` ont été poussé par un développeur sur la branche `master` (représenté par `origin/master`), et de votre côté, vous aviez les commits `F` et `G`. En fait, `git pull` est un raccourci regroupant deux commandes :

* `fetch` : récupère les données du dépôt central vers votre dépôt local,
* `merge` : pour fusionner la référence de la branche distante `origin/master` sur la branche locale `master`.

Le `pull` vu dans la section précédente ne présentait pas ce problème, car il n'y avait pas de divergence entre la branche locale et sa branche distante. On dit que le `merge` du `pull` de la section précédente s'est fait en **fast-forward**, ce qui veut dire que, dans l'historique, la référence de la branche locale a avancé jusqu'à la référence de la branche distante pour se mettre à jour.

Dans notre cas, on a un commit `F` et `G` sur notre branche. Si on exécute un `git pull` sur notre branche, le `merge` du `pull` se fera en **no-fast-forward**, c'est-à-dire qu'il va créer un commit de fusion pour mettre à jour sa branche.

En terme de lisibilité, l'historique n'est pas propre. Plutôt qu'un `pull` classique, nous pouvons utiliser un `git pull --rebase`. Cette option récupérera les commits de la branche distante sur le local et positionnera vos commits après ceux qui ont été récupéré. Avec cette option, les actions effectuées sont un `fetch` et un `rebase` (permettant de repositionner l'intégralité des commits d'une branche sur une autre).

```bash
D---E---A---B---C---F`---G`---H` origin/master + master
```

Les commits `F`, `G` et `H` ont été appliqués après les commits récupérés du dépôt central. Le contenu des commits ont potentiellement changé du fait qu'ils prennent désormais en compte les modifications des commits `A`, `B` et `C`. Ils ont donc été réécrit tenant compte de ces modifications.

## Récupération des commits depuis le dépôt central

Nous avons vu dans la partie précédente comment pousser ses commits sur le dépôt central. Si un autre développeur travaillant sur le même projet souhaite récupérer le travail poussé par vous ou un autre contributeur, il devra exécuter la commande :

```bash
$ git pull
```

Cette commande mettra à jour la branche sur laquelle vous vous situez actuellement (sur laquelle pointe votre `HEAD`).

> **Manipulation** : Récupérer les commits.
>
> Si ce n'est pas déjà fait, positionnez-vous sur la branche `master`.
>
> **Avertissement** : Pour cet exercice, vous avez deux possibilités :
>
> * **Vous continuez à travailler seul** : sur le dépôt que vous avez poussé dans la section précédente, exécutez la commande `git reset --hard HEAD~1` (cette commande a pour effet de positionner la branche locale d'un commit en arrière). En affichant le `status` du dépôt, celui-ci vous indiquera que vous êtes en retard d'un commit. En affichant l'historique, vous constaterez que la référence de la branche locale `master` est plus ancienne par rapport à la référence de la branche distante `origin/master`. Faites un `git pull` et affichez l'historique. **Vous avez mis à jour votre branche**.
> * **Vous vous mettez en duo, en trio ou plus** : comme vous avez poussé tous les deux un nouveau dépôt dans la section précédente, l'un de vous devra cloner (`clone`) le dépôt de l'autre pour que vous puissiez travailler sur le même dépôt. Ensuite, l'un de vous créera un commit (`commit`) et le poussera (`push`). L'autre exécutera un `git fetch` ayant pour effet de récupérer les commits du dépôt central. en affichant l'historique `log`, vous constaterez un retard sur votre branche courante. Exécutez la commande `git pull`. La personne ayant récupéré le(s) commit(s) affichera de nouveau l'historique Git. Vous devrez voir les commits poussés par votre duo.

## Gérer les conflits de fusion de deux branches

Nous avons vu dans la partie précédente qu'une fusion de branches peut se passer sans aucun souci. Dans cette section, nous allons voir que ce n'est pas toujours le cas et aborder une notion plus ou moins compliqué à appréhender : la **résolution de conflits**.

Les conflits peuvent survenir de plusieurs types de commandes :

* `merge`,
* `rebase`,
* `cherry-pick`,
* ou l'application d'un `patch`.

Il survient lorsque deux branches divergentes ont modifiées au moins une même ligne d'un même fichier, et que ces lignes sur les deux branches ont un contenu différent.

Dans la quasi-totalité des cas, malheureusement, la résolution d'un conflit nécessite une intervention humaine, et ne peut être résolu de manière automatique par *Git*.

> **Manipulation** : Clonez le projet suivant dans un autre répertoire :
>
> ```bash
> $ git clone https://github.com/sjaupart/cooking-recipes.git
> ```
>
> Dans ce dépôt se trouve une référence vers une branche distante nommé `origin/fix-salt-quantity`. Positionnez-vous sur cette branche avec un `git checkout fix-salt-quantity`.
>
> Regardez à quoi ressemble les changements de cette branche. Puis repositionnez-vous sur `master`, et exécutez :
>
> ```bash
> $ git merge fix-salt-quantity
> ```
>
> L'invite de commande devrait vous indiquer un conflit et vous demande de le résoudre. Nous allons essayer de comprendre ce qui s'est passé et corriger ce conflit. Ouvrez le fichier `pancakes.txt`, vous devriez voir quelque chose comme ceci :
>
> ```bash
> <<<<<<< HEAD
> 1 noisette de beurre
> 1 pincée de sel
> =======
> 1 noisette d ebeurere
> 2 pincées de sle
> >>>>>>> fix-salt-quantity
> ```
>
> Deux blocs se distinguent dans le fichier :
>
> * Le premier bloc `HEAD` correspond au bout de code de la branche sur laquelle vous étiez au moment du merge.
> * Le second bloc `fix-salt-quantity` correspond au bloc de la branche que vous avez fusionné.
>
> Pour résoudre le conflit, il faut être capable d'identifier si l'application d'un changement est légitime ou non pour garder une certaine cohérence au niveau du code :
>
> * sur la branche `master`, les changements apportés à cette portion de code consistait à corriger les erreurs de frappe (`sle` => `sel`),
> * sur la branche `fix-salt-quantity`, les changements apportés à cette portion de code consistait à modifier la quantité de sel (`1` => `2`).
>
> Autrement dit, les modifications apportées sur cette ligne ont une portée indépendante, il faut donc garder les deux modifications, car elles sont toutes les deux pertinentes, ce qui donnera :
>
> ```bash
> 1 noisette d ebeurere
> 2 pincées de sel
> ```
>
> **Manipulation** : Modifiez le fichier pour prendre en compte les deux changements. Ajoutez le fichier `pancakes.txt` à l'index et continuez la fusion :
>
> ```bash
> $ git merge --continue
> ```
>
> La fusion est censé se terminer correctement. Regardez l'historique et le contenu du fichier `pancakes.txt`. Tous les changements se sont appliqués correctement.

Pour cet exemple, le traitement du `merge` restait simple. Si, dans notre exemple, nous avions eu un changement de quantité de sel sur les deux branches, il aurait été nécessaire de se référer aux développeurs responsables de ces changement pour savoir comment résoudre le conflit correctement. L'intervention humaine reste obligatoire.

Des outils comme P4Merge ou l'outil de résolution de conflit de l'IDE IntelliJ existent pour gérer les conflits plus efficacement. L'utilisation d'une interface graphique pour la résolution facilite grandement le travail (néanmoins, vérifiez toujours le contenu du fichier après résolution).

## En conclusion

Dans cette partie, nous avons vu comment :

* récupérer le travail d'un autre développeur : `pull`,
* récupérer le travail d'un autre développeur sans commit de fusion : `pull --rebase`,
* gérer les conflits suite à un `merge` (la gestion de conflits est la même pour un `rebase` ou une application de `patch`).
