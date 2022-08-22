# Installation de octobercms avec docker.

> **Nous avons besoin de Ubundu : linux terminal**
>
> _1,2,3,4_.

- Envie de connaître le projet final **lien du site web** [^1]

[^1]: [Voici le lien du projet](https://administration-dashboard.herokuapp.com/#/)

## Table de matière

- [Admin dashboard](#admin-dashboard)
  - [Table de matière](#table-de-matière)
  - [Introduction](#introduction)
  - [Mise en place](#mise-en-place)
    - [Section 7](#section-7)
      - [Création du router authentification pour la page authentification](#création-du-router-authentification-pour-la-page-authentification)
    - [Section 8](#section-8)
      - [Création du formulaire de validation d’enregistrement & registre de navigation](#création-du-formulaire-de-validation-denregistrement--registre-de-navigation)
    - [Section 9](#section-9)
      - [Design du dashboard administratif](#design-du-dashboard-administratif)
    - [Section 10](#section-10)
      - [Backend pour le panel d'administration](#backend-pour-le-panel-dadministration)
    - [Section 11](#section-11)
      - [Authentication et protection des routes](#authentication-et-protection-des-routes)
    - [Section 12](#section-12)
      - [Créer le UI de la view Catégorie et lier le Backend de notre API à la page web](#créer-le-ui-de-la-view-catégorie-et-lier-le-backend-de-notre-api-à-la-page-web)
    - [Section 13](#section-13)
      - [Optimisation des routes pour éviter que notre application se redessine à tout moment](#optimisation-des-routes-pour-éviter-que-notre-application-se-redessine-à-tout-moment)
    - [Section 14](#section-14)
      - [Gestion des utilisateurs de l'application](#gestion-des-utilisateurs-de-lapplication)
    - [Section 15](#section-15)
      - [Télécharger des fichiers dans le backend et le lier avec Cloudinary et Déploiement de la version de notre application sur le web avec Heroku.](#télécharger-des-fichiers-dans-le-backend-et-le-lier-avec-cloudinary-et-déploiement-de-la-version-de-notre-application-sur-le-web-avec-heroku)
- [Utilisation des outils suivant](#utilisation-des-outils-suivant)

---

## Introduction

Nous allons installer Octobercms grâce à Docker et au terminal de linux : Ubundu . Pour en savoir plus sur le créateur [Sergio Nino](https://github.com/Sergioanino).

![screenshot.png](assets/screenshot.PNG)

---

## Mise en place

Aller sur Github et télécharger le projet avec un **clone** ou avec le **ZIP** [admin_dashboard](https://github.com/Sergioanino/admin_dashboard).

### Mise en place avec ubuntu & docker.

`Obtenez-le en exécutant la commande suivante pour obtenir les dépendances:`
`Il faut ouvrir la power shell avec mode admin:`

```
wsl --install
```

```
wsl -l -v
```

```
wsl --set-default-version 2
```

```
wsl --set-version Ubuntu 2
```

```
lsb_release -a
```

```
docker
```

```
ubuntu config --default-user root
```

```
mkdir -p /var/october/october_docker
cd /var/october/october_docker
```

```
bash -c "$(curl https://octobercms.com/api/dockerdevinstaller)"
```

```
default :8080 & 3333
```

```
code for open vscode : open de file !
```

```
\\wsl$\Ubuntu\var\october\october_docker
```

```
\\wsl$\Ubuntu\var\october\october_docker
```

---

### **Running CLI commands in the container**

#### Création du router authentification pour la page authentification.

- Install the extension.
- Open the Command Palette (ctrl+shift+p) and select Docker - Containers: Attach Shell.
- Select your container.
- That will open the Terminal panel attached to the container.

```
php artisan
```

```
./october-docker-install.sh
```

---

Sur le terminal :

1 : Connaître la version de docker : #7
docker --version ou docker -v

2 : Partir un container à partir d'un image : d'un projet sur le dockerHub - container des d'autres entreprise exemple : node.js et php: image !

- Docker pull : télécharge l'image mais ne va pas la faire courir.
  docker pull mysql

- Docker run : va faire courir l'image qui va se convertir dans un container.
  docker run <nom du container dockerHub>: <pour mettre un tag de la version>

exemple : docker run mysql:latest

\*\* : -e : Argument extra pour docker run : envoie un variable d'environnement pour le configurer.

Start a mysql server instance
Starting a MySQL instance is simple:

$ docker run --name <some-mysql> -e MYSQL_ROOT_PASSWORD=<my-secret-pw> -d mysql:tag -p <8080(externe):3030(interne)>

exemple : docker run --name <server_image_container> sergio_image -p 8080:3030

... where some-mysql is the name you want to assign to your container, my-secret-pw is the password to be set for the MySQL root user and tag is the tag specifying the MySQL version you want. See the list above for relevant tags.

3 : Créer un package json pour simplifier les images : container : FONCTIONNE : sur windows avant de créer un container.
nmp init -y

4 : Connaître les Images installer sur docker, et qui peuvent courir aussi sur l'ordinateur.

- add : | head - pour montrer seulement les derniers images.
  docker images ou docker images | head

5 : Connaître les containers qui courts dans mon ordinateur.
docker ps
docker ps -a : Il va nous montrer tous les containers run sur cette ordinateur.

ctrl+c sur un de container pour l'arrêter ou prendre le hashing du container avec la commande stop pour l'arrêter.
docker stop <hashing_container>

5.1 : Start un containers à partir d'un hashing :
docker start <hashing>

5.2 : Connaître les longing du container :
docker logs <hashing id container ou le nom du containers si specifier du moment de run le containers>

5.3 : Connaître le logs mais en attente de reception d'un log :
docker logs -f <hashing id>

% ! info : dans docker on écrit toujours en output ! Quand on fait docker logs on capture le container et l'image.

6 : RUN CMD & ENTRYPOINT différence : curl : c'est quoi ?

- run : run est pour lancer de commande au moment de construire l'image.

  -d : détacher le container pour le courir en background.

  docker run -d <nom de l'image>

- cmd : Les commandes qui vont s'executer par défaut au moment que tu run le container. exemple : pour courir un serveur : php,python & etc. En plus, nous pourrons sur-écrire une nouvelle commande pour écraser la commande par défaut, au moment de courir à nouveau l'image avec des commande extra : comme -it ou sh

- ENTRYPOINT : Les commandes vont être executer au moment d'initialiser le container sauf qu'il n'est pas créer pour qu'on l'utilise pour sur-écrire les commande, il est plus pour qu'il fonctionne comme un executable. Il est possible de le sur-écrire au moment de faire docker run avec de commande de plus.
  exemple : Il faut passer des arguments aux commande du container.

- exec va executer une commande à l'intérieur du container qui run déjà.

  -i : Une session interactif.
  -t : Émuler une terminal.

  sh : shell pour le terminal.

  docker exec -it <id hashing container> sh

  6.1 : Executer une image dans un container de manière interactive : De cette manière on rentre à l'intérieur d'un container!
  docker exec -it mymysql bash : exemple : docker exec -it sergio_image bash

- Cela va executer une bash sur notre système.

  6.2 : Voir les containers en execution. ps: show infos container execution.
  docker ps
  % Photo @lien assets

  6.1 Arrêter un container en execution.
  docker stop <hashing_container>

  6.2 Supprimer un container. arrêt du container avant suppression. rm: supprimer
  docker rm <hashing_container>

7 : 1er : Créer un dossier avec le nom : DockerFiles.

C'est quoi vim ? je crois que sa créer le dossier apres : - vim DockerFiles : Voir le fichier : DockerFiles pour la suite du Tuto.

7 : Créer un installateur de notre container avec tout les dépendes des apps pour le project.

    - docker build -t <nom du container> .<dit que ce sur ce folder est >

si nous voulons courir notre nouvelle image du container :

docker run <nom de l'image donné -t en haut>

    - Pour lui indique le port à courir au moment de run l'image pour le voir sur internet : -p 8080:3030

docker run -p 8080:3030 <nom de l'image>

ou -dp : mettre en veille l'écoute du log.

docker run -dp 8080:3030 <nom de l'image>

si nous voulons installer le thème et la console de zsh : sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

Pour persister les données ajouter au container et image de docker leur des ajouts sur la Database en ligne.

    - : - modification bidirectionnel

    - docker run -d -v /<path ou est installer notre image et container>:<url de l'image fin du path> -p 8080:3030 <nom image>

Pour persister des changements ou corriger des erreurs sans recréer l'image du container :

    - docker run -d -v /<path ou est installer notre image et container>:<url de l'image fin du path> -p 8080:3030 -v /<path ou est installer notre image et container/src>:<url de l'image fin du path du/src> <nom image>

    exemple : docker run -d -v /Users/Ubuntu/var/flutter/flutter_docker/app/etc:etc/todos -p 8080:3030 -v /Users/Ubuntu/var/flutter/flutter_docker/app/src:/app/src flutter_docker

- Après d'avoir persister tous les changements réaliser sur le container et l'image : nous pouvons re-créer l'image avec tous les nouveau changements :

docker build -t <nom-image>:v2 .

<!-- info : mettre l'image sur Dockerhub : repository public pour traduits -->

- Il faut bien tagues sont image: docker tag <id-img> <user-docker>/<nom-img>:v2

exemple : docker tag 123tagdocker456 sergioanino/flutter_docker:v2

- docker login
  add les user et le password du login :

- docker push sergioanino/flutter_docker:v2

<!-- info  : encore plus loin avec docker compose-->

<!-- :@ Docker Multi container :  -->
<!-- 52:04 min : https://www.youtube.com/watch?v=CV_Uf3Dq-EU&t=3406s&ab_channel=PeladoNerd -->

Il est nécessaire que plusieurs container courts sur la même "network"pour partager leur caractéristique.

exemple : c://flutter_docker/multi_container$ docker network create flutter_docker

1er : docker network create <nom-container-multi-container>

2e : c:\flutter_docker\multi-container$ docker run -d \

> --network flutter_docker --network-alias mysql \
> -v flutter_docker-mysql-data:/var/lib/mysql \
> -e MYSQL_ROOT_PASSWORD=secret \
> -e MYSQL_DATABASE=flutter_docker \
> mysql:5.7

Courir le network : docker exec -it <id-hashing-img-multi> mysql -p
Cela courir mysql -p à l'intérieur du container : <id_hashing-img-multi> à l'intérieur de ce container : il va utilise le binaire de mysql à l'intérieur du container pas celui de notre pc. need : password : le même que la commande en haut : secret.

show databases : à l'intérieur du container multi.

add new img : nicolaka/netshoot : va nous permette de nous connecter au network de notre environnement mysql du flutter_docker

- multi-container$ docker run -it --network <flutter_docker> nicolaka/netshoot

Par la suite il faut résoudre le problème de API du serveur local :
dig mysql - 52:43min

### Pour me connecter à mysql du network de la database du flutter_docker

docker run -dp 8080:3030 \

> --network flutter_docker \
> -e MYSQL_HOST=mysql \
> -e MYSQL_USER=root \
> -e MYSQL_PASSWORD=secret \
> -e MYSQL_DB=flutter_docker \
> flutter_docker:v2

docker ps : => voir images.

voir les logs : Voir que flutter_docker:v2 est connecter sur quelle port.

- Se connecter avec un autre mysql mais qui détient déjà tous la DB du projet et de mettre à jours les données dans les deux endroit sur la database.

docker run -dp 8080:3030 --network flutter_docker -e MYSQL_HOST=mysql -e MYSQL_USER=root -e MYSQL_PASSWORD=secret -e MYSQL_DB=flutter_docker flutter_docker:v2

<!-- :@ Docker Multi container : fin  -->

# Pour Simplifier les choses : il faut utiliser docker-compose.yml quand nous utilisons les multi-containers : Nous pouvons écrire une séries de commandes pour écrire les commandes que normalement nous devons l'écrire à la chaines manuellement.

https://docs.docker.com/compose/

8 : Créer en 1er : le file - vim docker-compose.yaml &

info : sert à combiner plusieurs container dans une seule documents de dependence_dev

<!-- info : Après d'avoir écrit notre docker-compose faire la commande suivante pour lancer les commander créer par docker compose. -->

- d : détachement.
  c:/multi-container$ docker-compose up -d

9 : Créer l'image de docker-compose.env.dev.
docker-compose up

9.1 : docker logs <l'img du docker-compose>

9.2 : mettre à terre tout la network de compose : docker-compose down

10 : Créer un build du container en env.dev
docker-compose up --build

11 : Installer un autre environnement de développement en production.
docker-compose.prod.yml up

<!-- info : Création de volume et de port dans le docker-compose -->

pour se rendre à un bash -it : docker exec -it <id-hash> bash
commande à l'intérieur d'un bash : terminal pour installer : ps
ps fax
apt-get install ps

TODOS: 10;59

<!-- Photo @lien assets -->

### **Accessing the MySQL database**

#### Création du formulaire de validation d’enregistrement & registre de navigation.

- mysql -uroot -proot octobercms
- show tables;
- exit
- Alternatively, if you have the MySQL client tools installed on your host computer, you can connect from your host machine in Windows Command Prompt: mysql --host=127.0.0.1 -uroot -proot --port=3307 octobercms. The port argument is the port number you entered in the container configuration. The connection string was displayed in the interactive script output.

---

### **How to License a Container**

#### Open in vs code : Remote-Containers: Attach to running container

- Open file :
- Écrire le mots du file comme suit : /var/www/html
- Licence.

```
php artisan project:set LICENSE-KEY
```

```
composer reinstall '*'
```

```
php artisan cache:clear
```

---

### **Section 10**

#### Backend pour le panel d'administration.

- Lien du `Backend` [backend_cafe](https://github.com/Sergioanino/backend_cafe)

| Légende de fonctionnalités | Prises en charge par l'API |
| -------------------------- | -------------------------- |
| Oui                        | :white_check_mark:         |
| Non                        | :x:                        |

1. Configuration d'un `backend`.
2. Connection à [MongoDB atlas](https://www.mongodb.com/).
3. Remplir la `base de données` avec des données.

| Fonctionnalité       | Android            | iOS                | Web                | Requête & Méthode |
| -------------------- | ------------------ | ------------------ | ------------------ | ----------------- |
| Créer user           | :white_check_mark: | :white_check_mark: | :white_check_mark: | POST              |
| Actualiser user      | :white_check_mark: | :white_check_mark: | :white_check_mark: | PUT               |
| Obtenir user paginer | :white_check_mark: | :white_check_mark: | :white_check_mark: | GET               |
| Effacer user         | :white_check_mark: | :white_check_mark: | :white_check_mark: | DEL               |
| Login                | :white_check_mark: | :white_check_mark: | :white_check_mark: | POST              |
| Google login         | :white_check_mark: | :white_check_mark: | :white_check_mark: | POST              |
| Obtenir catégories   | :white_check_mark: | :white_check_mark: | :white_check_mark: | GET               |
| Créer catégorie      | :white_check_mark: | :white_check_mark: | :white_check_mark: | POST              |
| Actualiser catégorie | :white_check_mark: | :white_check_mark: | :white_check_mark: | PUT               |
| Effacer catégorie    | :white_check_mark: | :white_check_mark: | :white_check_mark: | DEL               |
| Obtenir produits     | :white_check_mark: | :white_check_mark: | :white_check_mark: | GET               |
| Obtenir produit      | :white_check_mark: | :white_check_mark: | :white_check_mark: | GET               |
| Créer produit        | :white_check_mark: | :white_check_mark: | :white_check_mark: | POST              |
| Actualiser produit   | :white_check_mark: | :white_check_mark: | :white_check_mark: | PUT               |
| Effacer produit      | :white_check_mark: | :white_check_mark: | :white_check_mark: | DEL               |
| Recherches           | :white_check_mark: | :white_check_mark: | :white_check_mark: | GET               |
| Télécharger fichier  | :white_check_mark: | :white_check_mark: | :white_check_mark: | POST              |
| Actualiser image     | :white_check_mark: | :white_check_mark: | :white_check_mark: | PUT               |
| Obtenir image Path   | :white_check_mark: | :white_check_mark: | :white_check_mark: | GET               |
| Régénération Token   | :white_check_mark: | :white_check_mark: | :white_check_mark: | GET               |

---

### **Section 11**

#### Authentication et protection des routes.

- Nous allons utiliser le package **dio** pour lier notre _backend_ à notre authentification d'utilisateurs de notre site web.

---

### **Section 12**

#### Créer le UI de la view Catégorie et lier le Backend de notre API à la page web.

- Widget PaginatedDataTable,
- Pagination,
- Modals,
- CRUD,
- Prompts,
- DataTableSource.

---

### **Section 13**

#### Optimisation des routes pour éviter que notre application se redessine à tout moment.

- Changement du **navigateTo** --> `replaceTo`. [^2]

- Changement du **pushNamed** --> `pushReplacementNamed`. [^3]

[^2]: navigateTo garde les anciennes views en derrière plan.
[^3]: pushNames garde les anciennes views en derrière plan.

---

### **Section 14**

#### Gestion des utilisateurs de l'application.

- Trier le tableau par les en-têtes de colonne,
- Segments d'URL,
- Formulaire,
- Conception à deux colonnes,
- Valider le segment d'URL par rapport au backend,
- Traitement des erreurs.

---

### **Section 15**

#### Télécharger des fichiers dans le backend et le lier avec Cloudinary et Déploiement de la version de notre application sur le web avec Heroku.

- Cette section a pour but de télécharger des fichiers vers un backend à l'aide d'un sélecteur de fichiers.
- Nous allons également déployer notre backend et l'application Flutter vers un backend en ligne afin qu'il puisse être utilisé de n'importe où dans le monde. `#193 à #196`.
- Voir les étapes pour le [déploiement](https://docs.google.com/document/d/1W7xzfet0CbSPpZhR6251TDfYB1otAS0EMPZsCDP2m0Y/edit?usp=sharing) de l'application de production dans la `section 15`.

---

# Utilisation des outils suivant :

- [Visual Studio Code](https://code.visualstudio.com/)
- [Dart](https://dart.dev/)
- [Flutter](https://flutter.dev/)
- [Git](https://git-scm.com/)
- [GitHub](https://github.com/)
- [QuickType](https://quicktype.io/)
- [Node.js](https://nodejs.org/en/)
- [PostMan](https://www.postman.com/)
- [MongoDBAtlas](https://www.mongodb.com/atlas/database)
- [MongoDBCompass](https://www.mongodb.com/products/compass)
- [Cloudinary](https://cloudinary.com/)
- [Heroku](https://id.heroku.com/login)
