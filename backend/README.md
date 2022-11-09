# Backend du café

## Commencer

### Installation des dépendances

####Python 3.7

Suivez les instructions pour installer la dernière version de python pour votre plate-forme dans la [docs python](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of -python)

#### Environnement virtuel

Nous vous recommandons de travailler dans un environnement virtuel chaque fois que vous utilisez Python pour des projets. Cela permet de garder vos dépendances pour chaque projet séparées et organisées. Les instructions de configuration d'un environnement virtuel pour votre plate-forme se trouvent dans les [documents python](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### Dépendances PIP

Une fois que vous avez configuré et exécuté votre environnement virtuel, installez les dépendances en accédant au répertoire `/backend` et en exécutant :

```bash
pip install -r exigences.txt
```

Cela installera tous les packages requis que nous avons sélectionnés dans le fichier "requirements.txt".

##### Dépendances clés

- [Flask](http://flask.pocoo.org/) est un framework léger de microservices backend. Flask est nécessaire pour gérer les demandes et les réponses.

- [SQLAlchemy](https://www.sqlalchemy.org/) et [Flask-SQLAlchemy](https://flask-sqlalchemy.palletsprojects.com/en/2.x/) sont des bibliothèques pour gérer la base de données sqlite légère . Puisque nous voulons que vous vous concentriez sur l'authentification, nous nous occupons du gros du travail pour vous dans `./src/database/models.py`. Nous vous recommandons de parcourir d'abord ce code afin de savoir comment vous connecter au modèle Drink.

- [jose](https://python-jose.readthedocs.io/en/latest/) Signature et chiffrement d'objets JavaScript pour les JWT. Utile pour encoder, décoder et vérifier JWTS.

## Lancer le serveur

Depuis le répertoire `./src`, assurez-vous d'abord que vous travaillez avec votre environnement virtuel créé.

Chaque fois que vous ouvrez une nouvelle session de terminal, exécutez :

```bash
exporter FLASK_APP=api.py ;
```

Pour exécuter le serveur, exécutez :

```bash
flask run --reload
```

Le drapeau `--reload` détectera les changements de fichiers et redémarrera le serveur automatiquement.

## Tâches

### Configuration Auth0

1. Créez un nouveau compte Auth0
2. Sélectionnez un domaine locataire unique
3. Créez une nouvelle application Web d'une seule page
4. Créez une nouvelle API
   - dans Paramètres API :
     - Activer RBAC
     - Activer Ajouter des autorisations dans le jeton d'accès
5. Créez de nouvelles autorisations d'API :
   - `obtenir : des boissons`
   - `get:drinks-detail`
   - `post:boisson`
   - `patch : boissons`
   - `supprimer : boissons`
6. Créez de nouveaux rôles pour :
   - Barista
     - peut `get:drinks-detail`
     - peut `obtenir : des boissons`
   - Gestionnaire
     - peut effectuer toutes les actions
7. Testez vos terminaux avec [Postman](https://getpostman.com).
   - Enregistrez 2 utilisateurs - attribuez le rôle Barista à l'un et le rôle Manager à l'autre.
   - Connectez-vous à chaque compte et notez le JWT.
   - Importer la collection postman `./starter_code/backend/udacity-fsnd-udaspicelatte.postman_collection.json`
   - Cliquez avec le bouton droit sur le dossier de collecte pour le barista et le gestionnaire, accédez à l'onglet d'autorisation et incluez le JWT dans le champ du jeton (vous devriez avoir noté ces JWT).
   - Exécutez la collecte et corrigez les éventuelles erreurs.
   - Exportez la collection en écrasant celle que nous avons incluse afin que nous ayons vos JWT appropriés lors de l'examen !

### Implémenter le serveur

Il y a des commentaires `@TODO` dans le `./backend/src`. Nous vous recommandons d'aborder les fichiers dans l'ordre et de haut en bas :

1. `./src/auth/auth.py`
2. `./src/api.py`