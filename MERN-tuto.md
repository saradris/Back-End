# MERN 

Salut à tous, je vous propose de suivre étape par étape ce court tutoriel introduisant au stack technique MERN.

## Etape 1

Créez un nouveau dossier à l'emplacement de votre choix.
Ouvrez un terminal et naviguez jusqu'à entrer dans ce dossier.
Une fois fait, commencez pas créer un nouveau projet React à l'aide de la boite à outil [CF la documentation](https://fr.reactjs.org/docs/create-a-new-react-app.html)

```
npx create-react-app client
```
Pour rappel: 
- **NPX** est l'installation portable des package NPM.
- **Create-react-app** est la commande permettant d'utiliser la boîte à outils de react (pré-configuration des fichiers)
- **client** suffixe destiné au nom que vous souhaitez donner à votre projet react. Dans ce cas ci nous utilisons le terme client car notre projet react n'est que la partie "client" de notre application


## Etape 2

Une fois react installé dans votre projet, vous pouvez continuer la mise en place de votre environnement.
Comme vous le savez, pour utiliser les technologies spécifiques que vous avez choisies vous devez les installer au préalable. PHP et Wordpress s'installaient de manière globale sur votre ordinateur (il est également possible à l'aide de Docker de ne les installer qu'au sein d'un container d'environnement mais ce n'est pas le propos). Grâce à Node vous pouvez installer les différents frameworks et librairies JS dont vous avez besoin au sein de votre projet et uniquement à cet endroit.

Commencez par faire la liste des technologies dont vous avez besoin, puis rechercher leur mode d'installation et la version si nécessaire.

```
npm init
```

Dans notre cas nous aurons besoin d'express, mongoose, le package cors, ainsi que body parser.
Pour ne pas répéter indéfiniment les commandes d'installation vous pouvez simplement concaténer l'entierté des packages dont vous avez besoin en un npm install:

```
npm install express body-parser cors mongoose
```

Nous allons également installer nodemon.
Nodemon est un package permettant d'observer vos fichiers et ses changements lors du développement sur serveur local. Il vous permet ainsi de ne pas avoir à relancer systématiquement votre serveur pour chaque modification.

```
npm install nodemon
```

## Etape 3

Jetez un coup d'oeil à votre arboressence de fichiers. 
A ce stade du tutoriel vous possédez un dossier client, un dossier node_modules dans lequel sont installés les fichier sources des différents packages que nous venons de télécharger.
Un fichier package-lock.json contenant les meta informations des-dits packages.
Un fichier package.json comportant la configuration générale de votre application.

A la racine de votre dossier, créez un nouveau dossier appelé "server". Vous pouvez le créer à l'aide de votre terminal:

```
mkdir server
```

## MongoDB

MongoDB est le système de base de donnée noSQL que nous allons utiliser pour ce projet.
Si vous ne possédez pas encore son outils de visualisation (MongoDB Compass), je vous invite à le télécharger et l'installer via le lien suivant [Install MongoDB Server](https://www.mongodb.com/try/download/community?tck=docs_server) ainsi que celui ci afin d'installer le client Compass: [Install Compass](https://www.mongodb.com/try/download/compass)
Lorsque votre outil est installé, clickez sur l'onglet "New connexion"

Pour vous connecter à votre localhost tapez la commande suivante dans l'input prévu à cet effet:

```
mongodb://localhost:27017
```

Ensuite clickez sur le bouton "CREATE DATABASE"

Donnez un nom à votre base de donnée: todolist
Compass vous demandera ensuite de créer une première table, nommez là "todos".

## Etape 4

Vous pouvez maintenant naviguer, à l'aide de votre terminal, à l'intérieur de votre dossier server.
Nous allons créer un fichier server.js qui permettra de paramétrer notre serveur.
Utilisez la commande suivante:

```
touch server.js
```

Nous allons également créer un nouveau dossier DB au sein duquel nous allons configurer la connexion à la base de donnée.

```
mkdir DB
```

Ensuite, au sein de ce dossier créez un fichier index.js

```
touch index.js
```

## Etape 5

Nous allons maintenant nous pencher à la rédaction du code côté serveur.

Au sein du fichier **server.js** à la racine de votre dossier server copiez collez le code suivant:

```js
const express = require('express')
const bodyParser = require('body-parser')
const cors = require('cors')

const db = require('./db')

const app = express()
const PORT = 3000

app.use(bodyParser.urlencoded({ extended: true }))
app.use(cors())
app.use(bodyParser.json())

db.on('error', console.error.bind(console, 'MongoDB connection error:'))

app.listen(PORT, () => console.log(`Server running on port ${PORT}`))
```

- 1. On stock les différentes dépendances au sein de variables
- 2. La variable app permet de lancer l'infrastructure d'express.
- 3. La constante PORT défini sur quel port notre serveur va se positionner (n'oubliez pas qu'il faut un port pour le côté serveur et un port pour le côté client).
- 4. La méthode .use() est relative à express, elle permet de renseigner à l'application les dépendances à utiliser.
- 5. La méthode .listen() lance le serveur local à l'aide du port prédéfini plus haut.

## Etape 6

Dans votre fichier **index.js** à la racine du dossier DB:

```js
const mongoose = require('mongoose')

mongoose
    .connect('mongodb://127.0.0.1:27017/todos', { useNewUrlParser: true })
    .catch(e => {
        console.error('Connection error', e.message)
    })

const db = mongoose.connection

module.exports = db
```

Rappel: un module est un bout de code réutilisable partout dans l'application à l'aide des méthodes exports et require.

- 1. Pour nous connecter à notre base de donnée nous avons besoin du package mongoose qui permet de créer un lien entre node et mongoDB
- 2. La fonction connect reçoit deux arguments, l'URL de connexion en premier, l'objet de configuration de l'autre. 
- 3. Stockez la connexion au sein d'une variable afin de pouvoir l'importer facilement dans les fichiers où cela s'avère nécessaire

## Etape 7

Pour ce projet nous utilisons l'architecture MVC.
Créez un dossier Models au sein de votre dossier server

```
mkdir models
```

Puis naviguez à l'intérieur de ce nouveau dossier et créez un nouveau fichier todosModel.js

```
touch todosModel.js
```

Dans votre fichier todosModel, copiez collez le bout de code suivant

```js
const mongoose = require('mongoose')
const Schema = mongoose.Schema

const Todo = new Schema(
    {
        todo: { type: String, required: true },
    },
    { timestamps: true },
)

module.exports = mongoose.model('todos', Todo)
```

Il s'agit ici de définir un schéma des données à insérer dans votre DB
Pour ce faire nous utilison la classe Schema de mongoose (n'oubliez pas de l'importer au préalable).
Le schéma est défini comme un objet avec une clé et une valeur contenant elle même un objet permettant sa configuration (de quel type de donnée s'agit il, est ce un champs requis ou non?)
Ensuite le schéma est appliqué à la méthode model, elle même exportée afin d'être disponnible partout dans notre application.

## Etape 8

Nous allons maintenant configurer le router de notre serveur. Pour rappel le routeur côté serveur permet de configurer les URL de contact de notre base de donnée (Endpoints).
A la racine de votre dossier server, créez un nouveau dossier nommé router

```
mkdir router
```
Puis dans ce dossier, créez un nouveau fichier todosRouter.js

```
touch todosRouter.js
```

Copiez collez y le bout de code suivant:

```js

const express = require('express')

const todoCtrl = require('../controllers/todosController')

const router = express.Router()

router.post('/', todoCtrl.createItem)
router.get('/', todoCtrl.getTodos)

module.exports = router
```
Nous utilisons le middleware router d'express, il vous faut donc importer express et stocker sa méthode router au sein d'une variable portant le même nom (pour plus de transparence).
Comme vous pouvez le constater nous avons déjà préparé l'import du fichier contrôleur et de ses fonctions afin de définir les routes.
Pour rappel une route est définie par l'URL, la fonction vers laquelle nous souhaitons rediriger l'appel, et le verbe HTTP qui y correspond.

## Etape 9

Nous allons maintenant nous pencher sur la rédaction d'un contrôleur simple.

Comme pour les étapes précédentes, créez un dossier à la racine du dossier server

```
mkdir controllers
cd controllers
touch todosController.js
```
Puis copiez collez y le code suivant:

```js
const Todo = require('../models/todosModel')

createItem = (req, res) => {
    const body = req.body
    if (!body) {
        return res.status(400).json({
            success: false,
            error: 'You must provide an item',
        })
    }

    const todo = new Todo(body)

    if(!todo){
        return res.status(400).json({ success: false, error: err })
    }

    todo.save().then(() => {
        return res.status(200).json({
            success: true,
            id: todo._id,
            message: 'todo item created',
        })
    })
    .catch(error => {
        return res.status(400).json({
            error,
            message: 'todo item not created',
        })
    })
}

getTodos = async (req, res) => {
    await Todo.find({}, (err, todos) => {
        if (err) {
            return res.status(400).json({ success: false, error: err })
        }
        if (!todos.length) {
            return res
                .status(404)
                .json({ success: false, error: `Item not found` })
        }
        return res.status(200).json({ success: true, data: todos })
    }).catch(err => console.log(err))
}

module.exports = {createItem, getTodos}
```
Comme nous avons besoin du schéma de données de notre DB, commencez par importer votre modèle, c'est lui qui permettra de savoir où insérer votre requête au sein de la DB.
Pour rappel, c'est au sein du contrôleur que vous insérez votre CRUD.

## Etape 10

Nos fichiers sont maintenant tous prêts. Il nous reste à ajouter le routeur au fichier de configuration **server.js**.
Ajoutez cette ligne à la fin de vos imports:

```js
const todoRouter = require('./router/todoRouter')
```
Ensuite, ajoutez la ligne suivante à la fin de votre fichier, juste avant la ligne activant le serveur (app.listen()).

```js
app.use('/', todoRouter)
```

Votre fichier server.js devrait maintenant ressembler à ceci:

```js
const express = require('express')
const bodyParser = require('body-parser')
const cors = require('cors')

const db = require('./db')
const todoRouter = require('./router/todoRouter')

const app = express()
const PORT = 3000

app.use(bodyParser.urlencoded({ extended: true }))
app.use(cors())
app.use(bodyParser.json())

db.on('error', console.error.bind(console, 'MongoDB connection error:'))

app.use('/', todoRouter)

app.listen(PORT, () => console.log(`Server running on port ${PORT}`))
```

## Etape 11

Nous allons maitenant tester nos requêtes. Pour ce faire téléchargez et installez [POSTMAN](https://www.postman.com/downloads/) 
Ouvrez l'application, dans le champs prévu insérez l'URL de votre API (localhost:3000/)

Ensuite dans l'onglet body, sélectionnez l'item "raw", à l'extrême droite clickez sur la selection "text" et choisissez "JSON"

Dans l'espace dédié au corps de la requête insérez l'objet suivant

```js
{
    "todo":"test"
}
```

Clickez sur "SEND" et récupérez la réponse de votre requête


## Etape 12 

Si vos requêtes fonctionnent, vous en avez terminé avec la partie serveur de votre application.
Nous allons maintenant créer une interface utilisateur simple à l'aide de React.

Pour plus de facilité, nous allons utiliser Axios, une librairie JS permettant de créer des appels vers notre serveur.

Naviguez à l'intérieur de votre dossier client et tapez la commande suivante dans votre terminal:

```
npm install axios
```

Au sein de votre dossier **src**, créez un dossier **component**
Ensuite dans votre dossier component créez un fichier **Todo.js**

Puis copiez collez cet exemple de code:

```js
import React, { Component } from 'react'
import axios from 'axios';

export class Todo extends Component {
    constructor(props) {
        super(props)
    
        this.state = {
             todos : [],
             item : ""
        }
    }

    changeHandler = (event) => {
        this.setState({item: event.target.value})
    }

    clickHandler = (event) => {
        event.preventDefault()
        console.log(this.state.item)
        axios({
            method: 'post',
            url: 'http://localhost:3000/',
            data: {
              todo: this.state.item,
            }
          });
        this.setState({item:''})
    }

    componentDidMount() {
        axios.get('http://localhost:3000/').then((response) => {
            console.log(response.data.data)
            let data = [];
            console.log(response.data.data.length)
            for(var i =0; i < response.data.data.length; i++){
                data.push(response.data.data[i].todo)
            }
            this.setState({todos: data})
        });
    }
    componentDidUpdate() {
        axios.get('http://localhost:3000/').then((response) => {
            console.log(response.data.data)
            let data = [];
            console.log(response.data.data.length)
            for(var i =0; i < response.data.data.length; i++){
                data.push(response.data.data[i].todo)
            }
            this.setState({todos: data})
        });
    }
  
    render() {
        
        return (
            <div>
                <input type="text" onChange={this.changeHandler}/>
                <button type="submit" onClick={this.clickHandler}>add</button>
                <div>
                    <ul>{this.state.todos.map((todo, index) => <li key={index}>{todo}</li>)}</ul>
                </div>
            </div>
        )
    }
}
export default Todo;
```

## Etape 13

Enfin pour terminer, au sein de votre dossier src, dans le fichier **app.js** remplacé son contenu actuel par le suivant:

```js
import React from 'react';
import './App.css';
import Todo from './component/Todo';

function App() {
  return (
    <div className="App">
      <Todo/>
    </div>
  );
}

export default App;
```

Dans votre terminal, lancez votre serveur local client / votre serveur à l'aide de deux fenêtres ouvertes dans votre terminal de commande:

Commencez par la le serveur

```
nodemon server/server.js
```

Ensuite le client (n'oubliez pas d'ouvrir le terminal dans votre dossier client pour celui ci)

```
npm start
```
