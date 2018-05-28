## SYMFONY 3.4.9 
___
### dossier github : my_project_symfony
___
ressources cours :   
https://symfony.com/doc/3.4/index.html  
https://symfony.com/    

*bundle :* https://openclassrooms.com/courses/developpez-votre-site-web-avec-le-framework-symfony/symfony-un-framework-php     

 d*octrine, orm, entity*: https://symfony.com/doc/3.4/doctrine.html  https://openclassrooms.com/courses/developpez-votre-site-web-avec-le-framework-symfony/la-couche-metier-les-entites-1   
 https://symfony.com/doc/3.4/doctrine.html#relationships-and-associations      https://symfony.com/doc/3.4/doctrine/associations.html   

*formulaire:*
https://symfony.com/doc/3.4/forms.html    
https://openclassrooms.com/courses/developpez-votre-site-web-avec-le-framework-symfony/creer-des-formulaires-avec-symfony

*authentification:*  
https://symfony.com/doc/3.4/reference/configuration/security.html   
https://openclassrooms.com/courses/developpez-votre-site-web-avec-le-framework-symfony/securite-et-gestion-des-utilisateurs-1   

*autres ressources:*
https://knpuniversity.com/screencast/symfony3/hello-twig#play  
https://twig.symfony.com/doc/2.x/  
http://knpbundles.com/

----
### **INSTALLER SYMFONY**

**installer PHP 7.1**   
(vérifier installation cmd php-v, la version doit être supérieure à 5.4)

        dossier zip sur site php  
        extraire le dossier sous C:  
        modifier le path (nouveau)  

**installer composer**  

     composer.exe  

**créer un nouveau projet symfony avec composer** (éviter l'installation avec .phar)

    composer create-project symfony/framework-standard-edition nom_du_projet    

*possibilité de préciser la version, ajouter "3.4.9" au nom du projet, répondre ok (si BDD, préciser le nom)*

**Lancer le projet**  

    php bin/console server:run

*si problème : composer update*

NB : php bin/console security:check, cmd à faire souvent pour vérifier si les dépendances sont sécurisées

----
----
----
**1- STRUCTURE DU PROJET**

app/  
Contient des choses comme la configuration et les modèles. Fondamentalement, tout ce qui n'est pas du code PHP va ici.  

src/  
Votre code PHP vit ici.  
99% du temps, vous travaillerez dans src/(fichiers PHP) ou app/(tout le reste). Pendant que vous continuez à lire, vous apprendrez ce qui peut être fait à l'intérieur de chacun d'eux.  

bin/  
Le bin/consolefichier célèbre vit ici (et d'autres fichiers exécutables moins importants).  

tests/  
Les tests automatisés (par exemple les tests unitaires) pour votre application vivent ici.  

var/  
C'est là que sont stockés les fichiers créés automatiquement, comme les fichiers cache ( var/cache/), logs ( var/logs/) et sessions ( var/sessions/).  

vendor/  
Les bibliothèques tierces (c.-à-d. «Vendor») vivent ici! Ceux-ci sont téléchargés via le gestionnaire de paquets Composer .  

web/  
Ceci est la racine du document pour votre projet: mettez tous les fichiers accessibles au public ici (par exemple CSS, JS et images).  

----

**2 - ROUTAGE**

Plusieurs méthodes : annotations, YML, XML

**2.1 - annotations**

EXEMPLE:  

    // src/AppBundle/Controller/BlogController.php

    namespace AppBundle\Controller;

    use Symfony\Bundle\FrameworkBundle\Controller\Controller;
    use Symfony\Component\Routing\Annotation\Route;

    class BlogController extends Controller
    {
        /**
        * affiche la liste des blogs
        *
        * @Route("/blog", name="blog_list")
        */
        public function listAction()
        {
            // ...
        }  

**2.2 - YML, XML ou PHP**

la valeur "defaults" est une clé spéciale qui indique à Symfony quel contrôleur doit être exécuté lorsqu'une URL correspond à cette route  

*exemple .yml:*

        # app/config/routing.yml
        blog_list:
            path:     /blog
            defaults: { _controller: AppBundle:Blog:list }

        blog_show:
            path:     /blog/{slug}
            defaults: { _controller: AppBundle:Blog:show }

*exemple .xml :*

    <!-- app/config/routing.xml -->
    <?xml version="1.0" encoding="UTF-8" ?>
    <routes xmlns="http://symfony.com/schema/routing"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://symfony.com/schema/routing
            http://symfony.com/schema/routing/routing-1.0.xsd">

        <route id="blog_list" path="/blog">
            <default key="_controller">AppBundle:Blog:list</default>
        </route>

        <route id="blog_show" path="/blog/{slug}">
            <default key="_controller">AppBundle:Blog:show</default>
        </route>
    </routes>  


*exemple .php:*  

            // app/config/routing.php
        use Symfony\Component\Routing\RouteCollection;
        use Symfony\Component\Routing\Route;

        $routes = new RouteCollection();
        $routes->add('blog_list', new Route('/blog', array(
            '_controller' => 'AppBundle:Blog:list',
        )));
        $routes->add('blog_show', new Route('/blog/{slug}', array(
            '_controller' => 'AppBundle:Blog:show',
        )));

        return $routes;

----
**3 - BUNDLE**  

déf : comme un plugin, toutes les fonctionnalités d'une appli proviennent d'un bundle.  
Même arborescence que l'App mais avec ses propres fichiers.

**3.1- CREER UN BUNDLE**


    php bin/console generate:bundle  


répondre aux questions:   
    ->partager le bundle : oui ou non    
    ->bundlename: NomBundle  
    ->src : entrée  
    ->format : annotations  

si erreur avec composer.json, modifier le json :

        "autoload"
            psr-4 :
                "\\InscriptionBundle\\":"src/InscriptionBundle"

en ligne de commande faire : 

        composer dump-autoload  

modifier la vue du controller : '@Inscription/Default/index.html.twig"

*NB : vérifier dans le fichier config.yml et AppKernel.php si présence du bundle créé*  

*pour afficher la barre de debug, il suffit d'ajouter les balises html et body dans la vue (ou extends une vue ayant ces balises)*  

----
**4- BDD - DOCTRINE EST L'ORM QUI FACILITE L'INTERACTION AVEC LA BDD**

- Pendant la création de l'appli, si aucun nom de BDD soumis, configurer le fichier parametre.yml 

    app/config/parametre.yml   


------
------
------

**AUTHENTIFICATION**  
L'authentification est le processus qui va définir qui vous êtes, en tant que visiteur. Le FIREWALL gère l'authentification dans Symfony

**AUTORISATION**  
processus qui va déterminer si vous avez le droit d'accéder à la ressource (la page) demandée. Il agit donc après le firewall. Ce qui gère l'autorisation dans Symfony s'appelle l'access control.

## **I/ AUTHENTIFICATION**

**1- configurer le fichier app/config/security.yml**  

    security:
        encoders:
            Symfony\Component\Security\Core\User\User: plaintext

        role_hierarchy:
            ROLE_ADMIN:       ROLE_USER
            ROLE_SUPER_ADMIN: [ROLE_USER, ROLE_ADMIN, ROLE_ALLOWED_TO_SWITCH]

        providers:
            in_memory:                      //fournisseur d'utilisateurs pour le pare-feu
            memory:
                users:
                user:  { password: userpass, roles: [ 'ROLE_USER' ] }
                admin: { password: adminpass, roles: [ 'ROLE_ADMIN' ] }

        firewalls:
            dev:
            pattern: ^/(_(profiler|wdt)|css|images|js)/
            security: false

        access_control:
            #- { path: ^/login, roles: IS_AUTHENTICATED_ANONYMOUSLY, requires_channel: https }


**2- Mettre en place un parefeu**  

*2-1 Créer le pare feu*

    security:
        firewalls:
            dev:
                pattern: ^/(_(profiler|wdt)|css|images|js)/
                security: false
            main:                                   //nom du pare-feu
                pattern:   ^/                       //est un masque d'URL,toutes les URL commençant par « / » sont protégées par ce pare-feu
                anonymous: true                     //accepte les utilisateurs anonymes  


*2-2 Définir une méthode d'authentification pour le pare-feu*  

méthode d'authentification par formulaire, configuration fichier security.yml: 

        main:
            pattern:      ^/
            anonymous:    true
            form_login:                     //méthode d'authentification utilisée pour ce pare-feu
                login_path: login           //correspond à la route du formulaire de connexion
                check_path: login_check     //correspond à la route de validation du formulaire de connexion, c'est sur cette route que seront vérifiés les identifiants renseignés par l'utilisateur sur le formulaire précédent
            logout:                         //rend possible la déconnexion
                path:       logout          //nom route à laquelle le visiteur doit aller pour être déconnecté
                target:     login           //nom route vers laquelle sera redirigé le visiteur après sa déconnexion  


*2-3 définir les routes d'authentification, configurer le fichier routing.yml :*  


        login:
            path: /login
            defaults:
                _controller: UserBundle:Security:login

        login_check:
            path: /login_check

        logout:
            path: /logout                         
            
    //pas de controller sur les routes logincheck et logout car Symfony va attraper tout seul les requêtes sur ces routes grâce au gestionnaire d'évènements  


*2-4 créer le bundle de sécurité :*

    php bin/console generate:bundle  

supprimer les fichiers ci-dessous car inutile  :
   
    Le contrôleurController/DefaultController.php;  
    Son répertoire de testsTests/Controller;  
    Son répertoire de vuesResources/views/Default;  
    Le fichier de routesResources/config/routing.yml ;  
    La ligne d'import (oc_user) du fichier de routes dans le fichier app/config/routing.yml  


créer le la fonction "loginAction" du controller  
créer la vue twig  
tester la connection (login : user / mdp: userpass ou login:admin / mdp : adminpass)  

## **II/ AUTORISATION**  


*1-configurer le fichier security.yml*  

On définit ici uniquement la hiérarchie entre les rôles, et non l'exhaustivité des rôles. Ainsi, on pourrait tout à fait avoir un rôle "ROLE_TRUC" dans notre application, mais que les administrateurs n'héritent pas.  

        security:
            role_hierarchy:
                # Un admin hérite des droits d'auteur et de modérateur
                ROLE_ADMIN:       [ROLE_AUTEUR, ROLE_MODERATEUR]
                # On garde ce rôle superadmin, il nous resservira par la suite
                ROLE_SUPER_ADMIN: [ROLE_ADMIN, ROLE_ALLOWED_TO_SWITCH]

*1-2 Tester les rôles*  

Il existe quatre méthodes pour faire ce test : les annotations, le service security.authorization_checker", Twig, et les contrôles d'accès

1-2-1 Utiliser directement le service "security.authorization_checker "

        class AdvertController extends Controller
        {
            public function addAction(Request $request)
            {
                // On vérifie que l'utilisateur dispose bien du rôle ROLE_AUTEUR
                if (!$this->get('security.authorization_checker')->isGranted('ROLE_AUTEUR')) { 

                // Sinon on déclenche une exception « Accès interdit »
                throw new AccessDeniedException('Accès limité aux auteurs.');
                }
                // Ici l'utilisateur a les droits suffisant,
                // on peut ajouter une annonce
            }
        }


1-2-2 Utiliser les annotations dans un contrôleur  

La méthode de l'annotation permet de sécuriser une méthode de contrôleur


    use Sensio\Bundle\FrameworkExtraBundle\Configuration\Security;

    class AdvertController extends Controller
    {
        /**
        * @Security("has_role('ROLE_AUTEUR')")
        */
        public function addAction(Request $request)
        {
            // Plus besoin du if avec le security.context, l'annotation s'occupe de tout !
            // Dans cette méthode, vous êtes sûrs que l'utilisateur courant dispose du rôle ROLE_AUTEUR
        }
    }

si utilisateur a 2 rôles

    /**
    * @Security("has_role('ROLE_AUTEUR') and has_role('ROLE_AUTRE')")
    * /


1-2-3 Depuis une vue Twig    

La méthode avec Twig permet de sécuriser l'affichage

    {# On n'affiche le lien « Ajouter une annonce » qu'aux auteurs (et admins, qui héritent du rôle auteur) #}
        {% if is_granted('ROLE_AUTEUR') %}
            <li><a href="{{ path('oc_platform_add') }}">Ajouter une annonce</a></li>
        {% endif %}  


1-2-4 Utiliser les contrôles d'accès    

La méthode des contrôles d'accès permet de sécuriser des URL.

    // app/config/security.yml

        security:
            access_control:
                - { path: ^/admin, roles: ROLE_ADMIN }


## **III/ Utiliser des utilisateurs de la base de données**  

*1- créer une entité User dans le bundle de sécurité*  

        php bin/console doctrine:generate:entity

avec les champs :  

    userName : string, unique
    password
    salt (pour encodage des mdp)
    roles : array  

ajouter la méthodeeraseCredentials(), vide pour l'instant mais obligatoire de par l'interface UserInterface:

     public function eraseCredentials() { }


Et pour que Symfony l'accepte comme classe utilisateur de la couche sécurité, il faut qu'on implémente l'interfaceUserInterface  

    class User implements UserInterface

vérifer ajout de :

    use Symfony\Component\Security\Core\User\UserInterface;

mettre à jour la BDD

    php bin/console doctrine:schema:update
    php bin/console doctrine:schema:update --dump-sql
    php bin/console doctrine:schema:update --force  


*2- Créer des utilisateurs tests* 

Utiliser les fixtures : création d'utilisateurs tests

créer le dossier DataFixtures et orm  
créer la class LoadUser    

    use Doctrine\Common\DataFixtures\FixtureInterface;
    use Doctrine\Common\Persistence\ObjectManager;
    use UserBundle\Entity\User;  

    class LoadUser implements FixtureInterface
    {
        public function load(ObjectManager $manager)
        {
            // Les noms d'utilisateurs à créer
            $listNames = array('Alexandre', 'Marine', 'Anna');

            foreach ($listNames as $name) {
                // On crée l'utilisateur
                $user = new User;

                // Le nom d'utilisateur et le mot de passe sont identiques pour l'instant
                $user->setUserName($name);
                $user->setPassword($name);

                // On ne se sert pas du salt pour l'instant
                $user->setSalt('');
                // On définit uniquement le role ROLE_USER qui est le role de base
                $user->setRoles(array('ROLE_USER'));

                // On le persiste
                $manager->persist($user);
            }

            // On déclenche l'enregistrement
            $manager->flush();
        }
    }

php bin/console doctrine:fixtures:load

si la commande ne marche pas, ajouter dans fichier AppKernel.php : 

    if
     $bundles[] = new Doctrine\Bundle\FixturesBundle\DoctrineFixturesBundle();  


