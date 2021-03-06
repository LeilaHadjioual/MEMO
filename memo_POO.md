﻿#MEMO POO

faire de son site un ensemble d'objets qui interagissent entre eux.  
En d'autres termes : tout est objet  

**Objet**  
    
    programme autosuffisant  
    
**classe**   

	contiennent la définition ds objets.  
	c’est le plan de fabrication d’un objet.  
	On peut s’en servir autant qu’on veut.  
	Tout objet issu de classe possède les variables et fonctions.  
	ex:(moule)

**Instance**  

	se servir d’une classe pour créer un objet  
	(une instance est un objet)

**Instanciation**  

    créer un objet  
        ex : $t = new triangle();  
     $t est une instance  
     new : terme qui appelle l'objet  
     triangle() : objet  
     
     $t est une instance de l'objet triangle    

**attribut :**   

    variables d'une classe, peut être publique, privée ou protégée

**méthode :**   
    
        fonction de classe

**encapsulation**  

	masquer le code à l’utilisateur.  
	l’utilisateur invoque les méthodes en ignorant les attributs.

**Visibilité d’un attribut ou méthode**  
	
	inutile de masquer les méthodes
		- public, on y a accès depuis n’importe ou. visible par toutes les méthodes, classes...
		- privé: accès depuis l’intérieur de la classe. on ne veut pas modifier même par héritage.  
		        connu de sa propre classe seulement, inaccessible par une autre classe.  
		- protected : accessible par sa propre classe et classe fille.
	
**syntaxe attribut privé-public-protected:**  
 
	private $_force;
	public $force;
	protected  : idem private à l'exception que toute classe fille aura accès aux éléments protégés  
	ex : protected $attributProtege;

**getter ou accesseurs**  
	
	pour accéder à un attribut
	portent le même nom que l'attribut dont elles renvoient la valeur 
	
**setter ou mutateurs**  
	
	Modifier la valeur d'un attribut 
	syntaxe: public function setExperience($experience)
  
**constructeur**  

	méthode appelée lors de la construction d'un objet (pendant l'instanciation).   
	il a toujours le nom de la classe et est appelé par défaut.  
	possible d'avoir plusieur contructeurs dans une classe mais pas avec le meme nbr de paramètre sinon ne saura pas lequel appelé pendant l'instanciation.
	sert à construire l'objet, modifie les attributs
	utile si des attributs doivent être initialisés ou qu'une connexion à la BDD doit être faite.  
	il est exécuté dès la création de l'objet et aucune valeur ne doit être retournée.  
	syntaxe: public function __construct( $force, $degats ) {  }

**constante**  

	Une constante est une sorte d'attribut appartenant à la classe dont la valeur ne change jamais.  
	syntaxe: const FORCE_PETITE = 20; pas de $

**méthode statique**  
	
	les méthodes statiques sont des méthodes qui sont faites pour agir sur une classe et non sur un objet.  
	aucun $this dans la méthode car $this est un paramètre implicite et possible que sur méthode appelées sur un objet.  
	Syntaxe: public static function parler(  )

*exemple  :*  

		class King{  
			public static function proclaim(){  
				echo "A kingly proclamation !";  
			}
		}  
		echo King::proclaim();


**attributs statiques**  

	attribut statique appartient à la classe et non à un objet.  
	Tous les objets auront accès à cet attribut et cet attribut aura la même valeur pour tous les objets.  
	on accède à un attribut statique avec self :  
	  self::$_compteur++ 
	   
	syntaxe : private static $_texteADire='hhhh !';

**héritage**  
	
	c'est qu'on dit qu'une classe B hérite d'une classe A.  
	La classe A est donc considérée comme la classe mère et la classe B est considérée comme la classe fille  
	
	syntaxe : class Magicien extends Personnage{ }

**hydratation**  

	assigner des valeurs aux attributs de l’objet  
		ex : private $_id;  
		     public function hydrate($donnees){}  
		     public function id() {  
		        return $this->_id;   
		     }
		     
**classes finales (à éviter)**  

	Si une classe est finale, vous ne pourrez pas créer de classe fille héritant de cette classe.  
	
	Syntaxe : final class Guerrier extends Personnage{ }

**méthode finale**  

	Si vous déclarez une méthode finale, toute classe fille de la classe comportant cette méthode finale héritera de cette méthode mais ne pourra la redéfinir  
	
	syntaxe: final public function recevoirDegats(){ }

**cloner**  

    dupliquer  
        ex : $t3 = new triangle();
            $t3a = $t3 ;  
     
**surcharger**

    redefinir une méthode dans une classe fille. remplace la methode de la classe parent  
    ex : draw ( class figure : function draw //sans rien, class polygone : function draw //définit, class triangle et rectangle // draw hérité, class cercle: draw definit)  

**abstrait**  

    classe abstraite pour ne pas pouvoir y accéder. aucune possiblité de l'instancier.  
        ex : abstract class figure    


