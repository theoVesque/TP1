# La brève introduction

## La gestion de versions

La gestion de version consiste à gérer les modifications apportées à un ensemble de fichiers d'un projet, et à garder tous les états par lesquels ils sont passés.

Avant l'arrivée des systèmes de gestion de versions, il était ordinaire de conserver le code source sous archive ZIP et de stocker cela sur un serveur pour le partager avec d'autres collaborateurs. C'était une pratique fastidieuse, car réalisée manuellement et source d'erreurs. Les systèmes de gestion de version ont grandement simplifié la gestion du code source.

## Les systèmes de gestion de versions

Les systèmes de gestion de versions (ou *VCS*) sont utilisés pour faciliter la gestion de versions. En outre, ils vous permettront de :

* enregistrer les modifications apportées à un projet,
* visualiser les changements à travers le temps,
* revenir à un état précédent,
* détecter plus facilement les modifications porteuses d'erreurs.

Les *VCS* éliminent la crainte du changement et permet de revenir à un état stable du projet à n'importe quel moment. Vous pouvez donc expérimenter toute sorte de chose sur votre projet sans risquer de perdre des informations.

### Les types de *VCS*

Il existe plusieurs types de *VCS* :

* les ***VCS* centralisés** ou *CVCS* (Subversion, Perforce, ...) : ce type de *VCS* fournit un dépôt central situé sur un serveur sur lequels les contributeurs du projet peuvent se connecter, et extraire ses fichiers pour les modifier. Leur utilisation est simple, mais l'inconvénient majeur de ces systèmes est justement la centralisation du dépôt qui peut empêcher les contributeurs de travailler en cas d'indisponibilité du serveur sur lequel est stocké le dépôt.

![CVCS](../img/cvcs.png)

* les ***VCS* décentralisés** ou *DVCS* (*Git*, *Mercurial*, ...) : ce type de *VCS* pallient aux inconvénients des *CVCS*. La mise à jour des fichiers ne passe plus par l'extraction de ces fichiers, mais par la duplication du dépôt central. Chaque contributeur peut travailler indépendamment des autres contributeurs et sans connexion permanente avec le serveur central.

![DVCS](../img/dvcs.png)

## Git

*Git* est un *DVCS* libre et open-source initié par Linus Torvalds. Il s'agit du *VCS* le plus utilisé au monde (le *CVCS* Subversion arrive en seconde place).

L'outil présente de nombreux avantages :

1. Il est **rapide** : La quasi-totalité de ses opérations s'effectue en local, donc pas d'appel réseau à chaque exécution d'une commande.
2. Il est **décentralisé** : le dépôt est dupliqué en local. On peut donc travailler localement sans dépendre du dépôt central situé sur un serveur. Même si le dépôt central est corrompu, les contributeurs ayant cloné le projet ont une copie locale du dépôt et peuvent toujours le repousser sur un serveur.
3. Il utilise un **modèle basé sur les branches** : Sous Git, un historique de versions n'est pas linéaire. On peut créer des branches pour gérer des versions alternatives du projet, cela permet notamment de gérer différentes versions du projet, d'isoler les évolutions d'une version spécifique et de les reporter sur une version une fois le travail terminé.

___