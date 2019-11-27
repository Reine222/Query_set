# Query_set
les requetes

# Travailler avec des données

L'API QuerySet de Django fournit un large éventail de méthodes et de fonctions permettant de travailler avec des données. Dans cette section du chapitre, nous allons examiner toutes les méthodes, recherches de champs et fonctions d'agrégation QuerySet courantes.

# filter() :
Permet de filtrer par les paramètres de recherche donnés. Plusieurs paramètres sont joints par des virgules ",".
# exemples :





# exclude() :
Permet de filtrer par objets qui ne correspondent pas aux paramètres de recherche donnés.
# exemples :




# annotate() :
Permet d'annotez chaque objet dans le QuerySet. Les annotations peuvent être des valeurs simples, une référence de champ ou une expression agrégée.
# exemples :





# order_by() :
Permet de modifier le classement par défaut du QuerySet.
# exemples :



# reverse() :
Permet de renverser l'ordre par défaut du QuerySet.
# exemples :






# distinct() :
Permet d'effectuer une SELECTION DISTINCTE de requête pour éliminer les lignes en double
# exemples :






# values() :
Permet de renvoiyer des dictionnaires au lieu d'instances de modèles.
# exemples :





# values_list() :
Permet de retourner des tuples au lieu d'instances de modèle
# exemples :




# dates() :
Permet de renvoiyer un QuerySet contenant toutes les dates disponibles dans la plage de dates spécifiée.
# exemples :





# datetimes() :
Permet de renvoiyer un QuerySet contenant toutes les dates disponibles dans la plage de dates et d'heures spécifiée.
# exemples :
