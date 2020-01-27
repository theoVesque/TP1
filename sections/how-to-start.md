## Démarrer sur un projet

Il existe deux manières pour commencer à travailler sur un dépôt Git :

* Initialiser un nouveau projet.
* Cloner un projet existant.

### Initialiser un nouveau dépôt

Un dépôt Git (ou *Git repository*) est un simple répertoire contenant un dossier *.git*. Cependant, ce répertoire n'est pas créé manuellement par l'utilisateur. Il est généré par la commande `git init`.

> **Manipulation** : Pour créer un dépôt Git, créez un répertoire sur votre poste, placez-vous à l'intérieur et exécutez la commande suivante.
>
> ```bash
> $ git init
> ```

### Cloner un dépôt existant

Il existe des plateformes permettant le stockage et la gestion du code source versionné avec Git ([GitHub](https://github.com/), [GitLab](https://about.gitlab.com/), [BitBucket](https://bitbucket.org/), ...). Elles donnent accès librement ou non aux projets publiés sur celles-ci, et il est possible de contribuer à ces projets en les clonant.

Ce sujet de TP est d'ailleurs versionné avec Git, et libre d'accès. Nous allons le cloner, et l'utiliser pour la suite de ce TP.

> **Manipulation** : Clonez ce projet : `git clone https://github.com/sjaupart/git-init.git`
>
> Vous devez avoir un résultat de ce type :
>
> ```bash
> $ git clone https://github.com/sjaupart/git-init.git
> Cloning into 'git-init'...
> remote: Enumerating objects: 223, done.
> remote: Total 223 (delta 0), reused 0 (delta 0), pack-reused 223R
> Receiving objects: 100% (223/223), 27.91 KiB | 277.00 KiB/s, done.
> Resolving deltas: 100% (39/39), done.
> ```

Le clonage a créé un répertoire *git-init* qui est notre dépôt Git.

> **Information** : En dehors des commandes `config`, `init` et `clone`, les commandes Git ne peuvent s'exécuter que dans un dépôt Git. Une commande Git exécutée hors dépôt vous enverra ce message explicite :
>
> $ git log
> fatal: Not a git repository (or any of the parent directories): .git

___