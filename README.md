# 🚀 Le Jeu de l'Oie de l'Espace

TP8 – Méthodologie de travail pour l'informatique – *IA générative / Vibe coding*
Yassine Belmamoune – L1 Informatique, Avignon Université

Jeu de l'oie personnalisable, généré avec une IA générative (Claude) à partir d'un cahier des charges, puis testé et modifié.
Inspiré du dépôt exemple [tspriet/VibeOie](https://github.com/tspriet/VibeOie).

## ▶️ Lancer le jeu

Aucune installation n'est nécessaire : ouvrir `index.html` dans un navigateur (Safari, Firefox, Chrome).

```bash
git clone <adresse-de-ce-depot>
cd <nom-du-depot>
open index.html      # sur Mac
```

---

## 1. Cahier des charges fonctionnel

**Configuration**
- Saisir le nombre d'équipes (entre 2 et 10). Un nombre invalide (vide, 1, 11, 2.5…) affiche un message d'erreur.
- Donner un nom à chaque équipe (facultatif : « Équipe 1 », « Équipe 2 »… par défaut). Deux équipes ne peuvent pas avoir le même nom.
- Bouton « Lancer la partie ».

**Partie**
- Le plateau compte 63 cases plus une case départ (0). Il affiche les pions de toutes les équipes, et le pion de l'équipe dont c'est le tour est mis en évidence.
- Le joueur lance 2 dés (bouton ou touche Espace). Le pion avance case par case (animation).
- Si le pion dépasse la case 63, il recule du nombre de cases en trop.
- La première équipe qui tombe exactement sur la case 63 gagne. Un écran de victoire propose de rejouer.
- Un journal raconte tout ce qui se passe.

**Règles classiques du jeu de l'oie (version « espace »)**
| Case | Nom | Effet |
|---|---|---|
| 5, 9, 14, 18, 23, 27, 32, 36, 41, 45, 50, 54, 59 | 🚀 Fusée (oie) | avance encore du même nombre de cases |
| 6 | 🌉 Pont spatial | va directement à la case 12 |
| 19 | 🏨 Hôtel | passe 2 tours |
| 31 | 🕳️ Trou noir (puits) | bloqué jusqu'à ce qu'une autre équipe arrive sur la case |
| 42 | 🌀 Labyrinthe | retourne à la case 30 |
| 52 | 🔒 Prison | bloqué jusqu'à ce qu'une autre équipe arrive sur la case |
| 58 | 💀 Explosion (tête de mort) | retour à la case 0 |
| 63 | 🪐 Arrivée | victoire |
| 1er lancer 6+3 / 4+5 | | direct à la case 26 / 53 |

**Variante : les cartes action (comme au Mille Bornes)**
- Chaque équipe commence avec 2 cartes au hasard et en garde 3 au maximum.
- Les cases 15, 35 et 56 (🃏) font piocher une carte.
- Une carte se joue pendant son tour, **quand on veut**, avant de lancer les dés.

| Carte | Effet |
|---|---|
| ⚡ Turbo | +3 cases au prochain lancer |
| 🔁 Rejouer | rejouer une fois après ce tour |
| 🛡️ Bouclier | protège du prochain piège (et des cartes Gel / Téléporteur adverses) |
| 🔓 Libération | sortir de l'hôtel, du trou noir ou de la prison |
| 🧊 Gel | une équipe adverse passe son prochain tour |
| 🔄 Téléporteur | échanger sa place avec une autre équipe |

**Nouvelle action ajoutée (étape « modification du programme »)**
- 🌪️ **Tempête solaire** (cases 25 et 47) : *l'équipe recule d'autant de cases qu'il y a d'équipes dans la partie.*

## 2. Conditions techniques

- Exécution **en local**, dans un navigateur web récent, sur n'importe quel OS (macOS, Windows, Linux).
- Langages : **HTML + CSS + JavaScript**, sans bibliothèque externe, sans serveur, sans connexion internet.
- Un seul fichier : `index.html`.

## 3. Aspect graphique

- Ambiance **spatiale** : fond bleu nuit dégradé, accents jaunes.
- Plateau en serpentin (7 lignes × 9 colonnes), du départ en bas à gauche jusqu'à l'arrivée en haut.
- Couleurs de cases selon leur type : fusées en bleu, pièges en rouge, bonus en vert, tempête en violet, arrivée en or.
- Les icônes sont des emojis (pas de fichier image à fournir) et chaque équipe a son pion de couleur, numéroté.
- Mise en page adaptée aux petits écrans (le panneau passe sous le plateau).

---

## 4. Vérifications fonctionnelles (tests)

| Test | Résultat |
|---|---|
| Saisir 1, 11, vide ou 2.5 équipes | message d'erreur, la partie ne démarre pas ✅ |
| Deux équipes avec le même nom | message d'erreur ✅ |
| Partie à 2, 5 et 10 équipes | fonctionne ✅ |
| Rebond après 63 | le pion recule du surplus ✅ |
| Chaînage de cases (fusée → fusée, tempête → piège) | effets appliqués à la suite ✅ |
| Trou noir / prison : libération par une autre équipe | ✅ |
| Toutes les équipes coincées en même temps (blocage infini) | corrigé : une « onde de choc » libère tout le monde ✅ |
| Double-clic sur « Lancer les dés » pendant l'animation | bouton désactivé, pas de double lancer ✅ |
| Lancer les dés pendant le choix d'une cible de carte | impossible, il faut choisir ou annuler ✅ |
| Nom d'équipe contenant du HTML (`<b>test</b>`) | affiché comme du texte, pas interprété ✅ |
| Plusieurs parties de suite (« Rejouer ») | les états sont bien remis à zéro ✅ |
| Simulation automatique de 300 parties de 2 à 10 équipes | 300 parties terminées, aucune position invalide ✅ |

## 5. Modifications demandées à l'IA après la première version

1. Bug : le jeu plantait au lancement, parce que le plateau était dessiné après les pions. → Ordre corrigé.
2. Bug : pendant un « passe ton tour » automatique, on pouvait cliquer sur les dés. → Bouton bloqué pendant ce temps.
3. Cas non prévu : si toutes les équipes sont coincées, la partie ne se termine jamais. → Ajout de l'onde de choc.
4. Ajout de la nouvelle action **Tempête solaire**, en gardant le fonctionnement des autres cases (le prompt précisait de ne pas casser les cases existantes).

## 6. Que penser de tout cela ?

L'IA produit très vite un jeu qui marche, mais le code généré contenait des bugs. Certains apparaissaient tout de suite (le plantage au démarrage), d'autres ne se voyaient qu'en testant des situations rares (toutes les équipes bloquées). Sans tests, ils seraient passés inaperçus.
Pour garder le contrôle, il faut un cahier des charges précis, comprendre la structure du programme (ici : configuration → tour de jeu → déplacement → effet de la case → fin de tour), puis demander des modifications ciblées, une fonction à la fois, en disant ce qui ne doit pas changer.

**Découpage en fonctions du programme**
- `validerConfig()`, `demarrerPartie()` : configuration de la partie
- `dessinerPlateau()`, `dessinerPions()`, `rafraichir()` : affichage
- `lancerDes()` → `avancer()` → `appliquerCase()` → `finDeTour()` → `tourSuivant()` : un tour de jeu
- `jouerCarte()`, `appliquerCarteCiblee()` : cartes action
