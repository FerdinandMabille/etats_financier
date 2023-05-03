# Etats Financier des ARS

Automatisation du calcul des états-financier des ARS.

## Architecture

``` bash
_ README.md
_ .gitignore
_ etl
   |_ utilitaire
      |_ main.py
      |_ data
         |_ database
            |_ demo.db
         |_ input
            |_ CORRESP
               |_ demo.xlsx
            |_ DFAS
               |_ demo.xlsx
            |_ DGOS
               |_ demo.xlsx
            |_ DSS
               |_ demo.xlsx
            |_ FIR
               |_ demo.xlsx
            |_ FMIS
               |_ demo.xlsx
         |_ to_csv
            |_ demo.csv
         |_ output
            |_ demo.csv
      |_ modules
         |_ route_datacleaning
            |_ __pycache__
            |_ __init__.py
            |_ route_datacleaning.py
         |_ route_sqlite
            |_ __pycache__
            |_ __init__.py
            |_ query_sqlite.py
            |_ route_sqlite.py
      |_ settings
         |_ settings_demo.json
      |_ utils
         |_ __pycache__
         |_ __init__.py
         |_ utils.py
```

## Commandes

**_Pour exécuter les commandes, se rendre dans le dossier etats-financier/etl/utilitaire_**

* ```python main.py init_database``` : Initialise la base de données etats_financier.db dans _data/database_.
* ```python main.py create_csv``` : Convertit les fichiers présents au sein de _data/input_ et les enregistre sous CSV dans _data/to-csv_.
* ```python main.py load_to_db``` : Au sein de la base de données etats_financier.db, créer les tables et insères les données provenant des fichiers de _data/to-csv_.
* ```python main.py execute_sql``` : Exécute les requêtes SQL présentes au sein de _query-sqlite.py_ et enregistre le résultat des requêtes sous format CSV au sein du dossier _data/output_.
* ```python main.py clean_output``` : Uniformise les fichiers CSV présents au sein du dossier _data/output_.
* ```python main.py all``` : Effectue l'ensemble des commandes précédentes.

## Gestion des fichiers

**_Pour ajouter ou télécharger un nouveau fichier vers/depuis la VM, nécessaire d'ouvrir une fenêtre d'invite de commande_**

#### Insérer un nouveau fichier depuis une machine locale vers la VM :
Les fichiers sont à enregistrer au sein du dossier correspondant à l'origine du fichier dans __data/input__. Par exemple, les fichiers concernant le FIR sont à enregistrer au sein de __data/input/FIR__.
Si le dossier correspondant au fichier n'existe pas, se rendre dans __data/input__ et créer le nouveau dossier via la commande ```mkdir NOMDUDOSSIER```.

Commande à réaliser pour transférer un fichier du local vers la VM :
* scp /chemin/où/se/situe/le/fichier/sur/la/machine/locale/fichier.xlsx user@host:/etats_financier/etl/utilitaire/data/input/DOSSIER_CORRESPONDANT_AU_FICHIER

#### Télécharger les fichiers des résultats :
Commande à réaliser pour transférer un fichier de la VM au local :
* scp user@host:/etats_financier/etl/utilitaire/data/output/NOMDUFICHIER.csv C:\Users\prenom.nom\Documents
