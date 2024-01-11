





### Etape 6 : Appel de l'API MeteoConcept

### Faut-il une clé API pour appeler MeteoConcept ?
Oui, une clé API est nécessaire pour accéder aux services de MeteoConcept. 
Voici ma clé API pour météo-concept : 
meteoConceptApiKey=d5fdc1814b5510362df6eb8e8a65444ca8695c17118ad22be66ac04f97a8fc7f

### Quelle URL appeler ?
L'URL à utiliser pour obtenir la longitude et la latitude est : 
etalabApiUrl = "https://api-adresse.data.gouv.fr/search/?q=" + addressForm.getAddress(); 

L'URL à utiliser pour obtenir les prévisions météorologiques quotidiennes est : 
meteoConceptApiUrl = "https://api.meteo-concept.com/api/forecast/daily?token="
              + meteoConceptApiKey  + "&latlng=" + latitude + ","+ longitude;

### Quelle méthode HTTP utiliser ?
Utilisez la méthode HTTP GET pour récupérer les données météorologiques.
Response response = restTemplate.getForObject(meteoConceptApiUrl, Response.class);

### Comment passer les paramètres d'appels ?
Les paramètres requis pour la requête GET sont :
- `token`: Votre clé API obtenue lors de l'inscription.
- `longitude`: La longitude de l'emplacement souhaité.
- `latitude`: La latitude de l'emplacement souhaité.

Exemple d'URL avec paramètres :
meteoConceptApiUrl = "https://api.meteo-concept.com/api/forecast/daily?token="
              + meteoConceptApiKey  + "&latlng=" + latitude + ","+ longitude;

### Où est l'information dont j'ai besoin dans la réponse :
Pour afficher la température et la météo du lieu visé par les coordonnées GPS, 
on peut utiliser : 

        double tmin = response.getForecast().get(0).getTmin();
        double tmax = response.getForecast().get(0).getTmax();
        double weather = response.getForecast().get(0).getWeather();
        double wind10m = response.getForecast().get(0).getWind10m();
      
puis faire une methode dans la classe Forecast permettant de 
calculer la température ressentie : 

        double temperature = Forecast.calculateTemperature(tmin,tmax,wind10m);








### Description Succincte des dépendances dans pom.xml 

1. spring-boot-starter-data-jpa:
   Description : Starter pour l'utilisation de Spring Data JPA, qui simplifie l'accès
    et la manipulation de bases de données relationnelles en utilisant les concepts 
    de JPA (Java Persistence API).
   
2. h2:
   Description : Base de données relationnelle en mémoire, souvent utilisée pour 
   le développement et les tests. Cette dépendance est utilisée en tant que dépendance 
   de portée "runtime", ce qui signifie qu'elle n'est nécessaire qu'à l'exécution, 
   pas à la compilation.

3. spring-boot-starter-thymeleaf:
   Description : Starter pour l'utilisation de Thymeleaf, un moteur de template pour 
   la création de vues web dans les applications Spring Boot.

4. tomcat-embed-jasper:
   Description : Intégration de Tomcat et de Jasper (un moteur de compilation de JSP) 
   pour la prise en charge du rendu des pages JSP dans les applications Spring Boot.

5. spring-boot-starter-web:
   Description : Starter pour le développement d'applications web Spring Boot, incluant
    des fonctionnalités telles que les contrôleurs, les vues et la gestion des ressources statiques.

6. mysql-connector-java:
   Description : Connecteur JDBC pour MySQL, permettant à une application Java de 
   se connecter à une base de données MySQL.
    
7. spring-boot-starter-test:
   Description : Starter pour l'écriture de tests unitaires et d'intégration dans 
   les applications Spring Boot. Il inclut des bibliothèques telles que JUnit et Spring Test.



Ces dépendances couvrent un large éventail de fonctionnalités, allant de l'accès aux bases 
de données, à la création de vues web, en passant par le développement et les tests. 
L'utilisation de WebJars permet d'inclure facilement des bibliothèques JavaScript 
et CSS dans mon projet.

### Paramétrage de l'URL d'appel /greeting :
   - L'URL d'appel /greeting est paramétrée avec l'annotation `@GetMapping("/greeting")` 
   qui précède la méthode `greeting` du contrôleur. Cela signifie que lorsque l'application 
   reçoit une requête GET à l'URL /greeting, elle appelle la méthode `greeting` de ce contrôleur.

### Choix du fichier HTML à afficher :
   - Le choix du fichier HTML à afficher est déterminé par la valeur retournée par 
   la méthode `greeting`. Dans ce cas, la méthode retourne la chaîne "greeting". 
   Dans Spring Boot, cela est interprété comme le nom de la vue à afficher. Par défaut, 
   Spring Boot recherche un fichier HTML avec le même nom que la vue dans le dossier 
   des templates (souvent `src/main/resources/templates`). Ainsi, le fichier HTML 
   correspondant est "greeting.html".

### Envoi du nom pour saluer avec le second lien :
   - Le nom à qui dire bonjour est envoyé en tant que paramètre de requête dans l'URL. 
   Cela est géré par le paramètre `@RequestParam(name="nameGET", required=false, defaultValue="World") String nameGET`
   de la méthode `greeting`. Ce paramètre récupère la valeur du paramètre de requête "nameGET".
   Si ce paramètre n'est pas fourni dans l'URL, il prend la valeur par défaut "World". 
   La méthode ajoute ensuite ce nom au modèle (`Model`) avec la ligne `model.addAttribute("nomTemplate", nameGET)`, 
   ce qui le rend disponible pour être utilisé dans le fichier HTML associé.




### Utilité de @Autowired

@Autowired est utilisée en Spring pour effectuer l'injection de dépendances automatique. 
Elle permet à Spring de résoudre et d'injecter automatiquement les dépendances dans 
les composants gérés par le conteneur Spring, tels que les contrôleurs, les services etc.

