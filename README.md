# The Secret
[(le vrai)](https://www.youtube.com/watch?v=fQu_twwpKvk)

## Week 5 - Day 1
#### Lundi 5 février

First of all, have a look on what we've done yesterday on that amazing Heroku app: [Secret de l'Univers](https://secret-de-lunivers.herokuapp.com/).

Ce qu'il y a à savoir: Rien.

## 1. Les bases
### 1.1. Création
Console > **rails new secret**.
**cd secret**
SublimText > Ouvrir le dossier *secret*. Ouvrir le fichier *Gemfile*. Ctrl+a. Suppr. Ouvrir le fichier [Gemfile de Felix](https://github.com/felhix/cheat_sheets/blob/master/Ruby/Gemfile.rb). Ctrl+a. Ctrl+c. On ctrl+v tout ça dans le *Gemfile* du dossier *secret*. 

### 1.2. Le model
Console > **Rails generate model User email:string**</br>
Sublime text > app > models > user.rb </br>
On sait que ce model doit avoir un attribut email, unique, avec une présence obligatoire: </br> Dans notre model, le fichier User.rb, on va donc ajouter cet attribut: 
``` ruby
validates :email, presence: true, length: { maximum: 140 },
                    format: { with: VALID_EMAIL_REGEX }, uniqueness: { case_sensitive: false }
```
Ici on informe la base de donnée qu'elle n'enregistrera ces données si et seulement si il y a bien un input pour l'**:email** (presence: true), et qu'il fais moins de X caractères.</br>
De plus, on précise ici que le format de l'input doit respecter *VALID_EMAIL_REGEX*, mais qu'on est pas regardant au case sensitive. </br>
Cette variable ```VALID_EMAIL_REGEX``` est définie juste avant:</br> ```VALID_EMAIL_REGEX = /\A[\w+\-.]+@[a-z\d\-.]+\.[a-z]+\z/i``` qui indique les caractères acceptés et la "structure" que doit avoir l'adresse mail (@, . )...</br>
Je ne vais pas vous mentir, c'est copié directement du [Book](http://ruby.railstutorial.org/ruby-on-rails-tutorial-book).

On a donc un utilisateur qui input un email. Mais on est pas des sauvages, on va lui demander son nom: 
 validates **:name**,  presence: true, length: { maximum: 15 }.

On fais appel à la méthode 
``` ruby
has_secure_password 
  validates :password, presence: true, length: { minimum: 6 }
```
Qui dit que pour que les "password" soient stockés dans la Database, il doit être "présent" (true) et d'au minimum 6 caractères. Sans quoi le password ne sera pas enregistré.
  
### Petit po(i)nt.
On a donc créé un model qui prend en compte 3 attributs: l'**:email**, le **:name** et le **:password**. Ces 3 attributs ont des validations particulières, qui font que notre base de donnée va pas sauvegarder n'importe quoi.

### 1.3. CRUD
On se fait notre petit *CRUD* pour le model User:
* Une Methode New: `@user = User.new`
* Une Méthode Create: `@user = User.new(user_params)`
* Une Methode Show: `@user = User.find(params[:id])`
* Une Methode Edit: `@user = User.find(params[:id])`
``` ruby
@user = User.find(params[:id])
  	if @user.update(user_params)
  		redirect_to @user
  	else render 'edit'
  	end
```
Bien évidemment, au sein de ce controller, nous allons rajouter une methode '[private](http://edgeguides.rubyonrails.org/action_controller_overview.html#strong-parameters)' qui va définir quels attributs sont nécessaires pour les paramètres.

Ces Methodes auront chacune leur *'view'* que vous pouvez retrouver dans le Repository.

## 2. Brève architecture
Voici les deux pages importantes du site :
### 2.1. La home
Notre site va contenir une page d'accueil, qui va proposer en lien notre page top secrète.</br>
- Est ce qu'on ferait pas un petit **rails generate controller static_pages index** ? Bin si.
- Puis ensuite on ouvrirait notre fichier *config > routes.rb*
- Puis on y indiquerait que notre page *root* est la page Index dans notre controlleur static_pages, de la sorte: `root 'static_pages#index'`afin que notre application sache où est sa maison.
Dans le *index.html.Erb* qui se trouve dans en app>views>static_pages> on pourra faire une mise en bouche des plus explicites:
> <h1> Coucou toi </h1>
> <h2> T'as déjà un compte? </h2>
> <p> Non? T'attends quoi ? </p>




### 2.2. La page secrète
La page secrète doit annoncer la réponse à la question de l'univers.


## 3. Login ?


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



