# Projet 2020-21 : Des questionnaires pour le suivi des patients.


## 1. Contexte du projet

### 1.1. Accompagner la transformation numérique
```markdown
The digital transformation of healthcare among others is driven by the aging/growing population challenge, the rise of chronic diseases, increasing costs and the changed expectations and behavior of people whereby digital health plays an increasingly important role.
Overall smart healthcare market value by 2020 is estimated to be $169.32 billion by 2020. A major part of it will be for remote patient monitoring.
[Digital transformation: online guide to digital business transformation](https://www.i-scoop.eu/digital-transformation/)
```

### 1.2. Le projet CHAMPLAIN

Projet basé sur les travaux du projet CHAMPLAIN entre l’Université Nice - Sophia Antipolis (UNS) et l’Université du Québec à Montréal (UQAM), en visant plus particulièrement le développement d’applications logicielles en support à la population vieillissante.

[Extraits de la Description du Projet Champlain](ChamplainIntroduction.txt)

Ce TD reprend la forme du TD sur [The Landing Gear System Case Study](https://mi-git.univ-tlse2.fr/ECb/LGS/blob/master/README.adoc)

### L'équipe enseignante
- Mireille Blay-Fornarino, professeur en GL, 
- Jean-Michel Bruel, professeur en GL sur Toulouse qui prendra le maximum la main sur les enseignements de GL en LP DAM et IOTIA/

- Pierrick est chef de projet chez Air France. Il leur partagera son expérience et son vécu. Faîtes appel à lui si vous pensez que les étudiants ont besoin de coaching par exemple.

- Nicolas Ferry a initié cette version du projet... Il a fait cours aux DAM au 1e semestre et leur a donné des bases d’architectures, d’IC et de gestions de tâches sous Github.

### Pourquoi un sujet sous Github
L'ensemble du module est décliné sous Moodle qui référence ce site web.
Ce travail sera partagé avec d'autres équipes de notre université.
Utiliser nos propres outils pour nos enseignements.

## Vision globale du projet
Votre objectif est de modéliser un système permettant de construire des questionnaires dans un contexte médical.  Certaines questions sont classiques avec par exemple l’attente d’une réponse textuelle. Pour d’autres questions, les réponses pourront correspondre à mémoriser des relevés de composants électroniques : le nombre de pas enregistré toutes les 2 heures, le max de tension prise dans la journée, …  Voici la spécification qui vous est donnée.

Vous devez développer une application composée de plusieurs parties dont une partie permet aux soignants de créer des questionnaires adaptés aux patients et d’analyser leur réponse ; une autre partie permet au patient de définir son profil et de répondre à un questionnaire ; une partie centrale enregistre toutes les informations. Nous disposons d’une base de connaissance externe dans laquelle un grand nombre de types de supports mobiles ont été enregistrés (DeviceKB). Elle comprend des modèles de montres connectés, des tensiomètres, des appareils de détection de la glycémie connecté.

## Description détaillée
Un patient s’enregistre dans l’application centrale en précisant son nom et sa pathologie. Il peut pour cela être aidé par un membre de l’équipe médical si besoin. Il peut modifier son profil, et éventuellement enregistrer un nouveau dispositif mobile associé à son profil ; il doit alors faire référence à un type de support préenregistré dans DeviceKB. Il peut également préciser le personnel médical autorisé à accéder à son profil.

Un coach médical peut créer un questionnaire médical pour un patient donné. En fonction de la pathologie du patient et des dispositifs associés à son profil, un questionnaire adapté est automatiquement généré. Le coach peut alors adapter la durée du questionnaire : à partir de quand le questionnaire doit être actif et pour quelle durée. Il élimine, ajoute ou modifie des questions. A partir du moment où il a validé un questionnaire celui-ci est automatiquement déployé sur le téléphone du patient.

Dès que le questionnaire est actif, l’application du patient, en fonction du questionnaire, se charge de faire les relevés automatiquement, de lancer des rappels au patient pour répondre à des questions textuelles ou lui demander de faire des relevés comme par exemple prendre son taux de glycémie. A la fin de la durée du questionnaire, celui-ci devient inactif. Le coach peut réactiver le questionnaire.

A FINIR

## Attentes sur le projet

### Fonctionnalités
Vous devez au minimum : 
  - côté coach sportif : 
     * permettre de créer un questionnaire adapté à un patient avec une question textuelle au moins et deux profils différents possibles
   - côté patient : 
     * permettre de répondre aux questions du questionnaire et renregistrement automatique dans le server
   - partie centrale : 
     * a minima enregistrement des réponses.
     
 ### Exigences non fonctionnelles
patient : 
  - proposer une application à destination du patient sur laquelle le patient peut répondre à des questions.


## Propriétés attendues du logiciel

## E-1 : Adaptabilité dynamique 

Quelle que soit la variante du logiciel on attend que vous proposiez une adaptation dynamique du logiciel en fonction du handicap 
       ex. choix de la fonte, 
       ex. remplacement d'une image par le texte,
       ex. modification de la complexité des questions en retirant des réponses fausses, ...

## E-2 : Handicap comme une exigence de premier ordre

Quelle que soit la variante du logiciel on attend que vous preniez en compte le handicap à tous les niveaux par exemple
* métier
    * *globalement*,  
        * par exemple "ne pas proposer d'images à un déficient visuel"  peut impacter  
               * la construction des quizz par des aidants, 
               * le choix des quizz, ...
    *  *question*: 
        *  par exemple si handicap cognitif introduire les notions de complexité d'une question, handicap visuel, de visibilité, ...
    *  *Quiz* 
        * par exemple le handicap va impacter la manière de poser les questions d'un quizz (grille ou non), répéter les questions;
* interface par une adaptation des interactions Homme-Machine en fonction du handicap
* architecture : 
    * en cas de handicap lié à la mémoire les temps de réponses ont beaucoup d'importance, il convient donc de prévoir des palliatifs à un réseau faible par des téléchargements par exemple sur le téléphone.
    * le stockage des clicks quoique indispensable pour favoriser une amélioration des interfaces pose des question de vie privé, de charge, ... 
    
    

# II.4 Grandes étapes du projet

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
