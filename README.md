# `utilitR` : une documentation utile pour `R`  <a href='https://www.utilitr.org'><img src='resources/logo-utilitR.svg' align="right" height="139px" /></a>

<!-- badges: start -->
[![build-doc Actions Status](https://github.com/InseeFrLab/utilitR/workflows/bookdown/badge.svg)](https://github.com/InseeFrLab/utilitR/actions)
[![build-doc Actions Status](https://github.com/InseeFrLab/utilitR/workflows/pagedown%20PDF/badge.svg)](https://github.com/InseeFrLab/utilitR/actions)
[![build-doc Actions Status](https://github.com/InseeFrLab/utilitR/workflows/construction%20image%20docker/badge.svg)](https://github.com/InseeFrLab/utilitR/actions)
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gl/linogaliana%2FdocumentationR/binder?urlpath=rstudio)
<!-- badges: end -->

 
Code source pour le projet `utilitR`, documentation collaborative `R` 
à l'usage des agents de l'Insee. Elle a vocation à être validée annuellement 
afin de produire un guide des bonnes pratiques et des fiches techniques.

Elle prend la forme d'un livre qui est déployé à l'adresse <https://www.book.utilitr.org/>. 

Il est également possible de télécharger le fichier au format `pdf` 
ou les  fichiers `html` pour les consulter hors-connexion en cliquant
[ici](https://gitlab.com/linogaliana/documentationR/-/jobs/artifacts/master/download?job=bookdown)

# Présentation du projet `utilitR`

## Objectifs de la documentation `utilitR`

**Cette documentation s'adresse à tous utilisateur de `R` dans le cadre d'un usage courant pour l'analyse de données.** Elle est conçue pour aider les utilisateurs à réaliser des traitements statistiques usuels avec `R` et à produire des sorties (graphiques, cartes, documents). Cette documentation présente succinctement les outils les plus adaptés à ces tâches, et oriente les agents vers les ressources documentaires pertinentes. En revanche, elle n'aborde pas les outils les plus avancés, notamment ceux utilisés dans un cadre de développement logiciel.

Cette documentation a pour ambition de répondre à trois questions générales:

* Comment travailler avec `R` à l'Insee?
* Comment réaliser des tâches standards avec `R` (importation et manipulation de données, exploitation d'enquêtes, graphiques...)?
* Quelles sont les bonnes pratiques à respecter pour bien utiliser `R`?

Deux points importants sont à noter:

* **Cette documentation recommande les outils et les *packages* les plus adaptés au contexte d'utilisation de `R` à l'Insee**. Ces recommandations ne sont pas nécessairement adaptées à d'autres contextes, et pourront évoluer lorsque ce contexte évoluera.
* **Cette documentation recommande d'utiliser `R` avec `Rstudio`**, qui apparaît comme la solution la plus simple et la plus complète pour un usage courant de `R`, et qui est par ailleurs le choix effectué par l'Insee.

##  Place du projet `utilitR` au sein de l'Insee

**Le projet `utilitR` est porté par les agents du réseau LS<sup>2</sup> (Logiciels statistiques en Libre Service) de l'Insee.** La documentation `UtilitR` s'attache à être cohérente avec les recommandations émises par le comité de certification des _packages_ `R` (COPS).

## Comment contribuer à la documentation

**Le projet `UtilitR` est un projet collaboratif, évolutif, *open source* et ouvert à tous, auquel tous les agents peuvent contribuer.** Le projet est mené par un groupe de contributeurs qui en définissent eux-mêmes le contenu, la structure et le calendrier. Les objectifs et l'approche collaborative du projet `UtilitR` sont détaillés dans [`ce document`](Manifeste.md).

**Tout agent qui le souhaite peut modifier ou compléter la documentation en fonction de ses connaissances et de ses expériences**, et toutes les contributions sont les bienvenues: compléments, corrections d'erreur, améliorations, questions... Il n'y a aucun prérequis, et aucun niveau minimal en `R` n'est demandé. Le dépôt de la documentation est situé [ici](https://github.com/InseeFrLab/utilitR). Toute personne intéressée à contribuer au projet est invité à consulter le guide des contributeurs (`CONTRIBUTING.md`).

# Environnement de travail

Plusieurs solutions sont possibles pour disposer de l'environnement de travail nécessaire à la compilation de cette documentation : 

- pour une installation sur un poste, voir la procédure d'[installation des _packages_](#installation-des-packages). _Cette solution ne garantit pas la reproductibilité._

- [l'utilisation d'un container](#utilisation-dun-container). _Cette solution vous offre des garanties élevées de reproductibilité._

## Installation des _packages_

Les _packages_ nécessaires sont déclarés dans le fichier [DESCRIPTION](DESCRIPTION).  
Vous pouvez les installer en exécutant : 

```r
install.packages("remotes")
remotes::install_deps(dependencies = TRUE)
```

## Utilisation d'un container

L'environnement de travail utilisé pour la compilation de la documentation est disponible sous la forme d'une image docker :

```
docker.io/inseefrlab/utilitr:latest
```

Cette image comprend toutes les dépendances système ainsi que les packages R nécessaires à la compilation du livre.  
Il comprend également RStudio : voir la procédure ci-après pour exécuter cet environnement.

### Container temporaire

_Cette solution vous sera utile si vous souhaitez apporter une modification ponctuelle au projet._

#### Utilisation en ligne avec Binder

Afin d'assurer une parfaite reproductibilité, un environnement de travail est disponible en ligne en cliquant sur ce bouton 
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gl/linogaliana%2FdocumentationR/binder?urlpath=rstudio).

Vous arrivez sur un environnement de travail RStudio avec tous les packages déjà installés. Cet environnement utilise le service [Binder](https://mybinder.org) : il peut être indisponible ponctuellement.

#### Utilisation sur un poste de travail

Si docker est installé sur votre machine, vous pouvez exécuter : 

```bash
docker run --rm -p 8787:8787 -e PASSWORD=monpassword docker.io/inseefrlab/utilitr:latest
```

Vous pouvez remplacer `monpassword` par le mot de passe de votre choix.

Un serveur RStudio est alors disponible à l'url <http://127.0.0.1:8787>.  
Pour vous connecter sur ce serveur, vous devez utiliser :

- nom d'utilisateur : `rstudio`
- mot de passe : le mot de passe choisi ci-dessus (`monpassword`) dans l'exemple.

Une fois connecté à RStudio, vous devez ensuite cloner le projet <https://github.com/InseeFrLab/utilitR.git>.  
Si vous opérez des modifications, n'oubliez pas de transmettre vos modifications à l'aide de `git` grâce à un `push`. En effet, l'utilisation de l'option `--rm` détruira automatiquement votre container et son système de fichiers.

### Container permanent

Il vous est possible de créer un container permanent (attention, celui peut-être obsolète si de nouvelles dépendances sont ajoutées) ce qui vous permettra de ne pas perdre vos fichiers.

Créez un container appelé `mon_container` (vous pouvez changer ce nom) en mode détaché :

```bash
docker run --name mon_container -d -p 8787:8787 -e PASSWORD=monpassword docker.io/inseefrlab/utilitr:latest
```

Vous pouvez aussi attacher un volume à ce container grâce à l'option `-v` (sous linux, n'oubliez pas de rajouter l'option `-e USERID=$UID`). Par exemple, pour ajouter vos clés `ssh` : 

```bash
docker run --name mon_container -d -p 8787:8787 -v $HOME/.ssh:/home/rstudio/.ssh -e USERID=$UID -e PASSWORD=monpassword docker.io/inseefrlab/utilitr:latest
```

Une fois ce container créé et lancé, vous pouvez vous connecter sur le serveur RStudio disponible à l'adresse <http://127.0.0.1:8787>. Pour se connecter, le nom d'utilisateur est `rstudio` et le mot de passe `monpassword`.

Dans RStudio, vous pouvez ensuite cloner le projet <https://github.com/InseeFrLab/utilitR.git> et travailler. N'oubliez pas de sauvegarder vos modifications.

Une fois que vous avez fini de travailler :

- dans RStudio, cliquez sur l'icone rouge située en haut à droite _"Quit the current R session"_.
- dans votre terminal, exécutez : 
  ```bash
  docker stop mon_container
  ```

Pour relancer plus tard votre serveur RStudio et retrouver vos fichiers, vous pouvez redémarrer votre container : 

```bash
docker start mon_container
```
