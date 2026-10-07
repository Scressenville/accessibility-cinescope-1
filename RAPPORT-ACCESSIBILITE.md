# Rapport d'accessibilité — CinéScope

## Membres du groupe
- Sylvain CRESSENVILLE
- Sylvain GROSS

Objectif : simplifier la navigation au clavier, en privilégiant le HTML natif (pas de `tabindex` positif, ARIA seulement si nécessaire) et en conservant l'apparence.

## 5 constats

| # | Constat                                                            | Statut |
|---|--------------------------------------------------------------------|--------|
| 1 | Cartes de films non utilisables au clavier                         | Corrigé (détaillé) |
| 2 | Focus clavier invisible                                            | Corrigé (détaillé) |
| 3 | Favori et recherche sans nom accessible | Corrigé (détaillé)       |
| 4 | Disponibilité indiquée uniquement par la couleur                   | Corrigé |
| 5 | Pas de structure : `div` partout, titres h1 → h4, images sans `alt` | Corrigé |

## Constat 1 — Cartes non utilisables au clavier

- **Avant :** la carte est une `<div onClick>`. Elle ne reçoit pas le focus, et Entrée ne fait rien.
- **Après :** le titre est un `<button>` natif. Son `::after` couvre toute la carte, qui reste donc cliquable à la souris et ne compte que pour un seul arrêt de tabulation.
- **Impact :** avant, impossible de sélectionner un film sans souris. Après : Tab pour aller au film, Entrée pour le sélectionner, et la sélection est annoncée (`role="status"`).

## Constat 2 — Focus invisible

- **Avant :** `button:focus, input:focus, a:focus { outline: none; }`
- **Après :** `:focus-visible { outline: 3px solid #3b5bdb; }` (jaune sur la barre sombre). Sur une carte, le contour entoure toute la carte.
- **Impact :** avant, l'utilisateur au clavier ne savait pas où il était. Après, le focus est toujours visible, et rien ne change pour la souris.

## Constat 3 — Éléments sans nom

- **Avant :** le favori est lu « étoile blanche, bouton », trois fois, sans film associé. La recherche n'a qu'un `placeholder`.
- **Après :** le favori contient un texte masqué « Favori : *titre* » et l'attribut `aria-pressed`. La recherche a un vrai `<label>` (masqué visuellement).
- **Impact :** le lecteur d'écran lit « Favori : Orbite 9, bouton bascule, activé » : le contrôle est compréhensible et son état est connu.

## Autres corrections

- Ajout du texte « Disponible » / « Complet » à côté de la pastille de couleur.
- `header`, `nav`, `main`, liste `ul/li`, titres `h2` sous le `h1`, `alt=""` sur les affiches (décoratives).
- Logo `div` cliquable remplacé par un `<button>`.
- Contraste de la bordure du champ de recherche relevé à 3,5:1.
