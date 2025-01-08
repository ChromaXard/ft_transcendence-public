# ft_transcendence (public version)

Bienvenue aventurier, tu te trouves sur le dépôt public du projet ft_transcendence réalisé par mon groupe et moi. 

À nous quatre, nous avons réalisé le ft_transcendence que je me suis permis de rendre public. Ce dépôt contient tout le travail que nous avons fait pour rendre le projet, mais en version légèrement modifiée pour que tout le monde puisse le lancer chez lui tant qu'il a les prérequis qui seront indiqués plus bas.

## présentation des fonctionnalités

Dans cette présentation j'essaierai d'aborder le moins de sujets techniques possibles pour que cela soit accessible à tous. Vous aurez plus de détails dans la partie technique.

### gestion des utilisateurs

Pour ce point, rien de très compliqué, on a mis en place un système de création de compte et de connexion/déconnexion comme tout bon site existant. Touchant également ce point mais non accessible à un large public (juste aux étudiants de 42), c'est l'authentification à distance, mise en place avec l'API de 42.

### le jeu

Les différents modes de jeu sont accessibles uniquement lorsque vous êtes connecté sur le site. Une fois connecté et rendu sur la page de jeu en cliquant sur `play` de la barre de navigation, vous pouvez choisir le mode de jeu que vous souhaitez, il y en a un total de 5 qui sont :

- **Single Player** : c'est le mode classique chez nous, le pong, contre un adversaire contrôlé par IA que vous pouvez essayer de battre en contrôlant votre barre avec les touches W et S de votre clavier. Des modificateurs sont également disponibles si vous le souhaitez.
- **Multi Player (Local) et Multi 4 Player (Local) : sont le même mode que `Single Player` à la différence qu'il n'y a plus l'IA. En Multi Player, le second joueur contrôle sa barre à l'aide des flèches haut et bas du clavier. Pour le Multi 4 player, les touches sont : W/S pour le joueur 1 G/B pour le joueur 2, les flèches haut et bas pour le joueur 3 et les touches 6/3 du pavé numérique pour le joueur 4.
- **Multi Player (Remote) : même chose que les modes précédents à peu près, sauf qu'il n'y a plus les modificateurs et votre adversaire est contrôlé par une personne distante ayant également choisi de jouer dans ce mode. Vous contrôlez votre barre à l'aide de W/S.
- **Tournament : c'est un tournoi, comme son nom l'indique, de 4 joueurs qui vont s'affronter dans des parties de `Multi Player (Remote)`

### Le profil

La page profil (`Profile`) est une page simple regroupant toutes les informations de votre profil comme votre Username (plus communément appelé pseudo), votre email et votre photo de profil. Vous avez également la possibilité de changer ces informations en utilisant le formulaire donné par le bouton `change informations`

### Les amis

Nous avons créé notre petit système pour avoir des amis sur la page `Friend` de notre site. Sur cette page, nous pouvons voir notre liste d'amis, accéder à leur profil et voir leur statut (s'ils sont hors ligne, en ligne ou en train de jouer). Vous pouvez également en ajouter, en supprimer ou accepter une demande d'ami que vous avez reçue grâce aux boutons présents sur la page.

### L'historique

Votre page d'historique n'est disponible qu'à partir du moment où vous avez au moins terminé une partie. Une fois cette condition remplie, vous pouvez vous y rendre en cliquant sur `History` de la barre de navigation. Cela vous donne votre historique avec différents moyens visuels de voir les parties que vous avez faites. Vous disposez également de filtres que vous pouvez mettre à votre guise pour analyser certaines parties.


### Le chat

Passons à la dernière page de notre site, le chat (pas l'animal mais la fonctionnalité pour discuter à l'écrit 👀).

Voici une petite explication des fonctionnalités présentes : 

- **join channel** : cette partie vous permet de rejoindre un canal public du nom que vous souhaitez
- **Chatting section** : comme son nom l'indique, c'est la zone où vous allez pouvoir discuter avec les autres. En premier, vous avez une partie pour sélectionner le canal sur lequel vous voulez parler. Ensuite, vous avez deux colonnes, celle de gauche contenant tous les pseudos des personnes connectées sur le canal sélectionné, et celle de droite contient les messages qui ont été envoyés sur le canal. La dernière ligne de la partie chatting section est celle qui vous permet d'envoyer des messages, clear les messages du canal actuellement sélectionné ou quitter le canal sélectionné.
- **user filter** : c'est la petite partie qui vous permet d'appliquer les différents filtres sur le tableau qui est juste en dessous.
- **User tab** : cette partie contient le tableau avec tous les utilisateurs enregistrés sur le site, ce dernier affiche également les informations le concernant à votre niveau (si vous l'avez en tant qu'ami, s'il est muté, etc...), et d'autres informations comme son statut, la possibilité de lui envoyer un message privé ou de lancer une partie avec lui.


## détails techniques

Dans cette partie, je vais d'abord vous expliquer comment lancer le serveur de votre côté avant de vous dire les différents langages et frameworks que l'on a utilisés.

### prérequis pour le lancement

Pour pouvoir lancer le serveur, il faut une petite liste de programmes qui ne sont pas forcément installés, voici la liste des applications :

- docker
- docker-compose (si votre version de docker est inférieure à 20.10)
- python
- Make
- curl
- git (vous permettant de récupérer rapidement les fichiers du dépôt)

### lancer le serveur

Pour lancer le serveur c'est assez simple, voici les étapes : 

1. **Téléchargement** :
    
    clonez ce dépôt puis rentrez dans le dossier correspondant.

2. **Compilation + lancement** :

    Si vous avez installé correctement les prérequis indiqué vous avez juste executer la commande ci-dessous : 
    ```bash
    make 
    ```
    après quelques instant vous devriez avoir le texte suivant s'afficher.
    
    `Le serveur est prêt !`
    
    `Vous pouvez accéder à l'application via https://<ip de votre machine>:4433`

    indiquant que le serveur est prêt et accessible par toutes personne étant sur votre réseau

3. **connexion au site** :

    Pour vous connecter au site, il vous suffit d'ouvrir un navigateur et de vous rendre sur le lien indiqué par la denière ligne de la compilation

    exemple :
    ```
    https://192.168.1.24:4433/
    ```

#### Annexe : 

Liste de toutes les commandes du Makefile :

- **all (commande appelé par défaut lors d'un make)** : s'occupe de lancer les différents dockerfile (backend (django), base de données et de cache (postgreSQL), serveur web (nginx))
- **build** : build les dockerfile nécessaire
- **up** : lance le serveur
- **down** : arrete le serveur
- **logs** : affiche les derniers logs du serveur
- **logs-f** : affiche les logs du serveur "en direct"
- **clear** : arrete et supprime les données du serveur
- **check-env** : vérifie si le fichier d'environnement peut être créé
- **update_env** : créé le fichier d'environement adapté a votre machine
- **create-path** : créer les dossiers nécessaire pour le lancement du serveur
- **wait_server** : execute une boucle qui sera présente tant que le serveur ne retourne pas un code 200 (permet de savoir quand le serveur est réellement prêt a recevoir une connexion)
- **re** : execute les commandes clear et all

Liste de langages et frameworks :
    
- **backend** :
    
    - *frameworks* : 

        - Django
    
    - *Langages* :

        - Python
        - SQL

- **frontend** :
    
    - *toolkit* : 

        - Bootstrap
    
    - *Langages* :

        - html
        - css
        - javascript
## 🤝 Contribution

Ce projet a été réalisé avec les personnes suivantes :

- [Quentin Denizart](https://github.com/LaDeniseDe42)  
- [Alexandre Herrmann](https://github.com/alexandre6795)  
- [Damla Erblang](https://github.com/iamdamla)  
- [Axel Kastler](https://github.com/ChromaXard)






