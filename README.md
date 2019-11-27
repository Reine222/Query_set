# Query_set
les requetes

# Travailler avec des données

L'API QuerySet de Django fournit un large éventail de méthodes et de fonctions permettant de travailler avec des données. Dans cette section du chapitre, nous allons examiner toutes les méthodes, recherches de champs et fonctions d'agrégation QuerySet courantes.
#
#


# filter() :
Permet de filtrer par les paramètres de recherche donnés. Plusieurs paramètres sont joints par des virgules ",".
# exemples :

#




# exclude() :
Permet de filtrer par objets qui ne correspondent pas aux paramètres de recherche donnés.
# exclude() retournera un ensemble de requêtes d'objets qui ne correspondent pas aux paramètres de recherche donnés,
      from events.models import Venue
      Venue.objects.exclude(name="South Stadium")
      <QuerySet [<Venue: West Park>, <Venue: North Stadium>, <Venue: East Park>]>

#


# annotate() :
Permet d'annotez chaque objet dans le QuerySet. Les annotations peuvent être des valeurs simples, une référence de champ ou une expression agrégée.
# exemples : Les annotations peuvent être des valeurs simples, une référence de champ ou une expression agrégée. Par exemple, utilisons la Countfonction d'agrégation de Django pour annoter notre modèle d'événement avec un total de tous les utilisateurs participant à chaque événement:

      from events.models import Event
      from django.db.models import Count
      qry = Event.objects.annotate(total_attendees=Count('attendees'))
      for event in qry:
      ...     print(event.name, event.total_attendees) 
     
      Test Event 0
      Gala Day 2
      Club Presentation - Juniors 5
      Club Presentation - Seniors 3



#

# order_by() :
Permet de modifier le classement par défaut du QuerySet.
# exemples : order_by()modifie l'ordre par défaut du QuerySet. Les paramètres de fonction sont les champs de modèle à utiliser pour ordonner le QuerySet. La commande peut être à un seul niveau:

      from events.models import Event
      Event.objects.all().order_by('name')
      <QuerySet [<Event: Club Presentation - Juniors>, <Event: Club Presentation - Seniors>, <Event: Gala Day>, <Event: Test Event>]>
# Ou la commande peut être multi-niveau. Dans l'exemple suivant, les événements sont d'abord classés par date, puis par nom:

      >>> Event.objects.all().order_by('event_date','name')  
      <QuerySet [<Event: Club Presentation - Juniors>, <Event: Club Presentation - Seniors>, <Event: Gala Day>, <Event: Test Event>]>

# Par défaut, les champs QuerySet sont classés par ordre croissant. Pour trier par ordre décroissant, utilisez le signe négatif ( -) :

      >>> Event.objects.all().order_by('-name') 
      <QuerySet [<Event: Test Event>, <Event: Gala Day>, <Event: Club Presentation - Seniors>, <Event: Club Presentation - Juniors>]>

#

# reverse() :
Permet de renverser l'ordre par défaut du QuerySet.
# exemples : reverse() inverse le classement par défaut du QuerySet(suivant l'exemple precedent) :

      >>> Event.objects.all().reverse()                     
      <QuerySet [<Event: Test Event>, <Event: Club Presentation - Juniors>, <Event: Club Presentation - Seniors>, <Event: Gala Day>]>


#


# distinct() :
Permet d'effectuer une SELECTION DISTINCTE de requête pour éliminer les lignes en double
# exemples :




#

# values() :
Permet de renvoiyer des dictionnaires au lieu d'instances de modèles.
# exemples :



#

# values_list() :
Permet de retourner des tuples au lieu d'instances de modèle
# exemples :



#

# dates() :
Permet de renvoiyer un QuerySet contenant toutes les dates disponibles dans la plage de dates spécifiée.
# exemples :




#

# datetimes() :
Permet de renvoiyer un QuerySet contenant toutes les dates disponibles dans la plage de dates et d'heures spécifiée.
# exemples :
