# Les bases du language PHP

Dans ce cours nous aborderons les bases de la synthaxe du langage PHP.
Tout comme en Javascript nous y retrouverons des déclarations de variables, des fonctions, des conditions, des boucles...
Le PHP est également un language orienté objet. 

Voici un lien vers votre nouvelle bible, après la MDN, la documentation PHP: https://www.php.net/manual/fr/index.php
Le bloc de cours qui suit est une synthèse des éléments de la doc et du très bon cours de Pierre Giraud que je vous demande de lire pour l'apprentissage de la matière: https://www.pierre-giraud.com/php-mysql-apprendre-coder-cours/introduction/

## Table des matières

1. Déclaration de variable
2. Les types de variables
3. La structure echo et la fonction vardump()
4. Les tableaux associatifs = les dictionnaires 
5. Les constantes
6. Les opérateurs
7. Include et require
8. Les conditions
9. Les boucles
10. Les fonctions
11. La balise PHP
12. Les formulaires

## 1. Déclaration de variable

En PHP il existe des convention de nomenclature plus accentuée qu'en Javascript.
Certains noms de variable sont déjà réservés par le langage.
Règles de nomenclature:

1. Toute variable débute par le signe **$**
2. S'en suit le nom de la variable qui doit obligatoirement débuter par une **lettre** ou un **underscore** mais **jamais un chiffre**
3. Le nom ne peut contenir aucun caractère spéciaux 
4. Comme en Javascript, le nom d'une variable ne doit pas contenir d'espace

```php
$name = "Julie"; 
```

## 2. Les types de variables

Tout comme en Javascript, le PHP est un langage typé. 

1. Le type « chaine de caractères » ou String en anglais ; 
2. Le type « nombre entier » ou Integer en anglais ;
3. Le type « nombre décimal » ou Float en anglais ;
4. Le type « booléen » ou Boolean en anglais ;
5. Le type « tableau » ou Array en anglais ;
6. Le type « objet » ou Object en anglais ;
7. Le type « NULL »;
8. Le type « ressource » ou Resource en anglais ;

## 3. La structure echo et la fonction var_dump()

### var_dump() 

Selon la **documentation**:

Affiche les informations structurées d'une variable, y compris son type et sa valeur. Les tableaux et les objets sont explorés récursivement, avec des indentations, pour mettre en valeur leur structure.

Il s'agit d'une fonction, repérable par le constructeur (), var_dump() est comparable au console.log mais de façon limitée, il ne peut afficher que les variables, leur type et leur valeur.

### Echo

Affiche dans le HTML les valeurs suivant la déclaration de l'echo, echo n'est techniquement pas une fonction mais une structure du langage, ceci dit tous les éléments suivants sa déclaration seront affichés comme si il s'agissait de paramètres de fonctions. Pour concaténer deux variable l'opérateur "." est utilisé. Pour les afficher en tant qu'arguments multiples l'opérateur "," est utilisé.

Le lien vers la documentation:

https://www.php.net/manual/fr/function.echo.php

## 4. Les tableaux associatifs = les dictionnaires

Déclaré à l'aide de la structure de langage array(), il se présente sous forme de clé-valeur rendues sous la forme suivante:
```php
$array = array(
    "hello" => "world",
    "world" => "hello"
)
```

Ou d'une manière plus similaire à JS:
```php
$array = [
    "hello" => "world",
    "world" => "hello",
];
```
Le lien vers la documentation:

https://www.php.net/manual/fr/language.types.array.php

ATTENTION: il s'agit ici uniquement des tableaux associatifs, vous pouvez également retrouver des tableaux 'simples" comme en Javascript:

**$sirius = ['Laetitia', 'David', 'Vincent', 'Jeremy', 'Christophe', 'Gregory', 'Julie']**

La manière de pointer dans ces tableaux est identiques à celle du JS: vous utilisez le nom du tableau suivi de l'index désiré

```php
echo $sirius[0]
```


## 5. Les constantes

Ce sont des variables simples qui ne peuvent JAMAIS être modifiées dans le script.
Elles sont toujours déclarées en majuscules et suivent les autres règles de nomenclature des variables exception faite qu'elle ne sont pas initialisée à l'aide d'un **$**.

Elles sont définies à l'aide de la fonction define() qui attend 3 paramètres

```php

define("HELLO", "WORLD", true );
```

Le premier paramètre défini le nom de la fonction, le second paramètre sa valeur, le troisième défini sa sensibilité à la casse est **facultatif** je vous conseille de ne pas utiliser ce troisième paramètre.

**La documentation se rapportant aux constantes** : https://www.php.net/define

Il existe un pannel de constantes prédéfinies par php dites "constantes magiques" . Certaines sont automatiquements intégrée à votre version de PHP d'autres nécessitent en revanche des extensions.

Je vous conseille la lecture de ce chapitre du merveilleux cours de Pierre Giraud s'y rapportant:

https://www.pierre-giraud.com/php-mysql-apprendre-coder-cours/constante-magique/

## 6. Les opérateurs

A titre informatif il existe 11 groupes d'opérateurs en PHP

- Les opérateurs arithmétiques ;
- Les opérateurs d’affectation ;
- Opérateurs sur les bits ;
- Opérateurs de comparaison ;
- Opérateur de contrôle d’erreur ;
- Opérateur d’exécution ;
- Opérateurs d’incrémentation et décrémentation ;
- Les opérateurs logiques ;
- Opérateurs de chaînes ;
- Opérateurs de tableaux ;
- Opérateurs de types ;

Nous allons aborder les plus utilisé uniquement pour ce cours:

### Opérateur de chaîne et de concaténation

Pour rappel nous avons déjà vu plus haut ces opérateurs
Il s'agit du **.** et de la **,**.

```php
echo "Hello" . $world;
```
```php 
echo $hello, $world
```

Si vous souhaitez concaténer une variable avec une chaîne de caractère il vous faudra impérativement séparer la variable de la chaîne à l'aide du point et d'encadrer la chaîne de caractère à l'aide des guillemets.
Si vous souhaitez intégrer une variable à l'intérieur d'une chaîne de caractère unique c'est également possible de la manière suivante:

```php
echo "Hello {$world}";
```

### Opérateurs arithmétiques
Opérateurs de base, similaire au JS avec l'ajout de l'opérateur exponentiel:

- **+** ->	Addition
- **–**	-> Soustraction
- **\*** ->	Multiplication
- **/** ->	Division
- **%** ->	Modulo (reste d’une division euclidienne)
- **\*\***	Exponentielle (élévation à la puissance d’un nombre par un autre)

### Opérateurs d'affectation

Très similaire au JS :

- **.=**	-> Concatène puis affecte le résultat
- **+=**	-> Additionne puis affecte le résultat
- **-=**	-> Soustrait puis affecte le résultat
- **\*=**	-> Multiplie puis affecte le résultat
- **/=**	-> Divise puis affecte le résultat
- **%=**	-> Calcule le modulo puis affecte le résultat
- **\*\*=**	-> Élève à la puissance puis affecte le résultat

### Opérateurs de comparaison

Toujours similaire au JS:

- **==**	-> Permet de tester l’égalité sur les valeurs
- **===** ->	Permet de tester l’égalité en termes de valeurs et de types = strictement égal 
- **!=**	 -> Permet de tester la différence en valeurs
- **<>**	-> Permet également de tester la différence en valeurs
- **!==**	-> Permet de tester la différence en valeurs ou en types
- **<**  ->	Permet de tester si une valeur est strictement inférieure à une autre
- **>**	 -> Permet de tester si une valeur est strictement supérieure à une autre
- **<=** ->	Permet de tester si une valeur est inférieure ou égale à une autre
- **>=**	-> Permet de tester si une valeur est supérieure ou égale à une autre

### Opérateurs logiques

De la même manière qu'en Javascript:

- **AND**	-> Renvoie true si toutes les comparaisons valent true
- **&&**	-> Renvoie true si toutes les comparaisons valent true
- **OR**	-> Renvoie true si une des comparaisons vaut true
- **||**	-> Renvoie true si une des comparaisons vaut true
- **XOR**	-> Renvoie true si une des comparaisons exactement vaut true
- **!**	 -> Renvoie true si la comparaison vaut false (et inversement)

## 7. Include et Require

Permet l'importation de fichier au sein d'un autre document PHP. Include et Require font basiquement la même chose. Cependant: require requiert strictement l'existence du fichier pour fonctionner, si le fichier est introuvable il renverra une erreur fatale et bloquera le script, contrairement au include qui lui continuera d'executer le script sans renvoyer d'erreur.

Par exemple: vous souhaitez insérer le même menu dans chacune de vos pages PHP. Vous allez donc créer un fichier menu.php et ensuite l'insérer d

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Cours PHP & MySQL</title>
        <meta charset="utf-8">
        <link rel="stylesheet" href="cours.css">
    </head>
    
    <body>
        <h1>Titre principal</h1>
        <?php
            echo '<h2>Menu inclus avec include</h2> <br>';
            include 'menu.php';
            
            echo '<h2>Menu inclus avec require</h2> <br>';
            require 'menu.php';
        ?>
        <p>Un paragraphe</p>
    </body>
</html>
```

## 8. Les conditions

Il existe un panel de conditions en PHP:

De la même manière qu'en JS, mais avec quelques variantes.

1. If peut exister seul
2. If...else fait également acte de présence. 
3. If... elseif... else également.
4. Les opérateurs ternaires et la fusion null
5. L'instruction switch

1. if: Syntaxe:

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Cours PHP & MySQL</title>
        <meta charset="utf-8">
        <link rel="stylesheet" href="cours.css">
    </head>
    
    <body>
        <h1>Titre principal</h1>
        <?php
            $x = 4; //On affecte la valeur 4 à $x
            $y = 2; //On affecte la valeur 2 à $y
            
            if($x > 1){
                echo '$x contient une valeur supérieure à 1';
            }
            
            if($x == $y){
                echo '$x et $y contiennent la même valeur';
            }
        ?>
        <p>Un paragraphe</p>
    </body>
</html>
```

**Output dans le html**: $x contient une valeursupérieur à 1

2. if...else: syntaxe

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Cours PHP & MySQL</title>
        <meta charset="utf-8">
        <link rel="stylesheet" href="cours.css">
    </head>
    
    <body>
        <h1>Titre principal</h1>
        <?php
            $x = 4; //On affecte la valeur 4 à $x
            $y = 2; //On affecte la valeur 2 à $y
            
            if($x > 1){
                echo '$x contient une valeur stric. supérieure à 1 <br>';
            }else{
                echo '$x contient une valeur inférieure ou égale à 1 <br>';
            }
            
            if($x == $y){
                echo '$x et $y contiennent la même valeur <br>';
            }else{
                echo '$x et $y contiennent des valeurs différentes <br>';
            }
        ?>
        <p>Un paragraphe</p>
    </body>
</html>
```

**Output HTML**: $x contient une valeur strictement supérieure à 1,$x et $y contiennent des valeurs différentes

3. if...elseif...else: syntaxe

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Cours PHP & MySQL</title>
        <meta charset="utf-8">
        <link rel="stylesheet" href="cours.css">
    </head>
    
    <body>
        <h1>Titre principal</h1>
        <?php
            $x = 4; //On affecte la valeur 4 à $x
            $y = 2; //On affecte la valeur 2 à $y
            
            if($x > 1){
                echo '$x contient une valeur stric. supérieure à 1 <br>';
            }elseif($x == 1){
                echo '$x contient la valeur 1 <br>';
            }else{
                echo '$x contient une valeur stric. inférieure à 1 <br>';
            }
            
            if($x == $y){
                echo '$x et $y contiennent la même valeur <br>';
            }elseif($x < $y){
                echo '$x contient une valeur stric. inférieure à $y <br>';
            }elseif($x > $y){
                echo '$x contient une valeur stric. supérieure à $y <br>';
            }else{
                echo 'Les valeurs de $x et $y n\'ont pas pu être comparées';
            }
        ?>
        <p>Un paragraphe</p>
    </body>
</html>
```

**Output HTML:**

$x contient une valeur stric. supérieure à 1
$x contient une valeur stric. supérieur à $y

4. Les opérateurs ternaires

Une condition ternaire est en réalité une condition if...else condensée sur une ligne
Les opérateurs ternaires existent également en Javascript, je vous conseille de vous renseigner dessus, vous risquez d'y être confronté lors de votre stage, souvent utilisées par les mediors et seniors les plus aguêris 

- La priorité des opérateurs:

Comme en math (PEMDAS) il existe une priorité aux opérateurs, elle décrit la priorité de l'opérateur sur l'opérande, où doit il être positionné vis à vis de cette opérande: 

Par exemple:

L'opérateur d'incrémentation sera associé à droite de l'opérande

- **	-> associé à droite
- ++ (incrémentation), -- (décrémentation)	-> associé à droite
- !	-> associé à droite
- *, /, %	-> associé à gauche
- +, -, .	-> associé à gauche
- <, <=, >, >=	-> associé à non-associatif
- ==, ===, !=, !==, <>, <=>	-> associé à non-associatif
- &&	-> associé à gauche
- ||	-> associé à gauche
- ? : (ternaire)	-> associé à gauche
- =, +=, -=, *=, /=, %=, **=, .=	-> associé à droite
- AND	-> associé à gauche
- XOR	-> associé à gauche
- OR	-> associé à gauche

Exemple:

```html 
<!DOCTYPE html>
<html>
    <head>
        <title>Cours PHP & MySQL</title>
        <meta charset="utf-8">
        <link rel="stylesheet" href="cours.css">
    </head>
    
    <body>
        <h1>Titre principal</h1>
        <?php
            $x = 4; //On affecte la valeur 4 à $x
            $y = -12; //On affecte la valeur -12 à $y
            
            if(!$x >= 0 AND !$y >= 0){
                echo 'Ce texte est toujours affiché !<br>';
            }
            
            if(!($x >= 0) AND !($y >= 0)){
                echo 'Ce texte s\'affiche uniquement si $x et $y contiennent
                toutes les deux une valeur stric. négative <br>';
            }
            
             if(!($x >= 0 AND $y >= 0)){
                echo 'Soit $x contient une valeur stric. négative, soit $y
                contient une valeur stric. négative, soit les deux variables
                contiennent une valeur stric. négative';
            }
        ?>
        <p>Un paragraphe</p>
    </body>
</html>
```

**Output HTML**: 
Ce texte est toujours affiché!
Soit $x contient une valeur strictement négative, soit $y contient une valeur stric. négative, soit les deux variables continnent une valeur strict. négative.

- **La syntaxe de l'opérateur ternaire:**

```php 
$x >= 0 ?: '$x stocke un nb négatif';
```

Est équivalent à:

```php 
if($x >= 0){
                echo ($x >= 0).'<br>';
            }else{
                echo '$x stocke un nombre négatif<br>';
            }
```
On le lit donc de cette façon **$x est il inférieur ou égal à 0? Si l'interrogation renvoit "true" alors j'imprime '$x stocke un nb négatif'**.

- **L'opérateur fusion null**

Il ressemble à l'opérateur ternaire, utilise l'opérateur **??** qui test une condition, si la valeur renvoyée est NULL alors un bout de code est executé sinon il renvoit la valeur de la condition. 
On peut l'imaginer utile en cas de connexion utilisateur, existe t il déjà un token d'identification? Si la valeur renvoyée est null alors je renvois l'utilisateur vers la page de connexion, sinon je peux utiliser le token pour charger les données de mon utilisateur et afficher son profil à l'écran.

```php
$x  = 4;
$y = NULL;

$resultatx = $x ?? 'NULL';
$resultaty = $y ?? 'NULL';

echo '$x contient ' .$resultatx. '<br>
    $y contient ' .$resultaty. '<br>

```

**L'output HTML:** $x contient 4, $y contient null

- **L'instruction switch**

Très semblable au JS, permet d'exécuter un code en fonction de la valeur d'une variable et donc de gérer autant de cas que souhaité

```php
            $x = 2; 
            
            switch($x){
                case 0:
                    echo '$x stocke la valeur 0';
                    break;
                case 1:
                    echo '$x stocke la valeur 1';
                    break;
                case 2:
                    echo '$x stocke la valeur 2';
                    break;
                case 3:
                    echo '$x stocke la valeur 3';
                    break;
                case 4:
                    echo '$x stocke la valeur 4';
                    break;
                default:
                    echo '$x ne stocke pas de valeur entre 0 et 4';
            }
```

**Output HTML**: $x stocke la valeur 2

## 9. Les boucles:

Tout comme en JS:

- La boucle while (« tant que ») ;
- La boucle do… while (« faire… tant que ») ;
- La boucle for (« pour ») ;
- La boucle foreach (« pour chaque ») ;

**Les opérateurs d'incrémentations et de décrémentations:**

ATTENTION l'ordre d'affectation est à respecter pour le bon fonctionnement de vos boucles: 

- **++$x**	-> Pré-incrémentation : incrémente la valeur contenue dans la variable $x, puis retourne la valeur incrémentée

- **$x++**	-> Post-incrémentation : retourne la valeur contenue dans $x avant incrémentation, puis incrémente la valeur de $x

- **--$x**	-> Pré-décrémentation : décrémente la valeur contenue dans la variable $x, puis retourne la valeur décrémentée

- **$x--**	-> Post-décrémentation : retourne la valeur contenue dans $x avant décrémentation, puis décrémente la valeur de $x


- **La boucle while**

```php
            $x = 0;
            
            while($x <= 10){
                echo '$x contient la valeur ' .$x. '<br>';
                $x++;
            }
```

Affichera chaque valeur de 0 à 10 inclus

- **La boucle do...while**

```php
$x = 0;
            $y = 20;
            
            do{
                echo '$x contient la valeur ' .$x. '<br>';
                $x++;
            }while($x <= 5);
            
            do{
                echo '$y contient la valeur ' .$y. '<br>';
                $y++;
            }while($y <= 5);
```
La première boucle imprimera les valeurs de 0 à 5 inclus
La seconde n'imprimera que la valeur de $y: 20

- **La boucle for**

```php
            for($x = 0; $x <= 5; $x++){    
                echo '$x contient la valeur ' .$x. '<br>';
            }
```
Même format qu'en JS, la boucle imprimera les valeurs de 0 à 5 inclus

- **La boucle foreach**

Comme en JS elle est prévue pour tourner sur des tableaux:

Nous ne l'avons pas encore abordé mais 

```php 
$prenoms = ['Mathilde', 'Pierre', 'Amandine', 'Florian'];
            
            //On rajoute une valeur à $prenoms et on lui associe la clef 8
            $prenoms[8] = 'Lisa';  
            
            $taille = count($prenoms);
            for($i = 0; $i < $taille; $i++){
                $p .= $prenoms[$i]. ', ';
            }
            echo $p. '<br><br>';
            foreach ($prenoms as $valeurs){
                $resultat .= $valeurs. ', ';
            }
            echo $resultat;
```

La boucle for se base sur la taille du tableau comptée et contenue dans la variable $taille, on voit que Lisa est attribué à l'index 8 mais qu'il n'y a que 5 éléments dans mon tableau. La variable taille aura donc comme valeur 5. La boucle for n'affichera donc jamais l'index 8 'lisa'

La boucle foreach par contre prend en compte chaque valeurs du tableau prénom grâce au mot clé "as": et affichera: Mathilde, Pierre, Amandine, Florian, Lisa

## 10. Les fonctions

Tout comme en JS il existe un pannel de fonction déjà programmées en PHP.
Je vous laisse les consulter au moyen de la documentation.

Voici la syntaxe pour déclarer une fonction simple:

```php

function hello() {
    echo "Hello World";
}
```
Une fonction de rappel:

```php
function hello() 
{
  function world() 
  {
    echo "Je n'existe pas tant que hello() n'est pas appelé.\n";
  }
}
hello();
world();
```
Une fonction récursive (une fonction qui s'appelle au sein d'elle même):

```php 
function recursion($a)
{
    if ($a < 20) {
        echo "$a\n";
        recursion($a + 1);
    }
}
```
## 11. La balise PHP

Nous ne l'avons pas encore abordé.
Mais comment intègre-t-on du PHP à notre travail?
Contrairement au JS, HTML et PHP se mélangent dans le même fichier.
Votre index.html va devenir un index.php afin d'être lu et reconnu en tant que tel par votre navigateur.

Vous devez donc intégrer à un document HTML du contenu php via une balise.

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Cours PHP & MySQL</title>
        <meta charset="utf-8">
        <link rel="stylesheet" href="cours.css">
    </head>
    
    <body>
        <h1>Titre principal</h1>
        <?php
            echo '<h2>Menu inclus avec include</h2> <br>';
            include 'menu.php';
            
            echo '<h2>Menu inclus avec require</h2> <br>';
            require 'menu.php';
        ?>
        <p>Un paragraphe</p>
    </body>
</html>
```
```php
//Balise ouvrante
<?php
//votre code ici
//balise fermante
?>
```

## 11. Les formulaires

Pour ce point je vous laisse vous documenter via le cours de Pierre Giraud très complet:

https://www.pierre-giraud.com/php-mysql-apprendre-coder-cours/recuperer-manipuler-donnee-formulaire/

