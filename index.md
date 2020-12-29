# Projet 2020-21 : Des questionnaires pour le suivi des patients


## I. Contexte du projet

### I.1. Accompagner la transformation numérique
> The digital transformation of healthcare among others is driven by the aging/growing population challenge, the rise of chronic diseases, increasing costs and the changed expectations and behavior of people whereby digital health plays an increasingly important role.
> Overall smart healthcare market value by 2020 is estimated to be $169.32 billion by 2020. A major part of it will be for remote patient monitoring.
[Digital transformation: online guide to digital business transformation](https://www.i-scoop.eu/digital-transformation/)


### I.2. Le projet CHAMPLAIN

Projet basé sur les travaux du [projet CHAMPLAIN](https://ace-design.github.io/champlain/) entre l’Université Nice - Côte d'Azur (UCA) et l’Université du Québec à Montréal (UQAM), en visant plus particulièrement le développement d’applications logicielles en support à la population vieillissante.

Ce TD reprend la forme du TD sur [The Landing Gear System Case Study](https://mi-git.univ-tlse2.fr/ECb/LGS/blob/master/README.adoc)

### I.3. L'équipe enseignante
- Mireille Blay-Fornarino, professeur en GL;

- Jean-Michel Bruel, professeur en GL sur Toulouse qui prendra le maximum la main sur les enseignements de GL en LP DAM et IOTIA;

- Pierrick est chef de projet chez Air France. Il leur partagera son expérience et son vécu. Faîtes appel à lui si vous pensez que les étudiants ont besoin de coaching par exemple;

- Julien Crémoni est ingénieur Consultant chez Altran;

- Nicolas Ferry a initié cette version du projet... Il a fait cours aux DAM au 1e semestre et leur a donné des bases d’architectures, d’IC et de gestions de tâches sous Github.

### I.4. Pourquoi un sujet sous Github
L'ensemble du module est décliné sous [Moodle](https://lms.univ-cotedazur.fr/course/view.php?id=16573] qui référence ce site web.

Cependant, ce projet, principalement dans son énoncé, sera partagé avec d'autres équipes du projet Champlain. Il est donc nécessaire qu'il soit accessible à tous.

Cet enseignement qui inclut Génie Logiciel et Gestion de projet en INFORMATIQUE, utilise ainsi ses propres outils. 

## II. Spécifications
Votre objectif est de modéliser un système permettant de construire des questionnaires dans un contexte médical.  Certaines questions sont classiques avec par exemple l’attente d’une réponse textuelle. Pour d’autres questions, les réponses pourront correspondre à mémoriser des relevés de dispositifs électroniques : le nombre de pas enregistré toutes les 2 heures, le max de tension prise dans la journée, …  Voici la spécification qui vous est donnée.

Vous devez développer une application composée de plusieurs parties dont une partie permet aux soignants de créer des questionnaires adaptés aux patients et d’analyser leurs réponses, par jour ou par questions ; une autre partie permet au patient de définir son profil et de répondre à un questionnaire ; une partie centrale enregistre toutes les informations. 

### II.1. Description fonctionnelle

La description ci-dessous fait l'hypothèse d'un choix d'architecture. Vous pouvez décider d'en changer, pour autant que les fonctionnalités du point de vue des acteurs soient respectées.

#### II.1.1 Point de vue Patient

Un patient s’enregistre dans l’application centrale en précisant son nom et sa pathologie. Il peut pour cela être aidé par un membre de l’équipe médical si besoin. 
Il peut modifier son profil, et éventuellement enregistrer un nouveau dispositif mobile associé à son profil ; il doit alors faire référence à un type de support connu de votre application.

Il peut également préciser le personnel médical autorisé à accéder à son profil.

#### II.1.2 Point de vue Soignant

Un coach médical (soignant) peut créer un questionnaire médical pour un patient donné. 
En fonction de la pathologie du patient et des dispositifs associés à son profil, un questionnaire adapté est automatiquement généré. Le coach peut alors adapter la durée du questionnaire : à partir de quand le questionnaire doit être actif et pour quelle durée. Il élimine, ajoute ou modifie des questions. A partir du moment où il a validé un questionnaire celui-ci est automatiquement actif sur le téléphone du patient.

#### II.1.3 Point de vue Application sur le téléphone
L’application demande toutes les heures au questionnaire de faire ses relevés. Celui-ci fait, si c'est nécessaire, les relevés automatiquement en se connectant aux dispositifs, et lance éventuellement des rappels au patient pour répondre à des questions textuelles ou lui demander de faire des relevés comme par exemple prendre son taux de glycémie. 

Le questionnaire enregistre les réponses obtenues dans un « Recueil de données ». 

Si le recueil est dans l’état connecté, les réponses sont envoyées aussitôt à l’application centrale. Si le recueil est dans l’état déconnecté, les réponses collectées sont enregistrées sur le téléphone. Lorsque la quantité des réponses collectées est supérieure à un seuil donné, le recueil passe dans un état dégradé. Dans ce cas, différentes stratégies de gestion des données sont possibles. 
Dès que le recueil retourne dans l’état connecté, toutes les réponses mémorisées sont envoyées à l’application centrale.
Dans l’état dégradé, parmi les stratégies possibles, l’une consiste à effacer les réponses les plus anciennes chaque fois que de nouvelles réponses sont collectées. Une autre stratégie consiste à effacer les données moins prioritaires. Le choix des stratégies dépend du soignant lors de la création du sondage.

### II.2. Brefs exemples de scénario

1.	 Richard, patient souffrant de diabète s’enregistre dans l’application centrale avec son téléphone.
2.	 Richard enregistre son appareil de détection de la glycémie GlucofixTechLecteur002  et sa montre connectée SamPomp Galaxy Watch, SGW0012345
3.	 Richard autorise Yassine, coach médical (soignant), à accéder à son profil.
4.	 Yassine demande au système de créer un questionnaire. Le système lui demande pour quel patient, en lui présentant la liste de ses patients. Il sélectionne le patient - Richard. Le système génère un questionnaire qui comprend un ensemble de questions et de relevés et renvoie le questionnaire à Yassine pour qu’il l’adapte.
5.	Yassine précise que le questionnaire doit être actif à partir de demain pour une durée d’un an.
6.	Yassine garde les questions suivantes et en les spécialisant pour le patient, en particulier sur la fréquence :  
    1. Question : Comment s’est passée votre journée ? répondre après 19h, une fois par jour
    1. Question : Qu’avez-vous mangé aujourd’hui ? répondre matin, midi, soir
    1. Relevé : sur la montre SGW0012345; nombre de pas ; toutes les 2 heures
    1. Relevé : sur GlucofixTechLecteur002 ; glycémie ; matin, midi, soir
7.	 Yassine valide le questionnaire, qui est alors automatiquement chargé sur le téléphone de Richard.
8.	 Le lendemain matin, le téléphone notifie Richard qu’il doit prendre sa glycémie et répondre à la question b. Il relève le nombre de pas enregistré à 10h et place la donnée dans le recueil sur le téléphone.
9.	 Le recueil est dans l’état connecté ; il envoie directement la réponse à l’application centrale.

### II.3. Exigences non fonctionnelles

#### II.3.1 Protection des données
Les données du patient qu'il s'agissse des informations qui le concernent ou des données relevées sont privées.

#### II.3.2 Prise en compte du handicap, une exigence de première classe.
    * Handicap cognitif : 
        * Ne demandez pas à une personne atteinte de handicap cognitif plusieurs fois si elle a pris ses médicaments si vous n'avez pas les moyens de vérifier qu'elle ne les a pas déjà pris.
        * Tant qu'un relevé n'est pas fait, redemandez le; mais si la personne n'a pas de handicap, autorisez là à refuser le relevé.
    * Handicap visuel : 
       * Assurez-vous qu'une question n'est pas trop longue pour être visualisée en grand sur l'écran du téléphone ou au contraire dans une zone limitée du téléphone par exemple en cas de réduction du champs de vision
    * Handicap physique : 
        * Les boutons doivent être suffisamment gros et espacés pour qu'une personne ayant du mal à contrôler ses mouvements puissent cliquer au bon endroit.
        
Vous pouvez en fonction de votre propre expérience choisir d'autres exigences liées au handicap.
    
La notion de profil donnée initialement doit bien évidemment intégrer la notion de handicap.

#### II.3.2  Gérer le mode déconnecté
 * Les questionnaires doivent être accessibles en mode déconnecté.
Il peut exister plusieurs politiques de gestion de la récupération des données.
    
## III. Attentes sur le projet

Vous devrez préciser au début de votre projet avant la fin de la 2e semaine, quels sont vos objectifs.

### III.1. Fonctionnalités
Vous devez au minimum : 
  - côté coach sportif : 
     * permettre de créer un questionnaire adapté à un patient avec une question textuelle au moins.
   - côté patient : 
     * permettre de répondre aux questions du questionnaire et enregistrement automatique dans le serveur
   - partie centrale : 
     * a minima enregistrer des réponses.

Notez bien que la gestion du mot de passe ne fait pas partie du Produit Minimal Viable.

### III.2. Exigences non fonctionnelles

Vous devez prendre en compte chacun des points suivants.

#### 1. Protection des données.
Même si les mécanismes ne sont pas mis en place effectivement, explicitez ce que vous feriez, pour protéger les données.
L'utilisation d'un mot de passe n'est pas suffisante. 

#### 2. Handicap
Vous prendrez en compte au moins un aspect lié au handicap.

#### 3. Mode déconnecté
Gérer le mode déconnecté avec au moins deux politiques différentes, par exemple stockage sur le téléphone ou envoi des données.

# Autres Références

* https://www.w3.org/2019/12/pressrelease-intro-web-accessibility-course.html.fr
* https://camo.githubusercontent.com/c59ffa40ba8d00a552f74fb05742f6b950bf4a64/68747470733a2f2f692e696d6775722e636f6d2f463170373568422e706e67
* https://dev.to/madalynrose/5-things-you-need-to-know-about-manual-accessibility-testing-with-the-keyboard-and-screen-readers-3512




# --------------- PAS FINI --------------II.4 Grandes étapes du projet

1. Sprint 0 : Analyse du projet : *du 16/12/19 au 20/1/20*
    - [ TD Modélisation UML](TD/modelisation.md)
    - [ TD Exigences]](TD/exigences.md)
2. Sprint 1 : Livraison d'une version V0 d'un produit minimal viable  du *---*


### II.5 Livraisons
Les rendus du projet sont décrits dans le [MOODLE](https://lms.univ-cotedazur.fr/mod/assign/index.php?id=19082)
Chaque équipe devra
2.  [ ]  Remplir le document partagé suivant en précisant les membres de l'équipe, la variante du sujet choisi et le nom de l'équipe.
1.  [ ]  Proposer un premier document d'analyse de l'application en utilisant les diagrammes UML (voir [ TD Modélisation UML](TD/modelisation.md))




## III. Règles GIT

### III.1 Créer des templates
   * Un template pour les Histoires Utilisateurs
   * Un template pour les tâches Liées à la prise en compte du handicap
  

# Autres Références

* https://www.w3.org/2019/12/pressrelease-intro-web-accessibility-course.html.fr
* https://camo.githubusercontent.com/c59ffa40ba8d00a552f74fb05742f6b950bf4a64/68747470733a2f2f692e696d6775722e636f6d2f463170373568422e706e67
* https://dev.to/madalynrose/5-things-you-need-to-know-about-manual-accessibility-testing-with-the-keyboard-and-screen-readers-3512


Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/IUT-DEPT-INFO-UCA/LP-DAM-IOTIA-Project/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
