# Dynamique d'Opinion — Simulation & Contrôle Optimal

Modélisation mathématique de la formation des opinions dans une population d'agents, depuis les modèles classiques de consensus jusqu'au contrôle optimal par transport de masse, appliqué à des données réelles du World Values Survey.

---

## Modèles implémentés

### 1. Modèle de De Groot
Modèle de référence : chaque agent met à jour son opinion comme une moyenne pondérée des opinions de ses voisins selon une matrice d'influence stochastique. Convergence garantie sous conditions de connexité.

### 2. Bounded Confidence (Hegselmann-Krause)
Un agent n'est influencé que par les agents dont l'opinion est à une distance ε de la sienne. Deux variantes :
- **Symétrique** : `ε_gauche = ε_droite`
- **Asymétrique** : tolérances différentes selon le sens de l'écart

Extensions développées :
- **Self-confidence dynamique** : le poids accordé à son propre avis augmente avec le temps via `f(t) = 1 - 1/√(t+1)`
- **Epsilon variable** : chaque agent a un seuil de tolérance propre, distribué selon une gaussienne sur le spectre des opinions

### 3. Modèle continu avec fonction d'influence φ
Modèle à temps continu utilisant une fonction sigmoïde :

```
φ(x, y) = exp(-β(|x-y| - ε)) / (1 + exp(-β(|x-y| - ε)))
```

L'influence décroît progressivement avec la distance d'opinion, contrairement au seuil dur du BC.

### 4. Agents radicaux (Charismatic Leaders)
Ajout d'agents radicaux dont l'opinion est fixe (ou contrôlée). Phénomènes observés :
- Polarisation de la population autour du radical
- Indifférence si le radical est trop extrême
- Apparition de nouveaux radicaux par contagion

### 5. Contrôle optimal par distance de Wasserstein
Objectif : trouver la trajectoire optimale de quelques agents radicaux pour faire converger la distribution des opinions vers une distribution cible.

Coût minimisé :
```
W₂(distribution_finale, distribution_cible)
```

Méthodes d'optimisation utilisées :
- **Basin-Hopping** (scipy) avec sous-solveur L-BFGS-B
- **Brute force** sur grille

### 6. Contre-stratégie
Stratégie de réaction contre une campagne d'influence adverse cherchant à maximiser la somme des opinions. Implémentation d'un contre-contrôle optimal.

---

## Données réelles — World Values Survey

Extraction et prétraitement des données de l'enquête mondiale sur les valeurs (WVS, vagues 1 à 7, 1981–2010). Les réponses sont normalisées sur [0,1] pour servir de conditions initiales aux simulations.

```
WV1 (1981) → variable V66
WV3 (1990) → variable V66
WV4 (1995) → variable V82
WV5 (2000) → variable V46
WV6 (2005) → variable V55
WV7 (2010) → variable Q48
```

---

## Structure du projet

```
Dynamique-opinion/
├── Implementation/
│   ├── de_groot.py                  # Modèle De Groot
│   ├── bounded_confidence.py        # Bounded Confidence symétrique/asymétrique
│   ├── self_confidence.py           # Variante avec auto-confiance dynamique
│   ├── epsilon.py                   # Variante avec epsilon gaussien par agent
│   ├── imp.py                       # Modèle continu avec fonction phi
│   ├── radicals.py                  # Modèle avec agents radicaux
│   ├── transport_optimal.py         # Transport optimal (Earth Mover's Distance)
│   ├── optimiseur_basinhopping.py   # Contrôle optimal via Basin-Hopping
│   ├── optimiseur_brute.py          # Contrôle optimal via brute force
│   ├── radical_grid.py              # Grille de simulation avec radicaux
│   ├── counter_strategy.ipynb       # Contre-stratégie adversariale
│   ├── radical_optimise.ipynb       # Simulation radicaux optimisés
│   └── radical_non_optimise.ipynb   # Simulation radicaux non optimisés
├── data/
│   ├── data.py                      # Extraction et visualisation WVS
│   ├── opinion_model.ipynb          # Application du modèle aux données réelles
│   └── data_Codebook.pdf
├── bounded-confidence/
│   └── Bounded_confidence.docx      # Résumé de l'article de référence
├── Charismatic leaders/
│   ├── charismatic.pdf
│   └── constant_signal_theorem_.pdf
├── transport_optimal/
│   └── cours-transport-optimal.pdf
├── Rapport/
│   └── rapport.pdf
├── SUIVI.md                         # Journal hebdomadaire du projet
└── planning.xlsx
```

---

## Dépendances

```bash
pip install numpy matplotlib scipy POT pandas
```

| Package | Usage |
|---------|-------|
| `numpy` | Calcul matriciel et simulations |
| `matplotlib` | Visualisation des trajectoires d'opinions |
| `scipy` | Optimisation (basin-hopping, L-BFGS-B) et distance de Wasserstein |
| `POT` | Transport optimal (Earth Mover's Distance) |
| `pandas` | Traitement des données WVS |

---

## Résultats clés

- Le modèle BC asymétrique peut produire des **dérives unilatérales** impossibles avec le modèle symétrique.
- Trois radicaux suffisent à **rediriger significativement** une population de 50 agents via contrôle optimal.
- La distance de Wasserstein est un meilleur critère que la moyenne pour comparer deux distributions d'opinions.
- La contre-stratégie parvient à **neutraliser** une stratégie adverse même sans en connaître les paramètres exacts.

---

## Équipe

Mahmoud Bajjou · Amin · Youssef · Yasser

Projet encadré — ESILV / Polytech, février–juin 2026.
