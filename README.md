# RUBY ON RAILS POUR LES NULS :stuck_out_tongue:
Description des concepts essentiels pour Ruby on Rails

### Table des Matières

1. [La différence entre un site statique et un site dynamique](#stadyn)
2. [Le MVC: Model View Controller](#mvc)
3. [Les routes](#routes)
4. [Les Bases de Données](#bdd)
5. [GET / POST](#getpost)
6. [Le concept de migration](#migrate)
7. [Les relations entre les models des BDD](#models)
8. [Les fonctions du CRUD](#crud)

### <a name="stadyn"></a>La différence entre un site statique et un site dynamique
Un **_site web statique_** est une page dont le contenu ne varie pas en fonction de l'internaute et des caractéristiques de sa demande. Le lien renverra toujours **_le même contenu_** quelque soit l'utilisateur ou le nombre de visites. Voici un [**exemple**](http://motherfuckingwebsite.com/) de site statique.

A l'inverse, une **_page web dynamique_** est générée à la demande et **_son contenu varie_** en fonction des caractéristiques de la demande (heure, adresse IP de l'ordinateur du demandeur, formulaire rempli par le demandeur, etc..). L'URL d'une page peut donc renvoyer un affichage différent selon l'internaute. (ex: mon fil d'actualités Facebook vs. celui de mon voisin).

![Schéma site statique et dynamique](http://www.linformatique.org/wp-content/uploads/2014/07/creation-web-opter-site-statique-dynamique.jpg?x93808)

D'après ces deux définitions, on peut déduire que la différence majeure entre un site statique et un site dynamique est le fait que le **premier affiche toujours le même contenu** et le **second varie en fonction de la demande**.

Attention: cela ne signifie pas qu'un site statique ne peut pas contenir d'animations (GIF, vidéos, musiques). Il le peut mais ces animations resteront les mêmes pour tous les visiteurs du site.

### <a name="mvc"></a>Le MVC: Model View Controller
Le modèle-vue-contrôleur est une architecture composée de trois modules ayant chacun un rôle spécifique :
* Un modèle (Model) contient les fichiers permettant d'aller récupérer les données à afficher dans la BDD ;
* Une vue (View) contient le code HTML qui détermine l'interface graphique et la présentation des données à l'utilisateur ;
* Un contrôleur (Controller) contient le code logique faisant la passerelle entre le modèle, la vue et les actions de l'utilisateur.

![Schéma du MVC](https://i.pinimg.com/564x/f1/45/fa/f145fa01dd8cadd28537194de00cda59.jpg)

On retrouve cette structure dans chaque application Rails, dans un dossier app/, où nous allons retrouver des sous-dossiers models, views, controllers.

##### Model
C'est dans ce fichier que seront stockées toutes les requêtes vers votre Base de Données.

##### View
C'est ici que se trouve le code HTML de votre site web. C'est donc cette partie qui va s'occuper de mettre les données récupérées de la BDD sous forme HTML.

##### Controller
Lorsqu'un utilisateur se trouve face à son navigateur, il adresse ses requêtes au Controller. Chaque requête renvoie vers une action (fonction) dans le Controller. Chaque action va ensuite transmettre une requête vers le Model. Après réponse du Model, les données vont être envoyées vers le View pour la mise en forme. Pour chaque action du Controller il existera donc un fichier View qui contiendra le code HTML correspondant.

### <a name="routes"></a>Les routes
Les routes permettent d’**interpréter les URL** et d’**orienter vers les bonnes actions le controller**. On peut les configurer dans le fichier config/routes.rb.

Les routes d'un site sont représentées dans l'URL avec des '/' comme pour les chemins en terminal.

Ex: J'ai crée www.mon-site.fr et je dispose de 3 links: Accueil, Historique, Contact.

Si je tape dans la barre d'adresse de mon navigateur www.mon-site.fr/accueil, cela me renverra vers la page Accueil (en supposant que j'ai crée un fichier HTML correspondant).

Le principe des routes pour Rails consiste à rediriger un utilisateur vers l'action correspondante dans le Controller (puis ensuite refaire le parcours MVC).

Pour plus d'informations vous pouvez lire la doc rails sur les [routes](http://guides.rubyonrails.org/routing.html).

### <a name="bdd"></a>Les Bases de Données
Une base de données permet de stocker et de retrouver l'intégralité des données brutes ou d'informations en rapport avec un thème ou une activité. Ex: Amazon contient une énorme BDD qui contient les infos de chaque utilisateurs (noms, prénoms, ville, moyen de paiement, etc.), les infos des articles à vendre (nom, prix, descriptif, etc.), etc.

Plus basiquement, une BDD ressemble à un fichier excel (.xlsx) dans lequel un Id est par exemple relié à un string. Cette base de données est le modèle qui est utilisé pour les sites web dynamiques.

Rails permet de créer plusieurs fichiers qui peuvent nous montrer l'état des lieux des bases de données grâce à la commande `rails db:migrate`.

### <a name="getpost"></a>GET / POST

##### GET
Sert à appeler la méthode du Controller lié à l'URL rentrée par l'utilisateur.

Ex: l'utilisateur tape dans son navigateur monsite.com/welcome  => il sera renvoyé vers la méthode index situé dans le Controller appelé 'welcome'.
```ruby
Rails.application.routes.draw do
    get 'welcome', to: 'welcome#index'
end
```

##### POST
Sert à soumettre un formulaire.

Ex: un site web affiche toutes les marques de bières dans le monde. Si on souhaite ajouter une nouvelle marque on passera par la méthode POST qui elle même renvoie vers une méthode Create dans le Controller.

### <a name="migrate"></a>Le concept de migration
Les migrations permettent de **_faire évoluer la structure de la base de données_**. C'est une **simplification du language** pour rendre les modifications plus faciles et plus rapides.

La commande de base utilisée dans Rails est *db:migrate*.

Pour en savoir plus, vous pouvez regarder le tuto de Graphikart :

[![Apprendre Ruby on Rails : Les Migrations](https://img.youtube.com/vi/LBtCqTeJvfg/0.jpg)](https://www.youtube.com/watch?v=LBtCqTeJvfg)

### <a name="models"></a>Les relations entre les models des BDD
[Wikipedia][1] définit le modèle relationnel comme *"une manière de modéliser les relations existantes entre plusieurs informations, et de les ordonner entre elles."*

![Diagramme de base de données](https://www.memoireonline.com/02/12/5302/Conception-et-implementation-d-une-base-de-donnees-dynamique-et-partagee-de-gestion-clinique6.png)

Un modèle de bases de données définit entre autres **la structure logique** de cette base de données. Il existe beaucoup de modèles de bases de données différentes, mais comme pour les langages de programmation, certains sont plus utilisés que d'autres.

Les modèles de bases de données les plus courants sont:

- Modèle de base de données hiérarchique
- Modèle relationnel
- Modèle réseau
- Modèle de base de données orientée objet
- Modèle entité-association
- Modèle document
- Modèle entité-attribut-valeur
- Schéma en étoile
- Le modèle relationnel-objet, qui associe les deux éléments qui composent son nom

Vous pouvez consulter ce [**site**](https://www.lucidchart.com/pages/fr/quest-ce-quun-mod%C3%A8le-de-base-de-donn%C3%A9es) pour en savoir plus sur chacun de ces modèles.

### <a name="crud"></a>Les fonctions du CRUD
CRUD est un acronyme informatique anglais qui correspond à 4 fonctions nécessaires pour manipuler une base de données: "Create-Read-Update-Destroy". Il est intéressant de relier ces opérations à des méthodes HTTP. Le GET et le POST par exemple sont des méthodes HTTP qui correspondent respectivement aux opérations READ et CREATE. Pour les opérations Update et Destroy, les méthodes HTTP correspondantes sont PUT et DELETE.

Voici la synthèse des fonctions en tableau :

|**Opération**|**SQL**   |**HTTP**|
|:---|:---:|:---:|
|Create|[INSERT](https://fr.wikipedia.org/wiki/Insert_(SQL))|POST|
|Read|[SELECT](https://fr.wikipedia.org/wiki/Select_(SQL))|GET|
|Update|[UPDATE](https://fr.wikipedia.org/wiki/Update_(SQL))|PUT|
|Delete|[DELETE](https://fr.wikipedia.org/wiki/Delete_(SQL))|DELETE|

Pour en savoir plus, vous pouvez regarder [cette vidéo](https://www.grafikart.fr/formations/ruby-on-rails/crud).

___

Bravo si vous êtes arrivés au bout de ce README :clap:


