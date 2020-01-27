# Découverte de Git

## La brève introduction

___

## Et c'est parti ! (Installation et configuration)

### Installation

Pour Windows, vous pouvez télécharger Git sur le [site officiel](http://git-scm.com).
Pour Linux, vous pouvez passer par un `sudo apt install git-all`.

Une fois l'installation terminée, ouvrez un terminal et tapez `git --version`. Vous devriez avoir une réponse du type :

```bash
$ git --version
git version 2.15.1.windows.2
```

### Quels outils pour utiliser Git

Idéalement, nous privilégierons le **terminal de commande**. Il existe une multitude d'outils graphiques facilitant l'utilisation de Git, mais, dans une grande majorité des cas, ces derniers ne supportent l'entiéreté des commandes et options possibles en ligne de commande.

Dans un premier temps, il sera préférable d'apprendre par la ligne de commande avant d'utiliser une interface graphique servant de surcouche, pour mieux appréhender et comprendre l'intérêt et les possibilités de Git.

Vous trouverez tout de même une [liste d'outils graphiques](#liste-doutils-graphiques) à la fin de ce TP.

### Première configuration

Git trace les changements apportés par les différents contributeurs d'un projet. Pour pouvoir apporter des changements à un projet, il est nécessaire de fournir votre identité, à savoir :

- un prénom et nom
- une adresse mail

```bash
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```

Il s'agit de la configuration minimale obligatoire pour utiliser Git. Néanmoins, certaines configurations de base peuvent vous être utiles :

```bash
$ git config --global core.editor vim  ## Configurer l'éditeur de texte pour éditer les messages de commit.
```

___

## Démarrer sur un projet

Il existe deux manières pour commencer à travailler sur un dépôt Git :

- Initialiser un nouveau projet.
- Cloner un projet existant.

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

## Utilisation basique

Dans cette partie, nous allons aborder les commandes permettant une utilisation de base de Git (nous n'aborderons pas encore la gestion des branches et la collaboration entre contributeurs d'un même projet).

Nous verrons comment :

- consulter l'historique d'un projet,
- différencier deux versions à un instant T,
- publier un changement.

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

- un **identifiant** (une chaîne de 40 caractères hexadécimaux appelé **empreinte SHA-1**),
- un **auteur**,
- une **date de création**,
- un **message explicatif** (rédigé par l'auteur),
- un **ensemble de changements** (non affiché par défaut).

> **Manipulation** : Plus concrètement, pour afficher l'historique avec le détail des changements pour chaque fichier du projet, ajoutez l'option `-p` à la commande précédente.
>
> ```bash
> $ git log -p
> ```
>
> Les changements sont représentés par des ajouts et suppressions de lignes (caractérisés respectivement par des `+` et des `-` au début de chaque ligne modifiée).

On a tendance à privilégier l'usage d'outils graphiques à la ligne de commande pour la consultation de l'historique d'un projet. En ligne de commande, et même sans l'option `-p`, le `log` peut être assez verbeux. Néanmoins, cette commande possède un très grand nombre d'options pour simplifier l'affichage, rechercher des informations, ... et il est profitable de l'associer avec certaines options.

Parmi les options à utiliser avec la commande `log`, nous avons l'option :

- `--oneline` : affiche les informations d'un *commit* sur une ligne.
- `--graph` : affiche l'historique du projet sous forme de graphe (utile pour l'affichage des différentes branches que nous verrons dans la suite de ce TP).
- `--decorate` : affiche le nom des références (branches, tags, ...) dans l'historique.
- `--abbrev-commit` : limitant la taille des SHA-1 de *commit* à 7 caractères au lieu de 40 (les 7 premiers caractères étant suffisants à l'identification d'un *commit*).

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
> Cette commande crée un alias `lg` pour la commande `log` customisée.
>
> **Manipulation** : Vous pouvez exécuter la commande `git lg` et constater la bonne configuration de l'alias.

> **Information** : A noter que les configurations Git possibles grâce à la commande `config` peuvent être définies à différents niveaux : **global**, **system** et **local**. Nous n'utiliserons que la configuration globale pour ce TP.

___

## Gestion des branches

## Partage et mise à jour

## En supplément...

### Liste d'outils graphiques

- Git GUI (Windows, Linux, MacOS)
