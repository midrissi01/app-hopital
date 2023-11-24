<h1>Activité pratique 3</h1>
<h3>Introduction</h3>
<p>Ce rapport détaille le développement d'applications Web sécurisées à l'aide de Spring Boot et Spring Security, en mettant l'accent sur la gestion des patients. Le processus comprend la création d'un projet avec les dépendances requises, la mise en œuvre d'entités JPA pour les patients, la configuration de la persistance des données, la configuration des contrôleurs Spring MVC et la création de vues Thymeleaf. La flexibilité de se connecter à H2 ou MySQL est une caractéristique clé du projet. L'intégration de Spring Security avec trois stratégies d'authentification améliore la sécurité : InMemoryAuthentication, JdbcAuthentication et UserDetailsService. L'objectif final est de fournir une application Web entièrement fonctionnelle, adaptable et sécurisée qui utilise judicieusement les fonctionnalités fournies par Spring Boot et Spring Security.
</p>

<h3>Objectifs</h3>
<h3>Introduction</h3>
<p></p>
<p>Créer une application web JEE qui permet de gérer des patients</p>
<ol>
<li>Créer un projet spring boot avec les dépendances Web, Spring Data JPA, H2,
Lombock, Thymeleaf</li>
<img src="./captures/screenshot.png" alt="dependencies" style="width: 500px">
<li>Créer l'entité JPA Patient</li>
<img src="./captures/patient.png" alt="patient entity" style="width: 500px">
<li>Créer l'interface PatientRepository basée sur Spring Data</li>
<img src="./captures/patientRepository.png" alt="patient repository" style="width: 500px">
<li>Configurer l'application (application properties)</li>
<img src="./captures/applicationProperties.png" alt="application properties" style="width: 500px">
<li>Créer le contrôleur Spring MVC</li>
<p>Partie qui gère l'affichage des patients avec la pagination</p>
<img src="./captures/controller.png" alt="controller" style="width: 500px">
<p>Partie qui concerne le bouton delete pour effacer un patient</p>
<img src="./captures/deletePatient.png" alt="delete" style="width: 500px">
<img src="./captures/controller2.png">
<li>Créer les vues basées sur Thymeleaf</li>
<img src="./captures/vue.png" style="width: 500px">
</ol>

<h2>La validation des formulaires : </h2>
<h3>La dépendence utilisée :</h3>
<img src="./captures/dependence_validation.png" />
<p>Cette dépendance fournit des fonctionnalités de validation en intégrant la validation de Bean 
de Java (JSR-380) dans Spring Boot. On peut maintenant créer des classes de modèle pour vos formulaires 
et utiliser des annotations de validation pour définir les contraintes sur les champs de ces classes.</p>
<p>Maintenant, on peut utiliser les annotations pour valider les champs :</p>
<img src="captures/entity_validated.png">
<h2>La page template Layout : </h2>
<img src="captures/thymleeaf_layout.png">
<p>Container content : </p>
<img src="captures/layout_fragment.png">
<p>Le principe du template layout dans Thymeleaf est d'avoir un modèle de mise en page (layout)
qui définit la structure générale de nos pages web, avec des emplacements réservés pour le
contenu spécifique de chaque page. Cela permet de créer un modèle de conception cohérent pour notre 
site web tout en réutilisant certaines parties communes.</p>
<h2>Spring Security</h2>
<p>Spring Security est un framework puissant et hautement personnalisable qui fournit des 
fonctionnalités de sécurité pour les applications Java. Son rôle est de gérer l'authentification,
l'autorisation et la protection contre les attaques pour les applications basées sur Spring.</p>
<h3>Enoncé : </h3>
<p>Sécuriser l'application en intégrant un système d'authentification basé sur Spring Security avec 
les trois stratégies : InMemoryAuthentification, JdbcAuthentification et UserSetailsService.</p>
<h3>Les dépendances : </h3>
<img src="captures/security_dependencies.png"></img>
<ol>
<li><h3>InMemoryAuthentification</h3></li>
<p>La stratégie InMemoryAuthentification permet de définir les utilisateurs et leurs 
information d'authentification directement en mémoire, sans nécessiter de stockage externe comme 
une base de données.</p>
<p>Dans la classe SecurityConfig : </p>
<img src="captures/InMemoryAuthentification.png">
<li><h3>JdbcAuthentification</h3></li>
<p>L'authentification JDBC permet de gérer l'authentification en utilisant une base de donnée relationnelle
pour stocker les informations sur les utilisateurs, y compris leurs identifiants et leurs rôles.
Cela offre une solution plus robuste et extensible que l'authentification en mémoire pour des 
applications réelles.</p>
<p>application.properties : </p>
<img src="captures/jdbc_app_properties.png">
<p>Avec cette configuration, Spring Boot va chercher un script Sql et va l"executer.
Dans le script schema.sql qui se trouve dans ressources, On a mis les tables des utilisateurs
et les roles qui seront ajoutés à la base de données.</p>
<p>Dans la classe SecurityConfig :</p>
<img src="captures/jdbcUserDetailsManager.png">
<p>Dans la classe HopitalWebApplication :</p>
<img src="captures/jdbc_CLR.png"/>
<li><h3>UserDetailsService dans SecurityConfig</h3></li>
<p>Cette interface permet de récupérer les détails de l'utilisateur à partir de n'importe quelle source de données personnalisée telle qu'une base de données NoSQL, un service Web.</p>
</ol>
</br>
<p>Gestion des autorisations d'accès
Cette section cruciale de notre application se focalise sur la gestion minutieuse des droits d'accès, jouant un rôle essentiel dans la sécurité globale. Grâce à l'utilisation avisée de Spring Security, notre configuration permet une gestion précise des autorisations en définissant des règles spécifiques pour accéder à des ressources telles que les Webjars et la console H2. La classe SecurityConfig offre une flexibilité notable en permettant la définition de règles basées sur les rôles des utilisateurs, facilitée par les méthodes hasRole("USER") et hasRole("ADMIN").

Personnalisation du processus de connexion avec "httpSecurity.formLogin().loginPage("/login").defaultSuccessUrl("/").permitAll();"

httpSecurity.formLogin(): Active la gestion du processus de connexion fourni par Spring Security.
.loginPage("/login"): Spécifie la page de connexion personnalisée. Au lieu d'utiliser la page de connexion par défaut fournie par Spring Security, l'application redirigera les utilisateurs vers la page spécifiée ("/login") lorsqu'une authentification est requise.
.defaultSuccessUrl("/"): Définit l'URL par défaut vers laquelle un utilisateur est redirigé après une connexion réussie. Dans ce cas, l'utilisateur est redirigé vers la page principale ("/").
.permitAll(): Autorise l'accès à la page de connexion spécifiée par n'importe quel utilisateur, même s'il n'est pas authentifié. Cela garantit que la page de connexion est accessible à tous, même à ceux qui ne sont pas encore connectés.</p>
