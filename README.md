# The Hacking Project

## Week 5 - Day 1
#### Lundi 5 février

First of all, have a look on what we've done yesterday on that amazing Heroku app: [Secret de l'Univers](https://secret-de-lunivers.herokuapp.com/).

Ce qu'il y a à savoir: Rien.

## 1. Les bases
# 1.1. Création
Console > rails new **secret**.
```cd secret```
SublimText > Ouvrir le dossier *secret*. Ouvrir le fichier **Gemfile**. Ctrl+a. Suppr. Ouvrir le fichier [Gemfile de Felix](https://github.com/felhix/cheat_sheets/blob/master/Ruby/Gemfile.rb). Ctrl+a. Ctrl+c. On ctrl+c tout ça dans le **Gemfile** du dossier *secret*. 

## 1.2. Le model
Console > ```Rails generate model User email:string```
Sublime text > app > models > user.rb
On ajoute la ligne ```has_secure_password
  validates :password, presence: true, length: { minimum: 6 }``` 
  
  SI y a pas la suite c'est que j'ai pas eu le temps de finir mon REadME avant le gong :)

il y aura un attribut email, unique, avec une présence obligatoire
il y aura un password, que l'on va gérer avec has_secure_password. Si jamais ta mémoire te trahit, voici le lien du chapitre du bouquin de Hartl qui en parlait
Puis, étant donné que nous aimons bien créer des applications que les gens peuvent utiliser facilement, nous allons te demander de mettre à jour le fichier seeds.rb pour y rentrer un utilisateur qui te servira pour aller sur ton app.

1.3. CRUD
Pour le model User, fais un petit CRUD, afin de ne pas perdre la main ✌️

2. Brève architecture
Voici les deux pages importantes du site :

2.1. La home
Notre site va contenir une page d'accueil, qui va proposer en lien notre page top secrète.

2.2. La page secrète
La page secrète doit annoncer la réponse à la question de l'univers.

3. Login ?
Nous allons plus ou moins reprendre le chapitre de basic login pour cette partie. Si jamais tu es bloqué, la solution se trouvera sûrement dans ce chapitre 😎
Jouer avec les logins et les mots de passe est un bon moyen de voir comment une app marche, sous le capot.

3.1. La base
Nous allons donc créer le login. Pour cela, il faut créer le controller des sessions, puis faire les views correspondantes. Crée le controller des sessions, avec comme méthodes new, create, et destroy.

Nous allons commencer par la view pour la méthode new.

3.2. Le login
Nous allons nous attaquer à la méthode create. Si l'utilisateur arrive à s'autentifier, login ce dernier. Sinon, render new.

3.3. Session Helper
Le SessionHelper est très pratique pour utiliser les méthodes de login qui sont ultra conventionnelles chez Rails. Créé donc le SessionHelper avec les méthodes log_in(user), current_user, et logged_in?, et log_out.

3.4. Header
Le header du site doit afficher le lien pour se login (donc la page correspondante à session#new) si jamais l'utilisateur n'est pas login. Si ce dernier est login, le header doit afficher le lien pour se logout.

4. Restriction d'accès
Notre page avec la réponse de l'univers ne doit être accessible que pour les personnes enregistrées sur le site. Si une personne n'est pas login et essaie d'accéder à cette page, le site doit la rediriger vers la page de login.

5. Version des champions
Cette partie permettra d'ajouter un peu de fluidité dans l'utilisation de ton application.

5.1. Login au signup
Notre super site tourne, mais ce serait super cool si notre utilisateur arrivait à se login quand il s'inscrivait sur le site. Fais-donc ceci.

5.2. Restriction, niveau Grand BG des Famille
Actuellement, tous les utilisateurs peuvent aller éditer les pages de tout le monde. Fais en sorte que les pages d'édition de profil ne peuvent être accédées que par les utilisateurs concernés (et qui doivent être login bien entendu). On me dit dans mon oreillette que la variable current_user te sera utile 😉

5.3. Flash error
Pour la page top secrète, actuellement, quand une personne non login y va, le site le redirige vers la page de login. Ce serait bien d'afficher un petit flash pour lui dire "hey login-toi pour y accéder", c'est bien plus poli !

```<% if logged_in? %>```

Pour les formes des boutons, voilà une petite astuce bien sympa, histoire de pimenter le tout: [W3S](https://www.w3schools.com/bootstrap/bootstrap_buttons.asp).



