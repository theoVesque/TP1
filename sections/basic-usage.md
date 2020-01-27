## Utilisation basique

Dans cette partie, nous allons aborder les commandes permettant une utilisation de base de Git (nous n'aborderons pas encore la gestion des branches et la collaboration entre contributeurs d'un même projet).

Nous verrons comment :

* consulter l'historique d'un projet,
* différencier deux versions à un instant T,
* publier un changement.

### Analyser l'historique du projet

Précédemment, vous avez cloné ce sujet de TP sur votre poste. Nous allons consulter son historique pour connaître les changements apportés à ce projet.

> **Manipulation** : Exécutez la commande
>
> ```bash
> $ git log
> ```

L'historique affiché vous montre l'ensemble des changements apportés au projet et classés de manière antichronologique.

```bash
$ git log
commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    changed the version number

commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Sat Mar 15 16:40:33 2008 -0700

    removed unnecessary test
```

Chaque bloc apparaissant dans l'historique correspond à un **commit** (ou *instantané* en français, nous utiliserons néanmoins le terme *commit* pour le reste du TP).

Un *commit* est caractérisé par :

* un **identifiant** (une chaîne de 40 caractères hexadécimaux appelé **empreinte SHA-1**),
* un **auteur**,
* une **date de création**,
* un **message explicatif** (rédigé par l'auteur),
* un **ensemble de changements** (non affiché par défaut).

> **Manipulation** : Plus concrètement, pour afficher l'historique avec le détail des changements pour chaque fichier du projet, ajoutez l'option `-p` à la commande précédente.
>
> ```bash
> $ git log -p
> ```
>
> Les changements sont représentés par des ajouts et suppressions de lignes (caractérisés respectivement par des `+` et des `-` au début de chaque ligne modifiée).

On a tendance à privilégier l'usage d'outils graphiques à la ligne de commande pour la consultation de l'historique d'un projet. En ligne de commande, et même sans l'option `-p`, le `log` peut être assez verbeux. Néanmoins, cette commande possède un très grand nombre d'options pour simplifier l'affichage, rechercher des informations, ... et il est profitable de l'associer avec certaines options.

Parmi les options les plus importantes à utiliser avec la commande `log`, nous avons :

* `--oneline` : affiche les informations d'un *commit* sur une ligne.
* `--graph` : affiche l'historique du projet sous forme de graphe (utile pour l'affichage des différentes branches que nous verrons dans la suite de ce TP).
* `--decorate` : affiche le nom des références (branches, tags, ...) dans l'historique.
* `--abbrev-commit` : limitant la taille des SHA-1 de *commit* à 7 caractères au lieu de 40 (les 7 premiers caractères étant suffisants à l'identification d'un *commit*).

> **Manipulation** : Exécutez la commande `git log` en associant les différentes options citées ci-dessus. Vous constaterez que seules les informations utiles à l'affichage sont présentées.

### Utilisation des alias

Dans la section précédente, nous avons vu comment consulter l'historique d'un projet avec `git log` et ses options. Cependant, il est incommode de saisir cette commande avec ses options à chaque fois juste pour une consultation d'historique. Git simplifie l'usage de ses commandes, notamment par la création d'**alias**.

> **Manipulation** : Prenons la commande suivante stylisant le `log` :
>
> ```bash
> $ git log --graph --date=relative --pretty=tformat:'%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%an %ad)%Creset'
>```
>
> Même si, plutôt que de retaper entièrement la commande, vous faites une recherche de celle-ci via un [`history`](https://mediatemple.net/community/products/dv/204404624/using-the-history-command), cela reste peu pratique. A la place, privilégiez la création d'un alias.
>
> **Manipulation** : Créez un alias `lg` :
>
> ```bash
> $ git config --global alias.lg "log --graph --date=relative --pretty=tformat:'%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%an %ad)%Creset'"
>```
>
> Cette commande crée un alias `lg` pour la commande `log` customisée avec ces options.
>
> **Manipulation** : Vous pouvez exécuter la commande `git lg` et constater la bonne configuration de l'alias.

> **Information** : A noter que les configurations Git possibles grâce à la commande `config` peuvent être définies à différents niveaux : **global**, **system** et **local**. Nous n'utiliserons que la configuration globale pour ce TP.

### Où suis-je positionné dans l'historique

L'historique affichable par la commande `log` liste les changements apportés à un projet dans le temps. Avec un *VCS*, nous savons que nous pouvons revenir à un état précédent dans le dépôt, mais encore faut-il savoir où on se trouve.

Si vous exécutez la commande `git lg` créée précédemment, vous verrez dans l'historique une référence `HEAD` définissant l'endroit où nous nous trouvons dans le projet. Généralement, la référence `HEAD` pointe sur une branche (`master`, ...) ou un tag, mais nous détaillerons ça plus tard.

### Créer un commit

Nous savons désormais consulter l'historique de ce projet. Dans cette section, nous allons apprendre à versionner des changements que vous allez faire sur ce projet.

#### Les différents états d'un fichier

Sous Git, il existe trois grands états dans lesquels les fichiers peuvent se trouver :

* le **répertoire de travail** (*working directory*) : contient les changements que vous avez apportés au projet. Il correspond à votre travail en cours.
* l'**index** (*staging area*): recense toutes les modifications des fichiers prêtes à être versionné.
* l'**historique** ou le **dépôt** (*repository*) : contient l'ensemble des commits du projet.

![](img/git_file_states.png)

> **Manipulation** : Pour consulter l'état courant du dépôt, vous pouvez utiliser la commande :
>
> ```bash
> $ git status
> ```

Cette commande classera les modifications de fichiers en trois sections :

* les **fichiers enregistrés dans l'index** (*changes to be committed* ou *staged*) : géré par l'index, donc prêt à être versionné,
* les **fichiers en cours de modification** (*changes not staged for commit* ou *modified*) : recense les modifications qui diffèrent de l'index, donc en cours de travail,
* les **fichiers non suivis** (*untracked files*) : concerne tous les nouveaux fichiers inconnus (non versionnés) du dépôt.

![](img/git_files.png)

> **Manipulation** : Modifiez n'importe quel fichier de ce projet, et lancez un `git status`.
>
> Le fichier modifié apparaîtra dans le répertoire de travail.

#### Versionner un changement

> **Information** : Vous serez amené à saisir des messages de commit. Si vous souhaitez utiliser un éditeur de texte particulier, vous pouvez utiliser la commande suivante :
>
> ```
> $ git config --global core.editor vim  ## pour utiliser Vim
> $ git config --global core.editor nano ## pour utiliser Nano
> etc...
> ```

Si vous avez modifié un fichier d'un dépôt Git, celui-ci apparaîtra dans le répertoire de travail. Les fichiers apparaissant à cet endroit peuvent être ajoutés à l'index et versionné grâce à la commande `git commit`.

> **Manipulation** : Ajoutez le fichier modifié à l'index :
>
> ```bash
> $ git add README.md
> ```
>
> Le fichier *README* est ajouté à l'index. Vous pouvez vérifier cela grâce à un `git status`.
>
> Le fichier peut être versionné :
>
> ```bash
> $ git commit
> ```
>
> Un éditeur par défaut est censé s'ouvrir pour vous permettre de saisir votre message de commit. Saisissez-le, enregistrez-le et fermez l'éditeur.
>
> Le commit est créé.
>
> Vous pouvez consulter l'historique et voir qu'il a bien été créé.

### En conclusion

Nous avons vu comment :

* consulter l'historique d'un projet Git,
* créer des alias,
* connapitre l'état des répertoires de travail,
* versionner un ensemble de fichiers.

Pour le moment, nous n'avons travaillé que sur une seule branche. Dans la partie suivante, nous allons découvrir le système de branches de Git.

___