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

* un prénom et nom (ou pseudo)
* une adresse mail

```bash
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```

Il s'agit de la configuration minimale obligatoire pour utiliser Git. Néanmoins, certaines configurations de base peuvent vous être utiles :

```bash
$ git config --global core.editor vim  ## Configurer l'éditeur de texte pour éditer les messages de commit.
```

___