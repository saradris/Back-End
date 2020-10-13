# Introduction au langage de base de donnée SQL et à mySQL

## Table des matières:

1. Qu'est ce qu'une base de donnée
2. Qu'est ce que le SQL
3. Qu'est ce que MySQL
4. PHPmyadmin
5. Structure de base de données
6. La connexion à la DB
7. La création de la DB et création de tables/ colonnes
9. Qu'est ce qu'une query?

## 1. Qu'est ce qu'une base de donnée

Une base de donnée (ou Data Base, DB) est l'élément collecteur des données de votre application.
C'est la DB qui est le contenant pour toutes les informations nécessaire au bon fonctionnement de votre site web.
Données d'utilisateurs, inventaire de l'e-shop, to-do list, tâches, articles de blogs, peu importe, toute information devant être stockées au sein du serveur pour permettre le bon fonctionnement de votre site / application.

Une base de donnée porte un nom, contient des tables.
Par exemple dans le cadre d'une to-do list nous pouvons imaginer une table contenant les informations de connexion de l'utilisateur. Une table contenant les listes des utilisateurs, une table contenant les tâches relatives à l'utilisateur et à la liste auxquelles elles appartiennent.

Ces tables contiennent des colonnes, chaque colonnes correspond à la "clé" et chaque rangée à la "valeur" de cette clé.
Par exemple vous pourriez avoir une table contenant une colonne "user_name", la valeur serait le nom d'utilisateur enregistré par l'utilisateur: par exemple SamGrath

## 2. Qu'est ce que le SQL

Le SQL est un langage permettant d'interagir avec la DB. SQL tiens pour Structured **Query** Language, ou langage de requête structuré.
Grâce au SQL le back-end peut aisément créer des requêtes qui seront utilisées par les appels du front-end et modifier la base de donnée.

## 3. Qu'est ce que MySQL

MySQL n'est autre qu'un **programme** permettant de gérer ses bases de données. Il en existe tout un panel également, tous sur le même principe.  MySQL sert à envoyer des requêtes écrites en SQL standard la base de données.


## 4. Qu'est ce que PHPmyAdmin

Il s'agit d'un **logiciel**, d'une interface graphique permettant de gérer les bases de données, de les créer, supprimer, ajouter des tables, des colones, les modifier.
Vous pouvez ajouter manuellement des données, attention s'agit d'un ajout "statique" un ajout "dynamique" implique un appel de l'utilisateur vers le back-end qui renverra la requête à la DB.

## 5. Structure de base de données

Vous pouvez lire attentivement cette partie du cours de Pierre Giraud qui vous expliquera les principes de base d'une structure
https://www.pierre-giraud.com/php-mysql-apprendre-coder-cours/structure-base-donnee-mysql-phpmyadmin/

### Schéma de base de données

Pour faire suite au cours de Pierre Giraud je vous conseille ces chapitres d'openclassroom:
https://openclassrooms.com/fr/courses/4055451-modelisez-et-implementez-une-base-de-donnees-relationnelle-avec-uml/4458843-modelisez-dans-le-detail-votre-schema-de-base-de-donnees

## 6. Connexion à la DB

La connexion à la base de donnée se fait depuis le PHP.
Comme vous le savez il existe des extensions au langage permettant plus de fonctionnalités de la part.
Pour vous connecter à la base de donnée vous aurez le choix entre deux API/Extension (pour rappel une API est une interface de programmation):

- L'extension PDO (Php data object)
- L'extension Mysqli (mysql improved)

La différence entre les deux: Mysqli ne permet de fonctionner uniquement qu'avec du SQL
PDO prend en charge tout autre langage / système de gestion de base de donnée
Dans notre cas nous n'allons explorer **uniquement** la connexion **PDO**:

Voici les explications tirées du cours de Pierre Giraud:

## Connexion au serveur avec PDO

Pour se connecter en utilisant PDO, nous allons devoir instancier la classe PDO en passant au constructeur la source de la base de données (serveur + nom de la base de données) ainsi qu’un nom d’utilisateur et un mot de passe.

```php
<!DOCTYPE html>
<html>
    <head>
        <title>Cours PHP / MySQL</title>
        <meta charset="utf-8">
        <link rel="stylesheet" href="cours.css">
    </head>
    <body>
        <h1>Bases de données MySQL</h1>  
        <?php
            $servername = 'localhost';
            $username = 'root';
            $password = 'root';
            
            //On établit la connexion
            $conn = new PDO("mysql:host=$servername;dbname=bddtest", $username, $password);
        ?>
    </body>
</html>
```

Vous pouvez déjà remarquer ici que pour se connecter à une base de données avec PDO, vous devez passer son nom dans le constructeur de la classe PDO. Cela implique donc qu’il faut que la base ait déjà été créée au préalable (avec phpMyAdmin par exemple) ou qu’on la crée dans le même script.

Notez également qu’avec PDO il est véritablement indispensable que votre script gère et capture les exceptions (erreurs) qui peuvent survenir durant la connexion à la base de données.

En effet, si votre script ne capture pas ces exceptions, l’action par défaut du moteur Zend (plus de détail sur le moteur ici) va être de terminer le script et d’afficher une trace. Cette trace contient tous les détails de connexion à la base de données (nom d’utilisateur, mot de passe, etc.). Nous devons donc la capturer pour éviter que des utilisateurs malveillants tentent de la lire.

Pour faire cela, nous allons utiliser des blocs try et catch.
```php
<!DOCTYPE html>
<html>
    <head>
        <title>Cours PHP / MySQL</title>
        <meta charset="utf-8">
        <link rel="stylesheet" href="cours.css">
    </head>
    <body>
        <h1>Bases de données MySQL</h1>  
        <?php
            $servername = 'localhost';
            $username = 'root';
            $password = 'root';
            
            //On essaie de se connecter
            try{
                $conn = new PDO("mysql:host=$servername;dbname=bddtest", $username, $password);
                //On définit le mode d'erreur de PDO sur Exception
                $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
                echo 'Connexion réussie';
            }
            
            /*On capture les exceptions si une exception est lancée et on affiche
             *les informations relatives à celle-ci*/
            catch(PDOException $e){
              echo "Erreur : " . $e->getMessage();
            }
        ?>
    </body>
</html>
```

Ici, nous utilisons également la méthode setAttribute() en lui passant deux arguments PDO::ATTR_ERRMODE et PDO::ERRMODE_EXCEPTION.

La méthode setAttribute() sert à configurer un attribut PDO. Dans ce cas précis, nous lui demandons de configurer l’attribut PDO::ATTR_ERRMODE qui sert à créer un rapport d’erreur et nous précisons que l’on souhaite qu’il émette une exception avec PDO::ERRMODE_EXCEPTION.

Plus précisément, en utilisant PDO::ERRMODE_EXCEPTION on demande au PHP de lancer une exception issue de la classe PDOException (classes étendue de Exception) et d’en définir les propriétés afin de représenter le code d’erreur et les informations complémentaires.

Ensuite, nous n’avons plus qu’à capturer cette exception PDOException et à afficher le message d’erreur correspondant. C’est le rôle de notre bloc catch.

 

## Fermer la connexion à la base de données

Une fois la connexion à la base de données ouverte, celle-ci reste active jusqu’à la fin de l’exécution de votre script.

Si on utilise PDO, il faudra détruire l’objet représentant la connexion et effacer toutes ses références. Nous pouvons faire cela en assignant la valeur NULL à la variable gérant l’objet.

```php
try{
    $conn = new PDO("mysql:host=$servername;dbname=bddtest", $username, $password);
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    echo "Connexion Réussie";
}
catch(PDOException $e){
    echo "Erreur:" $->getMessage();
}
// Suite du script
//Une fois le script entièrement lu: terminer la connexion
$conn = null;
```

## 7. Création de la base de donnée

Maintenant que vous êtes connecté, vous pouvez créer votre première base de donnée et votre première table.
Puisque nous avons vu comment nous connecter via la PDO nous allons voir comment créer un DB grâce à cette même API

```php
//définition des variable permettant la connexion à la DB
            $servname = 'localhost';
            $dbname = 'pdodb';
            $user = 'root';
            $pass = 'root';
//try catch= essaie / attrape, on test si la connexion au serveur a été réussie, et la table bien créée, si oui on renvois un echo pour prévenir que la table a bien été créée, sinon on renvois une erreur et la fonction getMessage permet d'afficher le message d'erreur à l'écran  
            try{
                // On lance la connexion à la PDO
                $dbco = new PDO("mysql:host=$servname;dbname=$dbname", $user, $pass);
                $dbco->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
                //On crée la table et ses colonnes, on leur spécifie quelle est la clé primaire (ID, doit être utilisé une seule fois) et quelles sont les types valeurs attendues par les autres champs, NOT NULL permet de spécifier que le champs doit être spécifiquement rempli pour que la requête soit valide.
                $sql = "CREATE TABLE Clients(
                        Id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
                        Nom VARCHAR(30) NOT NULL,
                        Prenom VARCHAR(30) NOT NULL,
                        Adresse VARCHAR(70) NOT NULL,
                        Ville VARCHAR(30) NOT NULL,
                        Codepostal INT UNSIGNED NOT NULL,
                        Pays VARCHAR(30) NOT NULL,
                        Mail VARCHAR(50) NOT NULL,
                        DateInscription TIMESTAMP,
                        UNIQUE(Mail))";
                
                $dbco->exec($sql);
                echo 'Table bien créée !';
            }
            
            catch(PDOException $e){
              echo "Erreur : " . $e->getMessage();
            }
```
## 9. Qu'est ce qu'une query?

Une query est une instruction donnée en sql pour ajouter, supprimer, modifier, rechercher dans la base de données une donnée ou un ensemble de donnée.
La synthaxe est plutôt intuitive, voici la théorie tirée du cours de Pierre Giraud:

1. Insérer des données: https://www.pierre-giraud.com/php-mysql-apprendre-coder-cours/inserer-donnee-table-base/
2. Préparer ses requêtes grâce à la PDO: https://www.pierre-giraud.com/php-mysql-apprendre-coder-cours/requete-preparee/
3. Modifier des données: https://www.pierre-giraud.com/php-mysql-apprendre-coder-cours/modifier-donnee-table-base/
4. Supprimer des données: https://www.pierre-giraud.com/php-mysql-apprendre-coder-cours/supprimer-donnee-table-base/
5. Sélectionner de manière simple: https://www.pierre-giraud.com/php-mysql-apprendre-coder-cours/selectionner-donnee-table/
6. Utiliser des critères spécifiques pour la sélection: https://www.pierre-giraud.com/php-mysql-apprendre-coder-cours/critere-selection-where/