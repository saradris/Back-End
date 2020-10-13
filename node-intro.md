# Introduction Node.JS

## Table des matières 

1. Qu'est ce que Node.JS?
2. NPM
3. Package.json vs Package-lock.json
4. Les node_modules
5. Ressources

## 1. Qu'est ce que Node.JS?

**/!\ Node n'est pas à proprement parlé un langage, il s'agit d'une plateforme d'exécution, un environnement permettant d'héberger du code Javascript tant côté front-end que côté back-end.**

Node.JS est un framework EcmaScript, il se comporte comme un navigateur en lisant et interprêtant le code à l'aide du moteur Javascript V8 de Google. 
Il permet entre autre la création de services coté serveur, mais également de scripts utilisables dans votre invite de commande (nous pourrions imaginer un script traduisant un fichier excel en format JSON par exemple).

Node permet entre autre de créer un environnement de développement avec un serveur local sur lequel il peut compiler le code client et indépendament un autre serveur local permettant cette fois de compiler le code server.

Node ne possède pas une syntaxe propre, le code est rédigé autant côté serveur que côté client en Javascript pur (sauf utilisation concomitente d'un autre framework ou d'une librairie comme React coté client par exemple).

Standariser son code en utilisant du Javascript pour l'ensemble du programme permet de l'abstraire au maximum et d'éviter la redondance. 

Tout comme JS, Node permet l'asynchronisme et est dit "non bloquant" c'est à dire qu'il peut exécuter plusieurs tâches à la fois, les libertés sont multiples et il est facile de jongler entre front-end et back-end étant donné que tout deux sont envisagés en JS.

## 2. NPM

Lorsque vous installez Node sur votre machine, l'installation comprend le moteur JS, une invite de commande spécifique à node (que vous n'êtes **pas** obligé d'utiliser) ainsi que l'outil NPM.

Node Package Manager, la communauté NPM est une communauté de developpeurs Javascript, il s'agit d'un outil open source permettant de mettre en ligne des bouts de code / librairies / bibliothèques / frameworks écrit par les membres de la communauté. 
Ils permettent de bénéficier d'outils dévellopés par la communauté, et d'y participer en postant votre travail. Il peut s'agir d'une petite librairie permettant d'ajouter de l'effet à votre scroll ou d'un framework complet tel qu'express.

NPM s'utilise en ligne de commande, lorsque vous tapez npm + le nom et la version du package demandé, il va se charger de le télécharger pour vous et d'installer les dépendances soit de manière globale à votre machine (si vous le spécifiez) soit uniquement au sein de votre projet. 

Vous avez déjà tous travaillez avec Sass, le principe est identique ici.

https://www.npmjs.com/

## 3. Package.json Package-lock.json

Pour une première utilisation de tout nouveau projet comportant un fichier **package.json** ou **package-lock.json** veillez à bien lancer la commande 

```
npm install
```

Une fois les dépendances installées dans le projet original, elles seront répertoriées au sein d'un fichier package.json. Lorsque vous tapez la commande npm install, npm va utiliser votre copie du fichier package.json pour installer toutes les dépendances dont vous avez besoin afin de faire tourner correctement votre projet.

Le fichier package.json contient toutes les meta informations nécessaires à votre projet:

Le nom que vous souhaitez donner à votre package (projet). L'auteur, la license, les scripts, les dépendances nécessaires au bon fonctionnement de votre application. En substance toute information utile à l'utilisateur potentiel.

```
npm install --save
```

Permet de sauver la dépendance dans l'objet "dev-dependancies", pour chaque installation du projet la bonne version d'express sera installée.

Un petit mot sur les scripts:

Il s'agit ni plus ni moins de commande déterminées par le programmeur permettant de lancer différents services.
Par exemple vous pourriez retrouver un script permettant de "watch" votre code en continu: vous ne seriez dés lors plus obligé de relancer votre serveur local après chaque modification entrée afin d'observer les éléments nouveaux et leur comportement.

## 4. Node_modules

Il est impératif de retenir ceci:

**Ne jamais au grand jamais push vos node_module sur GitHub!!!**
Il suffit de créer en même temps que votre repository un fichier gitignore permettant à git d'ignorer les fichiers indiqués, dont les node modules.

*Pourquoi ne PAS les inclure?*

En dehors du fait qu'ils sont particulièrement volumineux, les node_modules sont installé en fonction de votre environnement. Les pousser sur un repo git et les rendre disponnibles pour vos collègues développeurs risquerait de casser leur propre environnement si vous n'utilisez pas strictement les mêmes machines.

## 5. Ressources

- [OpenClassRoom: Node / Express / MongoDB](https://openclassrooms.com/fr/courses/6390246-passez-au-fullstack-avec-node-js-express-et-mongodb)

- [Documentation officielle](https://nodejs.org/en/docs/)

- [Intro Node par JSPOINT](https://medium.com/jspoint/introduction-to-node-js-a-beginners-guide-to-node-js-and-npm-eca9c408f9fe)

- [NPM](https://www.npmjs.com/)

- [GitIgnore](https://www.atlassian.com/git/tutorials/saving-changes/gitignore)