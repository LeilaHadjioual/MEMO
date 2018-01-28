**Procédure d'installation serveur**



Pour se connecter : 
	ouvrir bash
	taper root@ 163.172.183.212 
	un message s'affiche : répondre yes
	Entrer le mot de passe par défaut qui est "azerty".



**Installation DEBIAN 9**

- **Etape 1** : Verifier que la distribution est à jour

	apt-get update && apt-get upgrade 


- **Etape 2** : installation de mysql 

	apt-get install mysql-server mysql-client
	*Création d'un mot de passe*


- **Etape 3** : installation du serveur web apache 2 

	apt-get install apache2 apache2-doc


- **Etape 4** : installation de PHP7 

	apt-get install php7 php7-mysql libapache2-mod-php7


- **Etape 5** : installation de PHP myadmin

	apt-get install phpmyadmin
	*Creation d'un mot de passe pour php myadmin*


- **Etape 6** : restart du serveur web

	service apache2 restart


- **Etape 7**: ouverture de la page "Debian default page"

	Dans un navigateur internet, saisir dans l'url l'adresse IP du serveur web.
	La page de debian devrait s'afficher avec "It works!".
	Cette page nous donne le chemin d'accès dans lequel on va pouvoir tester si le serveur fonctionne bien et les différentes versions installées.


-**Etape 8** : Changer de répertoire pour être dans HTML

	aller dans le répertoire HTML avec les commandes CD, 
	on devrait avoir un seul fichier "index.HTML" dans le dossier HTML


- **Etape 8** : créer le fichier Test.php

	nano test.php
	Création d'un fichier Test.php dans le répertoire HTML et ajouter  "<?php phpinfo(); ?>"
	*La commande nano crée le fichier s'il n'existe pas, mais permet aussi de lire le fichier ou de le modifier s'il est déjà crée. 
	(CTRL X pour sortir du fichier ).*
	
- **Etape 9** : afficher les versions de logiciel sur le navigateur

	AdresseIP du serveur web/test.php

	exemple : 152.187.251.132/test.php

*si des fenêtres s'affiche taper yes*
	


**Notre serveur est installé et configuré, prêt à fonctionner**




**IMPORTER LE PROJET**

	
*Importation du code depuis git hub* 

	1.se connecter au serveur
		ssh root@163.172.183.212
		mdp : darth_sidious (par défaut azerty mais modif en faisant la commande passwd)

	2.si erreur de connection : warning remote
		faire rm/p/ssh/know_hosts (ce chemin est précisé dans l'erreur) et retenter la connection

	3.git clone https://github.com/campus-digital-grenoble/MachinaCafe_ilot3.git

	4.créer un utilisateur 
		create user 'nom'@localhost' identified by 'motdepasse'

	5.Administrer des droits à un user
		grant all on machin_coffee.* to 'vader'@'localhost';

	6.créer une base de données
		create database nombdd

	7.vérifier si bdd créer
		show databases;

	8.lien entre entre fichier serveur et dossiers		
		ln -s/usr/share/phpmyadmin phpmyadmin
*le fichier phpmyadmin se retrouve dans le dossier html (c'est une copie du fichier phpmyadmin liée au fichier phpmyadmin, permet de l'avoir à jour directement).*

	9. Se connecter à phpmyadmin 
		mysql-u root

	10. si ouverture de la bdd via serveur distant
		user : phpmyadmin ou nom user créé
		mdp : si inchangé le mdp de la bdd

	11. importer la bdd de phpmyadmin en local et insérer dans la bdd de phpmyadmin distant (entrer dans la base de données créée au préalable)

	12. modifier le contenu d'un fichier
		nano var/www/html/machineacafe
		modifier le pdo – dbname et vérifier qu'il est nommé de la meme facon que la bdd créer sur serveur distant

**si erreur**
	var/log/apache2
	cat error.log
		verifier les erreurs, regarder le nom du fichier en question et le n°de ligne	
	retourner dans le dossier machineacafe
	nano fonctions.php
	modifier le fichier
	ctrl o
	entrée
	ctrl x
	mettre à jour : service apache2 restart
	
