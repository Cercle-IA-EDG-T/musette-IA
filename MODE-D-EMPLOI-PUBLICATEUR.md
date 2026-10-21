# Mode d’emploi du publicateur — Musette IA

Ce document s’adresse à l’équipe admin du Cercle IA. Tout se fait depuis github.com, sans installer Git.

## 1. Ce que contient le dépôt

| Fichier ou dossier | Rôle | Qui le modifie |
|---|---|---|
| `index.html` | Le site lui-même (affichage, charte, navigation) | Personne, sauf le bloc `CONFIG` une fois au départ |
| `catalogue.json` | La liste des outils affichés | Le publicateur, à chaque ajout |
| `outils/<id>/` | Les fichiers de chaque outil | Le publicateur, à chaque ajout |
| `README.md` | La page d’accueil du dépôt sur GitHub | Rarement |

Règle d’or : **on ne touche jamais au reste d’`index.html`**. Tout se passe dans `catalogue.json` et `outils/`.

## 2. Première mise en ligne (une seule fois)

| # | Action | Détail |
|---|---|---|
| 1 | Créer le dépôt | Nom `musette-ia.github.io` (organisation `musette-ia`), **Public**, avec README |
| 2 | Déposer le kit | Add file › Upload files : glisser tout le contenu du dossier `musette-ia` (pas le dossier lui-même), puis Commit changes |
| 3 | Activer le site | Settings › Pages › Deploy from a branch › `main` › `/ (root)` › Save |
| 4 | Régler `CONFIG` | Ouvrir `index.html`, icône ✏️, chercher `const CONFIG` et remplir les 3 lignes ci-dessous |
| 5 | Retirer les exemples | Dans `catalogue.json`, supprimer les fiches portant `"exemple": true` dès que les vrais outils arrivent |
| 6 | Compléter le README | Remplacer `ADRESSE-DU-SITE` par l’adresse affichée dans Settings › Pages |

Les trois réglages de `CONFIG` :

| Ligne | Mettre |
|---|---|
| `prototype: true` | `prototype: false` (une fois les vrais fichiers en place) |
| `mail: "adresse-du-cercle@proton.me"` | L’adresse Proton Mail du Cercle, qui reçoit les dépôts |
| `formulaireAvis` et `champOutil` | Le lien du Google Form d’avis et l’identifiant du champ « outil » (voir §6) |

Le site ne s’affiche pas correctement en double-cliquant sur `index.html` sur un ordinateur : il a besoin d’être servi par GitHub pour lire `catalogue.json`. Testez toujours sur l’adresse en ligne.

## 3. Circuit d’un dépôt

Le contributeur remplit la fiche sur le site (bouton « Déposer ») ; le site prépare un mail dont l’objet commence par `[DÉPÔT]`. En fin de mail, le bloc « FICHE CATALOGUE » est une fiche déjà écrite pour `catalogue.json` : il suffit de la copier, puis de compléter `fichier` et `verifie`.


| Étape | Qui | Action | Libellé dans la boîte mail |
|---|---|---|---|
| Réception | Équipe admin | Accusé de réception au contributeur | 📥 Reçu |
| Vérification | Vérificateur | Check-list du §4 | 🔍 En vérification |
| Correction éventuelle | Vérificateur | Renvoi avec les points à revoir | ✏️ À corriger |
| Publication | Publicateur (≠ vérificateur) | §5 ci-dessous | ✅ Publié |
| Refus | Vérificateur | Motif expliqué | ❌ Refusé |

## 4. Check-list de vérification

| Contrôle | Critère |
|---|---|
| Sécurité | Aucun script qui envoie des données vers l’extérieur ; aucun lien suspect |
| Contenu | Rien de sensible, aucune donnée personnelle, aucun nom de stagiaire |
| Autonomie | Une webapp tient dans un seul fichier HTML et fonctionne sans réseau |
| Charte | Insigne, filet tricolore, mention NON PROTÉGÉ, « Réalisé avec assistance IA » |
| Test | Essayé sur ordinateur et sur téléphone |
| Fiche | Tous les champs du mail de dépôt remplis, capture jointe |

## 5. Publier un outil

1. **Choisir un identifiant** : minuscules, chiffres et tirets seulement, sans accent ni espace (ex. `fiche-synthese-conference`). Pas de tiret bas `_` en début de nom.
2. **Créer son dossier** : dans `outils/`, Add file › Upload files, glisser le fichier en tapant `<id>/` devant son nom dans le chemin (ou créer d’abord `outils/<id>/LISEZMOI.md`).
3. **Ajouter sa fiche** dans `catalogue.json` en copiant `modele-fiche.json`, puis Commit.
4. **Si la branche est protégée**, GitHub propose « Propose changes » : un second admin ouvre la demande (onglet Pull requests) et clique Merge.
5. **Vérifier en ligne** 1 à 2 minutes plus tard, puis envoyer le lien au contributeur.

Attention aux virgules dans `catalogue.json` : chaque fiche est séparée de la suivante par une virgule, la dernière n’en a pas. Si le catalogue affiche « vide ou introuvable », c’est presque toujours une virgule ou un guillemet manquant. Collez le fichier sur jsonlint.com pour trouver l’erreur.

## 6. Les champs d’une fiche

| Champ | Exemple | Obligatoire |
|---|---|---|
| `id` | `"compte-rendu-visite"` | Oui, identique au nom du dossier |
| `titre` | `"Compte rendu de visite"` | Oui |
| `type` | `"skill"`, `"webapp"`, `"artefact"`, `"prompt"` ou `"projet"` | Oui |
| `domaine` | `"Rédaction"` | Oui |
| `niveau` | `"Débutant"` ou `"Confirmé"` | Oui |
| `resume` | Deux lignes maximum | Oui |
| `usage` | À quoi ça sert, concrètement | Oui |
| `etapes` | Liste de 2 à 4 phrases | Oui |
| `compat` | `["Claude", "IA locale"]` | Oui |
| `auteur` | `"Cercle IA EdG-T"` ou le grade et nom si l’auteur l’accepte | Oui |
| `version`, `date`, `verifie` | `"1.0"`, `"2026-10-21"`, `"2026-10-22"` | Oui |
| `fichier` | Nom du fichier dans `outils/<id>/` | Si téléchargeable |
| `demo` | Fichier HTML à ouvrir, ou lien complet `https://…` | Si on peut l’essayer |
| `note`, `avis` | `4.5`, `12` (ou `null`, `0` sans avis) | Oui |
| `historique` | `[["1.1", "Ce qui a changé."], ["1.0", "Première version."]]` | Conseillé |

Pour le formulaire d’avis : dans Google Forms, menu ⋮ › « Obtenir le lien prérempli », remplir le champ « outil » avec un mot quelconque, copier le lien. L’identifiant `entry.123456789` qui y apparaît va dans `champOutil` ; le début du lien (jusqu’à `viewform`) va dans `formulaireAvis`.

## 7. Mettre à jour un outil

Remplacer le fichier dans `outils/<id>/` (même nom), puis dans sa fiche : nouvelle `version`, nouvelle `date`, une ligne en tête de `historique`.

## 8. Reporter les notes

Une fois par semaine ou par quinzaine : ouvrir le Google Sheet des avis, calculer la moyenne par outil, reporter `note` et `avis` dans `catalogue.json`. Lire les propositions d’amélioration et les transmettre aux auteurs.

## 9. Passation

Avant de quitter l’École : nommer deux nouveaux propriétaires du compte, leur transmettre l’accès à la boîte mail générique, et retirer ses propres droits.
