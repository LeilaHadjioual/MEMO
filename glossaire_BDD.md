
**BASE DE DONNEES**



**SGBD** : système de gestion de base de données qui manipule les fichiers, permet une requête et renvoie un résultat.  
	- Moteur SQL (réalise des manipulations sur les fichiers, lit et retranscrit), 
	- authentification/catalogue (information utilisateur, droit accès),
	- processeur de requête (permet de comprendre le langage, prend la requête, récupère l’info et retourne le résultat),
	- langage de requête SQL (langage que le SGBD peut comprendre)  


**DICTIONNAIRE DE DONNÉES** (catalogue, bibliothèque) : inventaire des données à stocker  


**BANQUE DE DONNÉES** : ensemble de plusieurs bases de données  


**BDD** : ensemble de données, correspond au fichier principal  


**TABLE** : tableau composé de colonnes et lignes (ex : feuille excel), regroupe plusieurs attributs  


**LIGNE D’ENREGISTREMENT** (ligne, occurrence d’entité) : données.  


**ENTITÉS** : regroupement de données élémentaires similaires  (ex : entité =client, attribut=nom, prénom)  


**ATTRIBUTS** (champ, colonne): caractéristique de l’entité (ex : nom, prénom, DDN,etc...)  


**ASSOCIATION** : permet de relier plusieurs entités  


**SQL** : langage de requête, permet de créer, lire, modifier, supprimer (CRUD create, read, update, delete)  


**CLÉ PRIMAIRE** : attribut correspondant à un identifiant, elle est unique.  

**CLÉ ÉTRANGÈRE** : pointe un identifiant/clé extérieur venant d’une autre table et permet de relier ces 2 tables (possibilité de doublons).  


**Cardinalité** : interagit avec les identifiants/clés  
	plusieurs possibilités (min , max) : 	0 , 1 		0 , n		1 , 1		1 , n  
0 = aucun  
1 = une fois  
n = plusieurs fois  


**MCD (modèle conceptuel de données)** : permet de bâtir la BDD, schéma qui regroupe les entités, attributs, cardinalités  


**SYNTAXE SQL**  
pour créer une base :  
	CREATE (créer)  
	DROP (supprimer)  
	ALTER(modifier)  

pour manipuler les données :  
	SELECT (récupérer)  
	INSERT (insérer)  
	UPDATE (modifier)  
	DELETE (supprimer)  