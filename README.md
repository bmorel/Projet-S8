# MiDAS: Minecraft Data Analyst Server

## Collaborateurs
Ce projet a été réalisé en collaboration avec :
- Adrien MEGALY
- Baptiste MOREL
- Angelo CASTRO

## Matériels
Nous avons utilisé les matériels et logiciels suivants pour mettre en place le projet MiDAS :
- Un serveur Minecraft, configuré pour fonctionner en mode multijoueur.
- Plugin Bukkit/Spigot, pour permettre l'utilisation de plugins supplémentaires nécessaires à la collecte de données.
- Scripts Python, développés pour automatiser la récupération et le traitement des données provenant du serveur Minecraft.

## Données
### Logs du serveur
Les logs standards du serveur Minecraft Vanilla contiennent des informations essentielles telles que :
- **Connexions/Déconnexions des joueurs** : Suivre quand les joueurs se connectent et se déconnectent.
- **Commandes utilisées** : Enregistrer les commandes exécutées par les joueurs et les administrateurs, offrant un aperçu des interactions et des activités.
- **Messages de chat** : Collecter les messages échangés entre les joueurs pour analyser la communication et les interactions sociales.

Ces logs ont été analysés pour extraire des informations précieuses sur le comportement des joueurs et l'activité globale du serveur.

### Statistiques des joueurs
Minecraft Vanilla maintient des statistiques détaillées pour chaque joueur, telles que :
- **Nombre de blocs minés** : Mesurer l'activité de construction et d'extraction des ressources.
- **Nombre de sauts effectués** : Indiquer l'activité de mouvement des joueurs.
- **Nombre de monstres tués** : Suivre les interactions des joueurs avec les ennemis du jeu.

Ces données ont été extraites manuellement et via des scripts automatisés, nous permettant de dresser un profil précis de l'activité de chaque joueur.

### Sauvegardes de mondes
Les sauvegardes régulières du monde Minecraft ont été examinées pour :
- **Observer les changements dans les constructions** : Analyser comment les structures évoluent et se développent au fil du temps.
- **Utilisation du terrain** : Étudier comment les joueurs modifient et interagissent avec l'environnement naturel du jeu.
- **Modifications environnementales** : Suivre les changements dans l'écosystème du serveur.

### Succès
Les succès accomplis par les joueurs, tels que des objectifs spécifiques atteints dans le jeu, ont été surveillés pour :
- **Évaluer la progression** : Comprendre à quel rythme et dans quelle mesure les joueurs avancent dans le jeu.
- **Identifier les joueurs actifs** : Reconnaître les joueurs qui s'engagent le plus avec le contenu du jeu.

### Durée et fréquence de connexion
Nous avons extrait et analysé les logs pour suivre :
- **Durée de connexion** : Combien de temps chaque joueur passe sur le serveur lors de chaque session.
- **Fréquence de connexion** : À quelle fréquence les joueurs se connectent au serveur.

### Morts et lieux de respawn
Nous avons suivi les données sur :
- **Lieux de mort** : Identifier les zones du jeu où les joueurs meurent le plus souvent.
- **Lieux de respawn** : Voir où les joueurs réapparaissent après la mort.

Ces informations ont aidé à déterminer les zones dangereuses ou particulièrement difficiles du jeu.

## Plan d'action pour le suivi de déplacements et intégration Fiware

### Configuration du serveur Minecraft et collecte des données
Nous avons entrepris les étapes suivantes pour configurer le serveur et commencer la collecte de données :
1. **Choix de la version Minecraft** : Sélection d'une version de Minecraft compatible avec les plugins de collecte de données.
2. **Installation du serveur Minecraft** : Configuration du serveur localement, avec l'option d'utiliser un service d'hébergement pour une meilleure stabilité et performance.
3. **Choix des plugins de suivi des mouvements** :
   - **EssentialsX** : Plugin populaire pour enregistrer les positions des joueurs.
   - **Advanced Teleportation** : Suivi des mouvements des joueurs avec enregistrement des coordonnées.
   - **Prism** : Plugin de surveillance avancé pour suivre les mouvements et autres actions des joueurs.

4. **Configuration des plugins** : Paramétrage des plugins pour enregistrer les déplacements des joueurs à des intervalles réguliers (par exemple, toutes les 5 secondes).
5. **Stockage des données** : Choix de la méthode de stockage des données de mouvement (fichiers plats, base de données SQLite, etc.).

### Traitement et visualisation des données en temps réel
Pour le traitement et la visualisation des données en temps réel, nous avons suivi ces étapes :
1. **Choix d'un outil de streaming** :
   - **Apache Kafka** : Utilisé pour son efficacité et sa scalabilité pour gérer les données en temps réel.
   - **RabbitMQ** : Une alternative pour la transmission des données de mouvement.

2. **Développement d'un script de traitement** : Un script Python a été développé pour lire les données de mouvement du serveur Minecraft et les envoyer au système de streaming choisi.
3. **Intégration de Node-RED** :
   - **Installation de Node-RED** : Installation sur un serveur dédié pour une gestion centralisée.
   - **Création d'un flux Node-RED** : Conception d'un flux pour traiter les données de mouvement et les envoyer à une interface de visualisation.

4. **Choix d'une solution de visualisation** :
   - **Node-RED Dashboard** : Utilisé pour sa simplicité de configuration et son intégration facile.
   - **Grafana** : Choisi pour ses options de personnalisation et sa robustesse.
   - **Tableau** : Utilisé pour des visualisations de données avancées et interactives.

5. **Affichage en temps réel** : Configuration des interfaces pour afficher les déplacements des joueurs en temps réel sur une carte du monde Minecraft.

### Intégration de Fiware pour l'historique des déplacements
Pour intégrer Fiware et gérer l'historique des déplacements, nous avons réalisé :
1. **Installation et configuration d'Orion Context Broker** : Mise en place sur un serveur dédié, avec configuration pour recevoir les données de mouvement via des abonnements à des entités spécifiques.
2. **Adaptation du flux Node-RED** : Modification du flux pour envoyer les données de mouvement à Orion Context Broker en utilisant les protocoles NGSI-v2 ou NGSI-LD.
3. **Création d'entités Orion** : Définition d'entités pour représenter les joueurs, incluant les attributs de position (x, y, z) et d'autres informations pertinentes.
4. **Stockage de l'historique des déplacements** :
   - **QuantumLeap** : Utilisé pour stocker l'historique des données de mouvement en provenance d'Orion.
   - **Base de données** : Stockage des données dans des bases de données comme PostgreSQL ou MongoDB via des connecteurs Node-RED ou des scripts Python.

5. **Visualisation de l'historique** :
   - **Création de tableaux de bord Grafana** : Utilisation de Grafana pour visualiser l'historique des déplacements à partir de QuantumLeap ou des bases de données.
   - **Développement d'une application web** : Création d'une application web personnalisée pour interroger la base de données et afficher l'historique des déplacements.

## Outils utilisés
Pour réaliser ce projet, nous avons utilisé une variété d'outils et de technologies :
- **Serveur Minecraft** : Spigot, Paper, etc.
- **Plugins** : EssentialsX, Advanced Teleportation, Prism, etc.
- **Langages de script** : Python, Node.js
- **Streaming** : Apache Kafka, RabbitMQ
- **Fiware** : Orion Context Broker, QuantumLeap
- **Node-RED**
- **Visualisation** : Node-RED Dashboard, Grafana, Tableau

## Conseils supplémentaires
Quelques points clés que nous avons appris et que nous recommandons :
- **Sécurité** : Assurer la sécurité du serveur Minecraft et des services Fiware pour protéger les données des joueurs et les infrastructures.
- **Scalabilité** : Concevoir l'architecture du système pour gérer une augmentation du nombre de joueurs et du volume de données sans compromettre les performances.
- **Documentation** : Documenter chaque étape du projet pour faciliter la maintenance et les mises à jour futures, en s'assurant que toutes les configurations et processus sont clairement décrits.

Ce projet nous a permis de créer un serveur Minecraft avancé avec un suivi détaillé des mouvements des joueurs et une intégration efficace avec Fiware, fournissant des visualisations en temps réel et un historique détaillé des données de jeu.
