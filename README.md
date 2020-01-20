# Découverte de Git

## La brève introduction


## Et c'est parti ! (Installation et configuration)

### Installation

Pour Windows, vous pouvez télécharger Git sur le [site officiel](http://git-scm.com).
Pour Linux, vous pouvez passer par un `sudo apt install git-all`.

Une fois l'installation terminée, ouvrez un terminal et tapez `git --version`. Vous devriez avoir une réponse du type :

```bash
git version 2.15.1.windows.2
```

### Première configuration

Git trace les changements apportés par les différents contributeurs d'un projet. Pour pouvoir apporter des changements à un projet, il est nécessaire de fournir votre identité, à savoir :
- un prénom et nom
- une adresse mail

```bash
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```
Il s'agit de la configuration minimale obligatoire pour utiliser Git. Néanmoins, certaines configurations de base peuvent vous être utiles :

```bash
git config --global core.editor vim  ## Configurer l'éditeur de texte pour éditer les messages de commit.
```

## Démarrer sur un projet

Il existe deux manières pour commencer à travailler sur un dépôt Git :
- Initialiser un nouveau projet.
- Cloner un projet existant.

### Initialiser un nouveau dépôt

### Cloner un dépôt existant

## Utilisation basique

## Gestion des branches

## Partage et mise à jour
