# Express.JS

Express JS est un framework écrit en Javascript et émulé sur Node.JS, permettant d'utiliser l'objet JavaScript HTTP. Cet objet permet de créer et traiter les requêtes HTTP nécessaires au fonctionnement de votre application.

Il comprend entre autre un système de Routeur permettant de rediriger les appels vers les fichiers permettant de traiter ces appels et soliciter les requêtes, ainsi que des middlewares (petits programmes intermédiaires permettant le bon fonctionnement du programme général). 

## Un mot sur le middleware Body Parser

Body Parser est un des middlewares utilisé par Express. Dans le contexte d'une requête POST, il permet de gérer les types de données entrées via un formulaire (considérées comme "raw request" avant d'être traduite en "JSON request") afin de constituer un corps de requête acceptable par la base de données. Il permet de traduire la valeur des inputs en objet Javascript.

## Installation

Ouvrez votre terminal, naviguez jusqu'au dossier de votre projet nécessitant Express.

Tapez la commande suivante:

```
npm install express --save
```

## Architecture du projet

Privilégiez une architecture MVC.
Voir le fichier architecture-mvc.md à la racine de ce repository.

Dans l'arborescence des fichiers que je vous ai donné en exemple vous constaterez la présence d'un dossier routes.

Dans ce dossier, le fichier tutorial.routes.js contiens le middleware routeur d'express, il s'agira ici de programmer toutes les routes nécessaires à la création des Endpoints (points de contact) de votre API.

## Le fichier app.js, server.js ou index.js

A la racine du dossier server de votre application.
Il contient les imports et la configuration nécessaire aux dépendances installées, dont Express.

Pour rappel Express permet de mettre en place votre serveur, d'effectuer des requêtes HTTP, et de configurer les Endpoints de votre API

Voici un exemple de configuration du serveur.

```js
const express = require("express");
const bodyParser = require("body-parser");
const cors = require("cors");

const app = express();

var corsOptions = {
  origin: "*"
};

app.use(cors(corsOptions));

// parse requests of content-type - application/json
app.use(bodyParser.json());

// parse requests of content-type - application/x-www-form-urlencoded
app.use(bodyParser.urlencoded({ extended: true }));

// simple route
app.get("/", (req, res) => {
  res.json({ message: "Ahoy!" });
});
require("./routes/comment.routes")(app);
// set port, listen for requests
require('dotenv').config()
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}.`);
});
console.log(process.env.DATABASE_URI)
const db = require("./models");
db.mongoose
  .connect(process.env.DATABASE_URI || db.url, {
    useNewUrlParser: true,
    useUnifiedTopology: true
  })
  .then(() => {
    console.log("Connected to the database!");
  })
  .catch(err => {
    console.log("Cannot connect to the database!", err);
    process.exit();
  });
  ```

  Pour lancer ce script et par la même occasion mettre en route votre serveur vous pouvez configurer une ligne de script pour votre terminal de commande dans le fichier package.json

  Par exemple:

  ```js
  "npm start-server": "node server/index.js"
  ```

## La fonction app.use()

Accepte en paramètrele middleware nécessaire au fonctionnement de votre application.
Dans notre exemple il s'agit de body-parser. 
Le paramètre utilisé est la variable dans laquelle nous stockons le require des fichiers sources nécessaires.
Il peut accepter un second paramètre qui serait directement la fonction du middleware que nous désirons utiliser.

Dans notre cas nous utilisons deux fois le middleware body-parser.
Il va d'abord analyser le corps de la requête soit au format json, soit au format url-encoded. Ensuite il restitura le corps de la requête au sein de req.body

Pour info: express permet aussi de parser les cookies via le middleware cookieParser.

## Le routeur

Comme indiquez plus haut il s'agit de la configuration des points de contact de votre API;
Le routeur permet de créer une URL pointant vers les fichiers de traitement de données.

```js
module.exports = app => {
    const tuto = require("../controllers/tuto.controller");
  
    var router = require("express").Router();
  
    // Create a new Tutorial
    router.post("/", tuto.create);
  
    // Retrieve all Tutorials
    router.get("/", tuto.findAll);
  
    // Retrieve a single Tutorial with id
    router.get("/:id", tuto.findOne);
  
    app.use('/api/tuto', router);
  };
  ```
  module.exports: permet de créer un module et de l'exporter. Voir la théorie MDN sur les modules en JS.

  La variable tuto requiert l'utilisation du fichier tuto.controller contenant les contrôleurs de la table "tuto" de notre API.

  La variable router requiert l'utilisation d'express et de sa fonction Router().
  
  La fonction Router peut appliquer d'autres fonctions qui lui sont relatives. Par exemple get et post permettant de différencier le type de verbe HTTP qui sera utilisé pour une même route.

  Dans cet exemple la route "/" sert donc à créer via le verbe post mais également à afficher via le verbe get.

## Le middleware CORS

Permet de modifier la police de cross origin des serveurs.
Pour contacter votre API,si les cors sont activés, un programmeur sera dans la contrainte de vous demander l'accès. Si l'accès est refusé ses requêtes (même si elles sont correctement exécutées) seront refusées avant même d'atteindre votre serveur via les headers.

Je vous invite à revoir la théorie sur les headers envisagée plus tôt dans le premier cycle de formation.

Pour désactiver les cors il suffit de pointer l'accès sur "all", comme au sein du fichier de configuration app.js ci dessus.

## Ressources:

La très bonne documentation d'express en français: [Express](https://expressjs.com/fr/)