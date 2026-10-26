# Détection d'intrusions réseau : optimisation d'hyperparamètres

## 1. Contexte
Les réseaux informatiques sont exposés à des attaques (déni de service, scans de ports, accès non autorisés). Un **système de détection d'intrusions (IDS)** surveille le trafic et signale les connexions suspectes. Ce projet construit un modèle de machine learning qui joue ce rôle.

- **Domaine :** Sécurité
- **Problème :** détection d'intrusions réseau
- **Dataset :** NSL-KDD (`KDDTrain+.txt`, `KDDTest+.txt`)

## 2. Objectif
Développer un modèle de data mining performant et trouver sa **meilleure configuration d'hyperparamètres** en comparant plusieurs méthodes d'optimisation.

**Tâche :** classification binaire, une connexion est **normale** ou une **attaque**.
(Extension possible : classification multi-classe DoS / Probe / R2L / U2R.)

## 3. Besoins

### Besoins fonctionnels
- Charger et préparer les données NSL-KDD
- Entraîner plusieurs algorithmes avec leurs paramètres par défaut
- Optimiser les hyperparamètres avec 3 méthodes
- Comparer toutes les expériences dans un tableau
- Sélectionner le meilleur modèle et l'évaluer sur le jeu de test

### Besoins non fonctionnels
- Résultats reproductibles (graine aléatoire fixée, `random_state=42`)
- Code organisé et versionné sur Git
- Aucune fuite de données (le jeu de test n'est utilisé qu'à la fin)
- Rapport clair et justifié

## 4. Outils
Python, scikit-learn, XGBoost, Optuna, pandas, matplotlib, seaborn, Jupyter
(optionnel : Weka pour une comparaison)

## 5. Plan de travail

| Étape | Tâche | Livrable |
|---|---|---|
| 1 | Environnement, repo Git, chargement des données | Notebook `01_exploration` |
| 2 | Exploration et préparation (cible binaire, encodage, normalisation, split) | Notebook `02_preparation` |
| 3 | Baseline : algorithmes avec paramètres par défaut | Tableau des scores |
| 4 | Optimisation : Grid Search, Random Search, Optuna | Meilleurs hyperparamètres par méthode |
| 5 | Comparaison de toutes les expériences | Tableau + graphiques dans `results/` |
| 6 | Choix du meilleur modèle et de sa configuration | Modèle retenu |
| 7 | Évaluation finale sur le test set | Métriques finales |
| 8 | Rédaction du rapport | Fichier dans `reports/` |

## 6. Algorithmes testés
- Régression logistique
- Arbre de décision
- Random Forest
- XGBoost
- (optionnel) KNN, SVM

## 7. Méthodes d'optimisation
| Méthode | Principe |
|---|---|
| Grid Search | teste toutes les combinaisons d'une grille |
| Random Search | teste des combinaisons tirées au hasard |
| Optuna (bayésien) | choisit les prochains essais selon les résultats précédents |

Validation croisée (5 plis) pour toutes les méthodes.

## 8. Métriques d'évaluation
- Accuracy, Precision, Recall, F1-score, ROC-AUC
- Matrice de confusion
- Temps d'entraînement et d'optimisation

**Métrique principale : F1-score** (ou Recall sur la classe « attaque », car une intrusion manquée coûte cher).

## 9. Critères de réussite
- Le modèle optimisé dépasse la baseline sur le jeu de test
- Les 3 méthodes d'optimisation sont comparées (score et temps)
- Le meilleur modèle est justifié avec sa configuration

## 10. Structure du projet
```
intrusion-check/
├── data/         données (non versionnées)
├── notebooks/    exploration, baseline, optimisation
├── src/          code réutilisable
├── results/      tableaux et graphiques
├── reports/      rapport final
├── environment.yml
└── README.md
```

## 11. Installation
```bash
conda create -n intrusion-detection python=3.11 -y
conda activate intrusion-detection
conda install -c conda-forge pandas numpy scikit-learn matplotlib seaborn jupyter -y
pip install optuna xgboost
```

## 12. Résultats
*À compléter : meilleur modèle, hyperparamètres optimaux, scores finaux.*