# Query_set
les requetes

# Travailler avec des données

L'API QuerySet de Django fournit un large éventail de méthodes et de fonctions permettant de travailler avec des données. Dans cette section du chapitre, nous allons examiner toutes les méthodes, recherches de champs et fonctions d'agrégation QuerySet courantes.
#
#


# filter() :
Permet de filtrer par les paramètres de recherche donnés. Plusieurs paramètres sont joints par des virgules ",".
# exemples : 
# filter() retourne un ensemble de données ayant status=True ; 

      from events.models import Venue
      Venue.objects.filter(status=True)
      <QuerySet [<Venue: West Park>, <Venue: North Stadium>, <Venue: East Park>]>

#




# exclude() :
Permet de filtrer par objets qui ne correspondent pas aux paramètres de recherche donnés.
# exemple :  
# exclude() retournera un ensemble de requêtes d'objets qui ne correspondent pas aux paramètres de recherche donnés,
      from events.models import Venue
      Venue.objects.exclude(name="South Stadium")
      <QuerySet [<Venue: West Park>, <Venue: North Stadium>, <Venue: East Park>]>

#


# annotate() :
Permet d'annotez chaque objet dans le QuerySet. Les annotations peuvent être des valeurs simples, une référence de champ ou une expression agrégée.
# exemples : 
# Les annotations peuvent être des valeurs simples, une référence de champ ou une expression agrégée. Par exemple, utilisons la Countfonction d'agrégation de Django pour annoter notre modèle d'événement avec un total de tous les utilisateurs participant à chaque événement:

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
# exemples : 
# order_by()modifie l'ordre par défaut du QuerySet. Les paramètres de fonction sont les champs de modèle à utiliser pour ordonner le QuerySet. La commande peut être à un seul niveau:

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
# exemples : 
# reverse() inverse le classement par défaut du QuerySet(suivant l'exemple precedent) :
      from events.models import Event
      Event.objects.all().reverse()                     
      <QuerySet [<Event: Test Event>, <Event: Club Presentation - Juniors>, <Event: Club Presentation - Seniors>, <Event: Gala Day>]>


#


# distinct() :
Permet d'effectuer une SELECTION DISTINCTE de requête pour éliminer les lignes en double
# exemples : 
# distinct() retournera les tout les données une fois sans leurs doubles

      from events.models import Event
      Event.objects.all().distinct('nom')                     
      <QuerySet [<Event: Test Event>, <Event: Club Presentation - Juniors>, <Event: Club Presentation - Seniors>, <Event: Gala Day>]>



#

# values() :
Permet de renvoiyer des dictionnaires au lieu d'instances de modèles.
# exemple : 
#  values() retourne les dictionnaires Python, au lieu d'un objet QuerySet:
      from events.models import Event
      Event.objects.values()       
      <QuerySet [{'id': 1, 'name': 'Test Event', 'event_date': datetime.datetime(2019, 8, 25, 22, 42, 15, tzinfo=<UTC>), 'venue_id': 1, 'manager_id': 1, 'description': "It's all happening here!"}, {'id': 2, 'name': 'Club Presentation - Juniors', 'event_date': datetime.datetime(2019, 8, 1, 12, 0, tzinfo=<UTC>), 'venue_id': 4, 'manager_id': 2, 'description': ''}]>


# Vous pouvez également spécifier les champs que vous voulez renvoyer:
      from events.models import Event
      Event.objects.values('name','description') 
      <QuerySet [{'name': 'Test Event', 'description': "It's all happening here!"}, {'name': 'Club Presentation - Juniors', 'description': ''}]>

#

# values_list() :
Permet de retourner des tuples au lieu d'instances de modèle
# exemple : 
# values_list()est le même que values(), sauf qu'il retourne des tuples:
      from events.models import Event
      Event.objects.values_list() 
      <QuerySet [(1, 'Test Event', datetime.datetime(2019, 8, 25, 22, 42, 15, tzinfo=<UTC>), 1, 1, "It's all happening here!"), (2, 'Club Presentation - Juniors', datetime.datetime(2019, 8, 1, 12, 0, tzinfo=<UTC>), 4, 2, '')]>

# Vous pouvez également spécifier les champs à renvoyer :
      from events.models import Event
      Event.objects.values_list('name')
      <QuerySet [('Test Event',), ('Club Presentation - Juniors',)]>

#

# dates() et  datetimes() :
Permet de renvoiyer un QuerySet contenant toutes les dates disponibles dans la plage de dates et d'heures spécifiée.
# exemple : 
# Vous utilisez les méthodes dates()et datetimes()pour renvoyer des enregistrements limités dans le temps de la base de données (par exemple, tous les événements se produisant au cours d'un mois donné). Pour dates(), ces limites de temps sont year, month, weeket day. datetimes()ajoute hour, minuteet secondlimites.


      from events.models import Event
      Event.objects.dates('event_date', 'year')
      <QuerySet [datetime.date(2019, 1, 1)]>
      Event.objects.dates('event_date', 'month') 
      <QuerySet [datetime.date(2019, 8, 1)]>
      Event.objects.dates('event_date', 'week')  
      <QuerySet [datetime.date(2019, 7, 29), datetime.date(2019, 8, 5), datetime.date(2019, 8, 19)]>
      Event.objects.dates('event_date', 'day')  
      <QuerySet [datetime.date(2019, 8, 1), datetime.date(2019, 8, 10), datetime.date(2019, 8, 11), datetime.date(2019, 8, 25)]>


