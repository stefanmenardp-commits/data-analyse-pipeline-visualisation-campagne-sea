# Pipeline d'analyse des campagnes SEA

Étude de cas d'un pipeline de données marketing conçu pour centraliser, transformer et visualiser les données de performance des campagnes SEA au sein de plusieurs agences.

## Avis de confidentialité

Ce projet a été mené dans un cadre professionnel.

Le code source, les données de production, les informations relatives aux clients, les indicateurs de performance réels et les captures d'écran originales ne sont pas accessibles au public pour des raisons de confidentialité.

Ce référentiel présente la portée du projet, mes responsabilités, l’architecture technique ainsi que les principaux concepts d’ingénierie des données et d’analyse impliqués.

Certains diagrammes et illustrations ont pu être recréés à partir d’informations anonymisées ou fictives.

## Table des matières

- [Présentation du projet](#aperçu_projet)
- [Contexte métier](#contexte-metier)
- [Objectifs](#objectifs)
- [Mes responsabilités](#mes-responsabilités)
- [Sources de données](#sources-de-données)
- [Architecture technique](#architecture-technique)
- [Qualité des données et alertes](#qualite-des-données-et-alertes)
- [Visualisation](#visualisation)
- [Stack technique](#stack-technique)
- [Compétences développées](#compétences-développées)

## Présentation du projet

L’objectif de ce projet était de centraliser et d’analyser les données relatives aux dépenses et aux performances des campagnes SEA provenant d’environ 300 agences.

Ces données ont ensuite été enrichies à l’aide de sources externes et internes afin d’offrir une vision plus globale des performances des campagnes et de l’activité commerciale.

La solution comprenait :

- l’extraction de données à partir de multiples sources
- la centralisation dans BigQuery
- des transformations SQL
- des couches de données Bronze, Argent et Or
- une orchestration avec Dataform
- un contrôle de la qualité des données avec des alertes automatisées
- une visualisation via Looker Studio
- une documentation technique et fonctionnelle

---

## Contexte métier

L’organisation avait besoin d’un moyen fiable et centralisé pour suivre les performances de ses campagnes SEA.

Avant la mise en œuvre de la solution, les données provenaient de différentes sources et nécessitaient un traitement manuel récurrent. Cela rendait l’analyse plus chronophage et augmentait le risque d’incohérences.

Les tâches effectuées par les utilisateurs étaient :

- suivre les dépenses des campagnes
- comparer les performances des campagnes
- filtrer les données par agence, période, campagne ou autres dimensions
- identifier les valeurs anormales
- comparer les performances SEA avec des données externes (Pages Jaunes, données déclaratives liées aux réponses des utilisateurs sur les formulaires du site du client, etc.)
- accéder à des indicateurs fiables via des tableaux de bord

---

## Objectifs

Les principaux objectifs de la solution étaient les suivants :

1. Centraliser les données des campagnes dans un entrepôt de données unique
2. Réduire la préparation manuelle des données
3. Standardiser les indicateurs métier et les calculs
4. Enrichir les données des campagnes à l’aide de sources externes
5. Améliorer les performances et la convivialité du tableau de bord
6. Détecter automatiquement les problèmes de qualité des données
7. Faciliter la maintenance et les développements futurs
8. Documenter la solution pour assurer la continuité opérationnelle

---

## Mes responsabilités

Etant seul sur le projet, ma responsabilité intervenait de l'analyse du besoin jusqu'à la documentation du projet, en détail voici ce que cela donne :

- la collecte et la clarification des exigences analytiques
- l’identification des indicateurs clés et des dimensions requises
- la conception de maquettes de tableaux de bord
- la sélection et configuration des stratégies d'extraction et ingestion des données
- le développement de scripts d’extraction Python sur mesure lorsque cela était nécessaire
- la structuration des données en couches Bronze, Argent et Or
- la centralisation des transformations SQL dans Dataform
- la conception de contrôles de qualité des données et la mise en place d’alertes automatisées
- l’optimisation des tableaux de bord Looker Studio
- la création de la documentation technique et fonctionnelle (pour l'usage et la passation du projet)

---

## Sources de données

Le pipeline traitait plusieurs catégories de données.

### Données des campagnes SEA

Exemples d’informations traitées :

- dépenses publicitaires
- impressions
- clics
- conversions
- indicateurs liés aux performances (CPA, CPC, CPM, etc.)
- dimensions des campagnes et des comptes
- dates
- informations sur les agences

### Données externes

Les données de campagne ont été enrichies par des données externes ou complémentaires,
notamment :

- les données des Pages Jaunes 
- les données déclaratives collectées via le site web du client

Les champs et valeurs exacts ne sont pas publiés dans ce référentiel.

---

## Architecture technique

L'architecture générale suivait le schéma suivant :

```text
Sources de données
│
├── Plateformes SEA
│   ├── Google Ads
│   ├── Meta Ads
│   ├── Bing Ads
│   ├── Taboola
│   └── etc.
│
└── Sources externes
    ├── Pages Jaunes
    └── Données déclaratives utilisateurs
        │
        ▼
Couche d’extraction
│
├── Supermetrics → Google Sheets
└── Scripts Python
    ├── Google Cloud Functions
    └── Google Cloud Run Jobs
        │
        ▼
Stockage des données — BigQuery
        │
        ▼
Transformation des données
│
├── Couche Bronze
│   └── Données brutes et légèrement transformées
│
├── Couche Silver
│   ├── Données nettoyées, normalisées et enrichies
│   └── Données utilisées pour le contrôle qualité
│
└── Couche Gold
    └── Tables analytiques prêtes à l’emploi
        │
        ▼
Orchestration des transformations SQL
│
└── Google Dataform
        │
        ▼
Contrôle et alertes automatiques
│
└── Google Apps Script
        │
        ▼
Visualisation des données
│
└── Looker Studio
```

---

## Qualité des données et alertes

Des contrôles de qualité des données ont été mis en place afin d’identifier les anomalies avant qu’elles n’affectent les tableaux de bord ou les décisions métier.

Voici quelques exemples de contrôles surveillés :

- données manquantes
- nombre de lignes inattendu
- enregistrements en double
- valeurs anormales
- valeurs dépassant les seuils définis
- retards dans la mise à disposition des données

Lorsqu’un problème était détecté, une alerte automatisée pouvait être envoyée aux personnes concernées.

Les mécanismes d’alerte s’appuyaient sur des contrôles SQL et Google Apps Script.

---

## Visualisation

Les données finales ont été mises à disposition via des tableaux de bord Looker Studio.

Les tableaux de bord ont été conçus pour prendre en charge :

- la surveillance globale des performances
- l’analyse au niveau de l’agence
- l’analyse au niveau des campagnes
- la comparaison entre périodes
- le suivi des dépenses
- le suivi des indicateurs clés de performance (KPI)

Une attention particulière a été portée aux éléments suivants :

- la lisibilité des tableaux de bord
- les filtres pertinents
- les définitions des indicateurs
- les performances des requêtes
- la cohérence entre les visualisations
- la facilité d’utilisation pour les analyses quotidiennes

Voici un aperçu du tableau de bord : 

<img width="1424" height="1024" alt="dashboard" src="https://github.com/user-attachments/assets/74581cae-a213-462c-8b00-8e08b5051904" />

---

## Stack technique

| **Domaines** | **Technologies** |
|---|---|
| **Extraction** | `Supermetrics`, `Google Sheets`, `Python`, `Google Cloud Function`, `Google Cloud Run Jobs`  |
| **Stockage** | `Data Warehouse BigQuery` |
| **Transformation** | `SQL` |
| **Orchestration SQL** | `Dataform` |
| **Visualisation** | `Looker Studio` |
| **Alerte/Contrôle de données** | `SQL`, `Google Apps Script (JS)` |
| **Documentation** | `Technique et fonctionnelle` |

---

## Compétences développées

Ce projet m'a permis de développer et de mettre en œuvre mes compétences dans les domaines suivants :

- autonomnie dans la gestion d'un projet et la communication avec un client
- analyse métier et recueil des besoins
- conception de pipelines de données (Apprentissage de la Modern Data Stack)
- architecture de données
- traitement des données
- identification des métriques essentielles pour le contrôle de la qualité des données
- la conception de tableaux de bord
- la documentation technique
- le suivi d'un projet sur plusieurs années (maintenance et évolution)

Pour ce qui est des outils, j'ai développé des compétences dans ceux qui sont présents dans la partie stack technique.

