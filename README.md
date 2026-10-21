# Prédire l'échec scolaire en mathématiques par Machine Learning

Projet de Machine Learning réalisé par Céline Buob-Gandil et Lila Kacedan dans le cadre d'un cours à l'ISAE-SUPAERO (2026-2027).

L'objectif est de construire un **système d'alerte précoce** qui repère les élèves risquant d'échouer en mathématiques (note finale < 10/20), afin que l'établissement puisse leur proposer un accompagnement à temps.

## Données

Jeu de données *Student Performance* (P. Cortez et A. Silva, 2008, UCI Machine Learning Repository) : 395 élèves de deux lycées portugais en mathématiques, et 649 en portugais.

| Fichier | Contenu |
|---|---|
| `data/student-mat.csv` | Élèves du cours de mathématiques |
| `data/student-por.csv` | Élèves du cours de portugais |
| `data/student.txt` | Description des 33 variables |
| `data/student-merge.R` | Script d'appariement des élèves présents dans les deux fichiers |

## Démarche

Le notebook `projet_ml_reussite_scolaire.ipynb` suit les étapes suivantes :

1. Formulation du problème (classification binaire supervisée) et hypothèses
2. Exploration des données (distributions, box plots, corrélations)
3. Feature engineering et analyse non supervisée (ACP, K-means)
4. Apprentissage et comparaison de modèles (Naive Bayes, SVM, arbre de décision, Random Forest, Gradient Boosting)
5. Réglage des hyperparamètres (GridSearchCV, validation croisée répétée)
6. Évaluation finale et interprétation (matrices de confusion, ROC, choix du seuil, importance des variables)
7. Analyses complémentaires : régression, fuite de données, apport du cours de portugais, équité, généralisation à un autre lycée, parcimonie
8. Conclusion et pistes de poursuite

Trois scénarios sont comparés selon le moment de la prédiction : à la rentrée (profil seul), après le 1er trimestre (+G1) et après le 2e trimestre (+G1, G2).

## Principaux résultats

- Après le 1er trimestre, le modèle retenu repère 26 des 27 élèves en échec du jeu de test.
- À la rentrée, il en repère environ un sur deux : le signal du profil est réel mais diffus.
- La variable `absences` constitue une fuite de données (comptée sur toute l'année) et a été exclue des modèles.
- Retirer les variables sensibles (sexe, milieu, métier des parents) ne dégrade presque pas les performances.

## Lancer le projet

```bash
git clone <url-du-depot>
cd <nom-du-depot>
pip install -r requirements.txt
jupyter notebook projet_ml_reussite_scolaire.ipynb
```

Le notebook est déjà exécuté : les graphiques et résultats sont visibles directement sur GitHub. Une exécution complète prend quelques minutes. La graine aléatoire est fixée (42) pour la reproductibilité.

## Autrices

Céline Buob-Gandil et Lila Kacedan, ISAE-SUPAERO
