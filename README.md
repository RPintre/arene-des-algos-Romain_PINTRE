Utilisation de different modèle de ML pour arriver a une arène de modèle qui s'affonte et en sortir des résultats / conclusions

# Jour 2 
## phase 2
### Reparation de `TotalCharges`

J'ai choisi une strategie hybride: supprimer les lignes si la proportion de valeurs manquantes est inferieure a 1%, sinon imputer avec la mediane.

Pourquoi :
- dans ce jeu de donnees, il n'y a que 11 valeurs manquantes sur 7043 lignes, donc le taux reste tres faible ;
- si le manque est marginal, supprimer les lignes evite d'introduire une valeur artificielle ;
- si le manque devient plus important, l'imputation permet de conserver la taille du dataset ;
- la mediane reste un bon choix car elle est plus robuste que la moyenne si la variable est asymetrique.

En resume, le code privilegie la suppression quand la perte d'information est minime, et bascule vers l'imputation quand il faut proteger davantage de donnees.

### Phase 3 - `encoder_features`

Cette étape transforme toutes les colonnes catégorielles en variables numériques pour pouvoir entraîner un modèle.

J'ai séparé les colonnes catégorielles en deux groupes :

- les colonnes binaires, encodées simplement en `0/1`
- les colonnes nominales, encodées en One-Hot

### Colonnes binaires

Les variables binaires comme `Yes/No` sont encodées en `0/1` car il n'y a que deux modalités et l'information est naturellement binaire.

### Colonnes nominales

Les colonnes nominales sont encodées en One-Hot pour éviter d'imposer un faux ordre numérique entre les catégories.

### Cas de `Contract`

`Contract` contient trois modalités : `Month-to-month`, `One year` et `Two year`.  
Je la traite comme une variable nominale et non comme une variable ordinale, car je ne veux pas imposer au modèle un ordre numérique artificiel entre ces catégories.

### Cas de `customerID`

`customerID` est supprimée avant l'encodage, car c'est un identifiant unique et non une variable prédictive.  
Si on l'encodait par erreur en One-Hot, on créerait une colonne par client, ce qui provoquerait une explosion du nombre de dimensions sans apporter d'information utile. Ce qui ferait dont 7043 colonnes en plus.
