#  Catalogue LEGO – Documentation du projet

## 📌 Présentation générale

Le projet **Catalogue LEGO** est une application web permettant de consulter, gérer et acheter des sets LEGO.

L’application propose un catalogue interactif regroupant de nombreux ensembles avec leurs informations détaillées. Elle permet également aux utilisateurs d’interagir dynamiquement avec les produits via différentes fonctionnalités (recherche, tri, panier, modification…).

---

##  Objectifs du projet

* Développer une interface web moderne et intuitive
* Mettre en place un catalogue dynamique de produits
* Implémenter des fonctionnalités interactives (tri, recherche, filtres)
* Gérer un système de panier utilisateur
* Permettre la gestion complète des produits (CRUD)

---

##  Environnement technique

Le projet repose sur les technologies suivantes :

* Vue.js
* JavaScript (ES6+)
* HTML5
* CSS3
* Node.js / npm


## 📁 Structure du projet

```
Catalogue-LEGO/
│
├── public/
│   ├── img/
│   ├── favicon.ico
│   ├── index.html
│   └── Journal.md
│
├── src/
│   ├── assets/
│   │   └── logo.png
│   │
│   ├── components/
│   │   └── HelloWorld.vue
│   │
│   ├── router/
│   │   └── index.js
│   │
│   ├── store/
│   │   └── index.js
│   │
│   ├── views/
│   │   ├── AboutView.vue
│   │   └── HomeView.vue
│   │
│   ├── App.vue
│   └── main.js
│
├── package.json
├── package-lock.json
├── babel.config.js
├── vue.config.js
└── README.md
```

---

##  Organisation de l’interface

Le fichier `index.html` constitue le point central de l’interface utilisateur.

### 📄 Structure détaillée du fichier

* **Lignes 9 à 786 :**
  Définition des styles CSS (mise en page, animations, thèmes…)

* **Lignes 791 à 803 :**
  Barre de navigation (Navbar) :

  * Logo
  * Mode jour / nuit
  * Accès au panier

* **Lignes 805 à 974 :**
  Zone de gestion des produits :

  * Tri par prix (croissant / décroissant)
  * Filtrage par thème
  * Barre de recherche dynamique
  * Ajout d’un produit
  * Mode grille / liste

* **Lignes 1088 à 1387 :**
  Cartes des produits :

  * Affichage des sets LEGO
  * Informations détaillées
  * Actions (modifier, supprimer, ajouter au panier)

---

## 🚀 Fonctionnalités principales

###  Catalogue produits

Chaque produit contient :

* Nom
* Prix
* Référence
* Nombre de pièces
* Thème
* Stock
* Description
* Image

---

### 🎨 Thèmes disponibles

* Harry Potter
* Disney
* Fleurs
* Mario
* Animaux

---

### 🔍 Recherche et filtres

* Recherche dynamique en temps réel
* Filtrage par thème
* Tri :

  * Prix croissant
  * Prix décroissant

---

###  Affichage

* Mode grille
* Mode liste

---

### 🛒 Panier

* Ajout d’articles
* Consultation du panier

---

###  Gestion des produits

* Ajout d’un nouveau set (avec image)
* Modification des caractéristiques
* Suppression d’un produit
* Affichage des détails

---

### 🌙 Interface utilisateur

* Mode jour / nuit

---

## ⚠️ Anomalies et Comportements Inattendus
Plusieurs composants du catalogue présentent des instabilités techniques. Une révision globale des scripts de gestion est nécessaire.

### 🛠 Dysfonctionnements de l'Interface (UI)
Contrôles de luminosité : L'interaction avec l'icône de mode jour provoque une interruption critique du service.

Fiches produits : Défaut d'affichage (champs manquants).

Mode Liste : Instabilité visuelle majeure lors de la permutation du mode d'affichage.

Assets graphiques : Problème d'indexation sur certains visuels. 

### Système de Recherche et Tri
Filtres thématiques : Les filtres "Animaux" et "Fleurs" ne retournent aucune donnée 

Indexation des prix : L'algorithme de tri décroissant rencontre une erreur d'exécution bloquante.

###  Expérience Utilisateur et Panier
Gestion du panier : Des anomalies sonores et visuelles non documentées surviennent lors de l'ajout d'articles.

Composant "Détails" : Le déclencheur d'affichage détaillé ne parvient pas à charger le contenu.

###  Gestion du cycle de vie des produits
Persistance visuelle : La suppression d'un produit ne semble pas libérer l'espace mémoire à l'écran.

---

## 📈 Améliorations attendues

* Stabilisation de l’interface
* Correction des erreurs bloquantes
* Amélioration de la recherche
* Fiabilisation des interactions utilisateur
* Optimisation globale des performances*
* Rendre le site dynamique 

---

## 👥 Équipe projet

* Adi Katia
* Luce-Dubas Léna
* FEHA Hermann Junior
* Touazi Yacine

---
