#  Catalogue LEGO — Documentation du projet

> Application Vue 3 de catalogue de sets LEGO avec panier, filtres, modes d'affichage, easter eggs et bugs volontaires.

---

## Table des matières

- [Catalogue LEGO — Documentation du projet](#catalogue-lego--documentation-du-projet)
  - [Table des matières](#table-des-matières)
  - [Présentation du projet](#présentation-du-projet)
  - [Stack technique](#stack-technique)
  - [Bugs corrigés](#bugs-corrigés)
  - [Améliorations apportées](#améliorations-apportées)
    - [Fond LEGO avec texture de picots en CSS pur](#fond-lego-avec-texture-de-picots-en-css-pur)
    - [Système de favoris / wishlist](#système-de-favoris--wishlist)
    - [Slider de plage de prix (dual range)](#slider-de-plage-de-prix-dual-range)
    - [Police `Schoolbell` sur le titre](#police-schoolbell-sur-le-titre)
  - [Fonctionnalités complètes](#fonctionnalités-complètes)
    - [Catalogue \& navigation](#catalogue--navigation)
    - [Panier](#panier)
    - [Gestion des produits](#gestion-des-produits)
    - [UX \& style](#ux--style)
  - [Easter eggs \& bugs volontaires](#easter-eggs--bugs-volontaires)
  - [Structure des données](#structure-des-données)
    - [Article](#article)
    - [LocalStorage](#localstorage)
  - [Notes développeur](#notes-développeur)

---

## Présentation du projet

Le **Catalogue LEGO** est une Single Page Application (SPA) développée avec **Vue 3 (CDN, Options API)** sans outil de build. Elle permet de parcourir un catalogue de 60 sets LEGO répartis en 5 thèmes, d'ajouter des produits au panier, de filtrer/trier l'affichage, et contient plusieurs easter eggs humoristiques (écran bleu, screamer, fenêtres d'erreur Windows...).

---

## Stack technique

| Technologie | Usage |
|---|---|
| **Vue 3** (CDN `unpkg`) | Framework réactif, Options API |
| **HTML5 / CSS3** | Structure et styles, aucun framework CSS |
| **JavaScript ES6+** | Logique métier, localStorage, Web Audio API |
| **Google Fonts** | Police `Schoolbell` pour le titre |
| **LocalStorage** | Persistance des favoris entre les sessions |

---

## Bugs corrigés

| # | Localisation | Problème | Correction |
|---|---|---|---|
| 1 | Template HTML (`<body>`) | Commentaire CSS `/* */` placé directement dans le HTML — affiché comme texte brut | Remplacé par `<!-- -->` |
| 2 | Bloc `<style>`, règle `.fav` | Commentaire `//` invalide en CSS | Remplacé par `/* */` |
| 3 | Input de recherche | `@input="declencherOndulation"` référençait une méthode commentée → erreur Vue silencieuse à chaque frappe | Binding `@input` supprimé |
| 4 | Article id 49 — *Livre Monstre* | Extension d'image `.web` au lieu de `.webp` → image cassée | Corrigé en `.webp` |
| 5 | `<head>`, import Google Fonts | Balise `<link></link>` avec fermeture invalide en HTML5 | Remplacé par `<link />` |
| 6 | Méthode `startBSOD()` | Barre de progression pouvait dépasser 100% | Clampée à 100 avant affichage |

---

## Améliorations apportées

###  Fond LEGO avec texture de picots en CSS pur

Remplacement du fond jaune uni `#ffc93d` par un motif de picots LEGO en quinconce, réalisé avec quatre `radial-gradient` superposés et décalés. Les gradients utilisent des `rgba` transparents qui tintent le jaune sans le remplacer, ce qui préserve la compatibilité avec les animations BSOD et le mode sombre.

```css
body {
  background-color: #ffc93d;
  background-image:
    radial-gradient(circle at 50% 30%, rgba(255,255,255,0.18) 28%, transparent 29%),
    radial-gradient(circle at 50% 30%, rgba(0,0,0,0.10) 32%,  transparent 33%),
    radial-gradient(circle at 50% 30%, rgba(255,255,255,0.18) 28%, transparent 29%),
    radial-gradient(circle at 50% 30%, rgba(0,0,0,0.10) 32%,  transparent 33%);
  background-size:     32px 32px, 32px 32px, 32px 16px, 32px 16px;
  background-position: 0 0,       0 0,       16px 8px,  16px 8px;
}
```

---

###  Système de favoris / wishlist

Permet de marquer des produits avec un cœur `♡ / ♥` et de filtrer l'affichage pour n'afficher que les favoris. Les IDs sont persistés dans `localStorage` sous la clé `lego_favoris`.

**State ajouté :**
```js
favoris: JSON.parse(localStorage.getItem('lego_favoris') || '[]'),
afficherFavoris: false,
```

**Méthodes :**
```js
estFavori(id) {
  return this.favoris.includes(id);
},
toggleFavori(id) {
  if (this.favoris.includes(id)) {
    this.favoris = this.favoris.filter(f => f !== id);
  } else {
    this.favoris.push(id);
  }
  localStorage.setItem('lego_favoris', JSON.stringify(this.favoris));
},
```

**Filtre dans `articlesFiltres` :**
```js
if (this.afficherFavoris && !this.favoris.includes(a.id)) return false;
```

Le bouton cœur est présent dans les deux modes d'affichage (grille et liste). Le filtre favoris se cumule avec tous les autres filtres.

---

###  Slider de plage de prix (dual range)

Deux `<input type="range">` empilés en `position: absolute` permettent de définir un prix minimum et maximum. Un `<div class="range-fill">` se positionne dynamiquement entre les deux thumbs pour coloriser la zone sélectionnée.

**State ajouté :**
```js
prixMin: 0,
prixMax: 500,
prixBorne: 500,
```

**Anti-croisement des thumbs :**
```js
clampPrix() {
  if (this.prixMin > this.prixMax) this.prixMin = this.prixMax;
  if (this.prixMax < this.prixMin) this.prixMax = this.prixMin;
},
```

**Filtre dans `articlesFiltres` :**
```js
if (a.prix < this.prixMin || a.prix > this.prixMax) return false;
```

Un bouton "Réinitialiser" remet les deux curseurs à leurs valeurs extrêmes. Le style s'adapte automatiquement en mode sombre.

---

###  Police `Schoolbell` sur le titre

Import Google Fonts + application sur `.title` pour un rendu plus ludique et artisanal, en accord avec l'univers LEGO.

---

## Fonctionnalités complètes

### Catalogue & navigation
- 60 produits répartis en 5 thèmes : Animaux, Disney, Fleurs, Harry Potter, Mario
- Recherche textuelle en temps réel
- Filtre par thème, filtre favoris, filtre plage de prix — tous cumulables
- Tri par prix (croissant / décroissant)
- Mode grille et mode liste
- Modal de détails produit

### Panier
- Ajout/retrait avec gestion du stock en temps réel
- Modification des quantités depuis le panier
- Badge compteur sur l'icône
- Total dynamique et validation de commande

### Gestion des produits
- Formulaire d'ajout (toggle)
- Modal d'édition de tous les champs
- Suppression définitive

### UX & style
- Mode sombre complet
- Fond LEGO texture CSS
- Police Schoolbell sur le titre
- Responsive (breakpoint 900px)

---

## Easter eggs & bugs volontaires

| Fonctionnalité | Déclencheur | Description |
|---|---|---|
| **BSOD Windows** | `startBSOD()` | Écran bleu réaliste avec progression, fausse barre des tâches, horloge temps réel, son de crash (Web Audio API), blocage total du clavier et du clic droit |
| **Écran noir** | Fin du BSOD | Succède au BSOD après la progression à 100%, son oscillateur `square` pendant 8 secondes |
| **Fenêtres d'erreur** | `bugMode: true` | Fenêtres d'erreur Windows en cascade, codes `0x0000XXX` aléatoires, croix rouge qui fuit le curseur |
| **Screamer** | `screamerVisible` | Image plein écran (Annabelle) en `z-index: 12000` |
| **Bug image flottante** | `imageBugVisible` | Image animée (`popBug` + `floatBug`) en superposition |
| **Flash rouge** | `windows-alert` | Fond clignotant rouge sang, s'arrête si l'onglet perd le focus |
| **Mot-clé secret** | Frappe "lego" au clavier | `typedKeys` accumule les touches — logique de déclenchement à brancher |

---

## Structure des données

### Article
```js
{
  id: Number,
  nom: String,
  theme: String,       // "Animaux" | "Disney" | "Fleurs" | "Harry Potter" | "Mario"
  ref: String,
  pieces: Number,
  description: String,
  prix: Number,        // float, en euros
  stock: Number,       // décrémenté à l'ajout panier
  quantite: Number,    // quantité dans le panier (init à 0)
  image: String,       // chemin relatif .webp
}
```

### LocalStorage
| Clé | Type | Contenu |
|---|---|---|
| `lego_favoris` | JSON (tableau) | Liste des `id` produits favoris |

---

## Notes développeur

- **Pas de bundler** — fonctionne directement depuis un serveur statique ou en local, Vue 3 via CDN `unpkg`.
- **Réactivité favoris** — le tableau `favoris` est remplacé par `.filter()` à la suppression (nouveau tableau = Vue détecte le changement). Le `.push()` suffit pour l'ajout car Vue 3 intercepte les mutations de tableaux.
- **Clamping du slider** — géré dans `@input` plutôt qu'un `watch` pour éviter une boucle de réactivité.
- **`prixBorne` hardcodé à 500** — couvre le produit le plus cher (Poudlard, 469,99 €). À rendre dynamique si le catalogue évolue :
```js
// version computed dynamique
prixBorne() {
  return Math.ceil(Math.max(...this.articles.map(a => a.prix)) / 50) * 50;
}
```
- **Blocage clavier BSOD** — le listener utilise `{ capture: true }` pour intercepter les événements avant Vue, garantissant le blocage même avec des `v-on` actifs sur la page.

---

*Projet réalisé dans le cadre du projet tma - par Hanine, Molka, Fatoumata et Aissatou.*
