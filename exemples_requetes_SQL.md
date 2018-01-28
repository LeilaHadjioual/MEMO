**REQUETES SQL**



- sélectionner le nom de la boisson de la table boisson 
	**SELECT nomboissons FROM boissons**

- Liste des ingrédients en manque (dont la quantité est nulle)
	**SELECT nomIngredients FROM ingredients WHERE enStock = 0**

- Liste des boissons dont le libellé contient le mot « café »
	**SELECT nomboissons FROM boissons WHERE nomboissons LIKE '%café%'**

- Liste des boissons dont le prix est entre 0.30 et 0.50 euros
	**SELECT nomboissons FROM boissons WHERE prix BETWEEN '30' AND '50'**

- Liste des ventes d’aujourd’hui classées par n° décroissant
	**SELECT refcommandes, date 
	FROM commandes 
	WHERE  DATE_FORMAT(date,'%Y-%m-%d') 
	ORDER BY refcommandes DESC**

OU 	**SELECT refcommandes, date 
	FROM commandes 
	WHERE DATE(date)= CURRENT_DATE 
	ORDER BY refcommandes DESC**

- Liste des ingrédients (nom et qte nécessaire) d’une boisson donnée 
	**SELECT nomIngredients, QtéIngredient 
	FROM boissons_ingredients
	INNER JOIN ingredients 
	ON boissons_ingredients.ingredients_idingredients = 	ingredients.idingredients 
	WHERE boissons_code = 001**

ou 	**SELECT nomIngredients, QtéIngredient, nomboissons 
	FROM boissons_ingredients
	INNER JOIN ingredients ON boissons_ingredients.ingredients_idingredients = 	ingredients.idingredients 
	INNER JOIN boissons ON boissons.code = boissons_ingredients.boissons_code
	WHERE nomboissons ='cafeLong'**

- Liste des boissons disponibles (pour lesquelles les ingrédients sont dispo)
	**SELECT nomboissons FROM boissons WHERE nomboissons NOT IN(SELECT nomboissons FROM boissons
	INNER JOIN boissons_ingredients ON boissons_ingredients.boissons_code = boissons.code
	INNER JOIN ingredients ON ingredients.idingredients = boissons_ingredients.ingredients_idingredients
	WHERE enStock =0)**

- Liste des boissons vendues aujourd’hui
	**SELECT nomboissons, date 
	FROM boissons 
	INNER JOIN commandes 
	ON commandes.boissons_code = boissons.code
	WHERE date = CURDATE()**

- Prix de la dernière boisson vendue 
	**SELECT nomboissons, prix FROM boissons 
	INNER JOIN commandes 
	ON commandes.boissons_code = boissons.code 
	WHERE date = (SELECT MAX(date) FROM commandes)**

- Nombre de ventes de la boisson « CaféLong » 
	**SELECT COUNT('café long')
	FROM boissons 
	INNER JOIN commandes
	ON commandes.boissons_code = boissons.code
	WHERE nomboissons= 'café long'**

- Rajouter la boisson « Café au lait »
	**INSERT INTO boissons(code, nomboissons, prix) 
	VALUE ('006','café au lait', '70')**

- Rajouter 100 à la quantité en stock de l’ingrédient « sucre »
	**UPDATE ingredients SET enStock=enStock+100 
	WHERE idingredients=6**

- Augmenter de 0.10 euros le prix de toutes les boissons
	**UPDATE boissons SET prix = prix+10**

- Créer une nouvelle vente d’expresso avec 2 sucres
	**INSERT INTO commandes(boissons_code, date, nbsucres)
	VALUES('001','2018-01-05','2')**

- Supprimer cette vente
	**DELETE FROM commandes WHERE refcommandes=14**


- gestion des stocks, soustrait la quantité d’ingrédients du stock
	**SELECT (ingredients.enStock)-(boissons_ingredients.QtéIngredient)
	FROM ingredients 
	INNER JOIN boissons_ingredients
	ON boissons_ingredients.ingredients_idingredients= ingredients.idingredients
	INNER JOIN boissons ON boissons.code=boissons_ingredients.boissons_code
	WHERE code = 001**

- gestion stock sucre
	**UPDATE ingredients
	SET enStock = enStock -2
	WHERE idingredients = 6**