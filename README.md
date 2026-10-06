# Booste225
augmenter la visibilité d’une publication, gérer des campagnes, automatiser des tâches, suivre des statistiques, etc.
Pour créer une application qui gère des campagnes, augmente la visibilité d'une publication, automatise certaines tâches et suit des statistiques, voici un code complet utilisant Flask. Ce code inclut toutes les fonctionnalités demandées en un seul bloc. 

### Configuration :

Assurez-vous d'avoir Python et Flask installés. Installez les dépendances requises :

```bash
pip install Flask Flask-SQLAlchemy
```

### Code Complet :

Voici le code que vous pouvez copier et coller dans un fichier Python (par exemple, `app.py`) :

```python
from flask import Flask, request, jsonify
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///campagnes.db'
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
db = SQLAlchemy(app)

# Modèle de campagne
class Campagne(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    nom = db.Column(db.String(100), nullable=False)
    visibilité = db.Column(db.Integer, default=0)

    def to_dict(self):
        return {'id': self.id, 'nom': self.nom, 'visibilité': self.visibilité}

# Création des tables
@app.before_first_request
def create_tables():
    db.create_all()

# Endpoint pour créer une campagne
@app.route('/campagnes', methods=['POST'])
def creer_campagne():
    data = request.json
    campagne = Campagne(nom=data['nom'])
    db.session.add(campagne)
    db.session.commit()
    return jsonify(campagne.to_dict()), 201

# Endpoint pour obtenir une campagne par ID
@app.route('/campagnes/<int:id>', methods=['GET'])
def obtenir_campagne(id):
    campagne = Campagne.query.get_or_404(id)
    return jsonify(campagne.to_dict())

# Endpoint pour augmenter la visibilité d'une campagne
@app.route('/campagnes/<int:id>/augmenter_visibilite', methods=['POST'])
def augmenter_visibilite(id):
    campagne = Campagne.query.get_or_404(id)
    campagne.visibilité += 1
    db.session.commit()
    return jsonify(campagne.to_dict())

# Endpoint pour obtenir des statistiques sur toutes les campagnes
@app.route('/stats', methods=['GET'])
def obtenir_stats():
    campagnes = Campagne.query.all()
    stats = {campagne.nom: campagne.visibilité for campagne in campagnes}
    return jsonify(stats)

# Démarrage de l'application
if __name__ == '__main__':
    app.run(debug=True)
```

### Comment Utiliser l'Application :

1. **Démarrez l'application** en exécutant le fichier Python :
   ```bash
   python app.py
   ```

2. **Création d'une campagne** : 
   - Envoyez une requête POST à `http://127.0.0.1:5000/campagnes` avec un corps JSON :
     ```json
     {"nom": "Nom de la campagne"}
     ```

3. **Obtenez une campagne par ID** :
   - Faites une requête GET à `http://127.0.0.1:5000/campagnes/<id>`.

4. **Augmentez la visibilité** :
   - Envoyez une requête POST à `http://127.0.0.1:5000/campagnes/<id>/augmenter_visibilite`.

5. **Obtenez des statistiques** :
   - Faites une requête GET à `http://127.0.0.1:5000/stats
     Pour créer une application qui gère des campagnes, augmente la visibilité d'une publication, automatise certaines tâches et suit des statistiques, voici un code complet utilisant Flask. Ce code inclut toutes les fonctionnalités demandées en un seul bloc. 

### Configuration :

Assurez-vous d'avoir Python et Flask installés. Installez les dépendances requises :

```bash
pip install Flask Flask-SQLAlchemy
```

### Code Complet :

Voici le code que vous pouvez copier et coller dans un fichier Python (par exemple, `app.py`) :

```python
from flask import Flask, request, jsonify
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///campagnes.db'
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
db = SQLAlchemy(app)

# Modèle de campagne
class Campagne(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    nom = db.Column(db.String(100), nullable=False)
    visibilité = db.Column(db.Integer, default=0)

    def to_dict(self):
        return {'id': self.id, 'nom': self.nom, 'visibilité': self.visibilité}

# Création des tables
@app.before_first_request
def create_tables():
    db.create_all()

# Endpoint pour créer une campagne
@app.route('/campagnes', methods=['POST'])
def creer_campagne():
    data = request.json
    campagne = Campagne(nom=data['nom'])
    db.session.add(campagne)
    db.session.commit()
    return jsonify(campagne.to_dict()), 201

# Endpoint pour obtenir une campagne par ID
@app.route('/campagnes/<int:id>', methods=['GET'])
def obtenir_campagne(id):
    campagne = Campagne.query.get_or_404(id)
    return jsonify(campagne.to_dict())

# Endpoint pour augmenter la visibilité d'une campagne
@app.route('/campagnes/<int:id>/augmenter_visibilite', methods=['POST'])
def augmenter_visibilite(id):
    campagne = Campagne.query.get_or_404(id)
    campagne.visibilité += 1
    db.session.commit()
    return jsonify(campagne.to_dict())

# Endpoint pour obtenir des statistiques sur toutes les campagnes
@app.route('/stats', methods=['GET'])
def obtenir_stats():
    campagnes = Campagne.query.all()
    
