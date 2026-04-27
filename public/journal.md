# Journal de bord – Atelier Vue.js – Catalogue LEGO

##  Contexte du projet

- Objectif : réaliser une application de **catalogue de produits** avec **Vue.js** (catalogue LEGO).
- Consigne : construire progressivement une vraie app Vue.js, avec filtres, tri, panier etc.
- Mise en place du projet :
  - Création du projet avec `flutter create ateliervuejs`
  - Ajout de **`index.html`** dans le dossier `public/` avec tout le code Vue.js.
  - Ajout de toutes les **images LEGO** dans `public/img/...`.

---

##  Étape 1 – Démarrage & structure

### Actions

- Compréhension de l’arborescence générée par le projet.
- Mise en place de la structure HTML :
  - `div id="app"` comme racine Vue.
  - Topbar avec logo LEGO + titre + bouton panier.
  - Panel central avec :
    - Zone de recherche
    - Filtre par thème
    - Grille de cartes produits
    - Panier (modal)

### Réussites

- Mise en place d’une **mise en page propre et moderne** (topbar, panel, fond jaune LEGO).
- Intégration du **logo LEGO** et des images produits classées par thème.

---

##  Étape 2 – Données & réactivité Vue.js

### Actions

- Création de l’instance Vue avec :
  - `articles` : grand tableau d’objets (id, nom, thème, prix, stock, image, description…)
  - `recherche`, `themeSelectionne`, `panierOuvert`, `selectedArticle`, etc.
- Utilisation des **liaisons dynamiques** :
  - `v-for` pour afficher les produits
  - `v-model` pour la recherche et le filtre par thème
  - `v-if` / `v-else` pour le stock, le panier, la modale de détails
- Calculs avec `computed` :
  - `articlesFiltres` (recherche + thème)
  - `totalPanier`
  - `totalMontantPanier`
  - `anneeCourante`

### Réussites

- Filtre qui fonctionne : on peut chercher “chat” ou filtrer par “Disney”.
- Panier dynamique : le total et les quantités se mettent à jour en temps réel.
- Affichage conditionnel des stocks : **vert** si dispo, **rouge** si rupture.

---

##  Étape 3 – Design


- Ajout d’une **mise en forme travaillée** :
  - `.panel` en carte blanche avec ombre
  - `.card` pour chaque produit avec image, description, prix, stock
  - `.price-high` (prix > 100€) en rouge
  - `.price-low` (prix <= 100€) en vert
- Mise en forme du **panier** dans une modale :
  - Liste des articles avec boutons `+` et `−`
  - Affichage d’un message si le panier est vide
  - Bouton “Payer”

### Réussites

- Interface clair avec l’univers LEGO.
- Utilisation réussie de classes pour différencier les prix :

```css
.price-high {
  color: #c1121f; /* rouge si prix > 100€ */
}

.price-low {
  color: #2a9d8f; /* vert sinon */
}
```

## Étape 4 – Fonctions avancées

Ajout du tri par prix (aucun / croissant / décroissant) avec sortPrix + computed.
Ajout d’un mode liste / mode grille pour l’affichage des produits.
Ajout d’un thème clair / sombre :
Bouton ☀️ / 🌙 dans la topbar
Ajout / suppression de la classe dark sur <body>.
Ajout d’un panier avec badge dans le bouton topbar :
Affichage du badge rouge seulement si totalPanier > 0.

## Étape 5 – Formulaire & manipulation de produits

Création d’un formulaire d’ajout de produit avec v-model :
Nom, thème, référence, pièces, prix, stock, image, description.

Validation simple : blocage si nom/thème/prix manquants.

Ajout d’un système d’édition :
Ouverture d’une modale avec les champs pré-remplis (produitEnEdition).

Modifications appliquées directement au tableau articles.

Gestion du bouton “Annuler” (reset de produitEnEdition).



## Difficultés rencontrées

### 1. Comprendre et maîtriser Vue.js (nouveau langage / nouveau framework)
Vue.js introduit beaucoup de notions nouvelles d’un coup :

data() { return {...} }
computed, methods
directives (v-if, v-for, v-model, :class, @click)

Il a fallu du temps pour comprendre où écrire quoi et comment lier le HTML aux données JavaScript.
Solution :

Regarder la doc + expérimenter directement dans le projet.
Repartir de cas simples (un petit tableau, une boucle, un v-model) puis complexifier.

### 2. Gestion du panier et synchronisation stock / quantite

Il fallait faire attention à ne pas :
Autoriser les quantités négatives
Acheter plus d’articles que le stock disponible

Solution :
Conditions dans ajouter() et changerQuantite() :
décrémenter le stock uniquement si > 0
incrémenter / décrémenter quantite de façon cohérente
Recalcul du total du panier via un computed.

### 3. Erreurs de syntaxe (accolades, parenthèses, doublons)

Plusieurs erreurs bloquantes sont apparues :
Accolades {} mal fermées dans data()
Propriétés dupliquées (ex : produitEnEdition déclaré deux fois)
Confusion entre les objets JS et les propriétés Vue.

Solution :
Lire attentivement les messages d’erreur de la console.
Bien indenter le code pour repérer les blocs.


## Améliorations possibles

Connecter les données à une API ou une base de données.

Ajouter un système de routes (Vue Router) pour séparer :
Catalogue
Détails d’un produit
Page panier

Gérer des utilisateurs (connexion / déconnexion) avec un panier persistant.

Ajouter des promotions, des filtres supplémentaires (prix min/max, stock uniquement, etc.).

Rendre l’application full responsive (mobile first).

## Conclusion

Ce projet nous a permis de :
Prendre en main Vue.js sur un vrai cas concret (catalogue LEGO).
Manipuler les concepts essentiels : données réactives, computed, events, composants, formulaires.
Construire une interface riche et interactive, avec filtrage, tri, panier et thèmes.
Réfléchir à la structure du code pour le rendre plus clair, réutilisable et évolutif.

