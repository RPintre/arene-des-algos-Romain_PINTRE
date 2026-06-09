Utilisation de different modèle de ML pour arriver a une arène de modèle qui s'affonte et en sortir des résultats / conclusions

# Jour 2 phase 2
## Reparation de `TotalCharges`

J'ai choisi une strategie hybride: supprimer les lignes si la proportion de valeurs manquantes est inferieure a 1%, sinon imputer avec la mediane.

Pourquoi :
- dans ce jeu de donnees, il n'y a que 11 valeurs manquantes sur 7043 lignes, donc le taux reste tres faible ;
- si le manque est marginal, supprimer les lignes evite d'introduire une valeur artificielle ;
- si le manque devient plus important, l'imputation permet de conserver la taille du dataset ;
- la mediane reste un bon choix car elle est plus robuste que la moyenne si la variable est asymetrique.

En resume, le code privilegie la suppression quand la perte d'information est minime, et bascule vers l'imputation quand il faut proteger davantage de donnees.