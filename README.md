# Prédire l'échec scolaire en mathématiques par Machine Learning

L'objectif est de construire un **système d'alerte précoce** qui repère les élèves risquant d'échouer en mathématiques (note finale < 10/20), afin que l'établissement puisse leur proposer un accompagnement à temps.

## Données

Le projet utilise le jeu de données *Student Performance* (P. Cortez et A. Silva, 2008, UCI Machine Learning Repository). Les données ont été collectées pendant l'année scolaire 2005-2006 dans deux lycées publics de la région de l'Alentejo, au Portugal : Gabriel Pereira (GP) et Mousinho da Silveira (MS). Elles proviennent des bulletins scolaires et de questionnaires remplis par les élèves.

Deux fichiers correspondent à deux matières :

| Fichier | Matière | Élèves | Répartition GP / MS | Élèves en échec (G3 < 10) |
|---|---|---|---|---|
| `student-mat.csv` | Mathématiques | 395 | 349 / 46 | 33 % |
| `student-por.csv` | Portugais | 649 | 423 / 226 | 15 % |

Chaque élève est décrit par 33 variables :
- **profil démographique et familial** : âge, sexe, milieu urbain ou rural, taille de la famille, niveau d'études et métier des parents ;
- **scolarité** : nombre d'échecs passés, temps d'étude hebdomadaire, soutien scolaire et familial, cours particuliers, absences, souhait de faire des études supérieures ;
- **mode de vie** : temps libre, sorties, consommation d'alcool en semaine et le week-end, état de santé, relation amoureuse ;
- **notes** sur 20 : G1 (1er trimestre), G2 (2e trimestre) et G3 (note finale, la cible).

Une partie des élèves suit les deux matières. Le script `student-merge.R` fourni avec les données les apparie sur 13 attributs communs et trouve 382 élèves ; notre notebook montre que cet appariement est en partie ambigu et n'en retient que 358 (section 7.3).

| Fichier | Contenu |
|---|---|
| `data/student-mat.csv` | Élèves du cours de mathématiques |
| `data/student-por.csv` | Élèves du cours de portugais |
| `data/student.txt` | Description détaillée des 33 variables |
| `data/student-merge.R` | Script d'appariement des élèves présents dans les deux fichiers |

Référence : P. Cortez et A. Silva, « Using Data Mining to Predict Secondary School Student Performance », *Proceedings of 5th FUture BUsiness TEChnology Conference (FUBUTEC 2008)*, Porto, 2008, p. 5-12.

## Démarche

Le notebook `projet_ml_reussite_scolaire.ipynb` suit les étapes suivantes :

1. Formulation du problème (classification binaire supervisée) et hypothèses
2. Exploration des données (distributions, box plots, corrélations)
3. Feature engineering et analyse non supervisée (ACP, K-means)
4. Apprentissage et comparaison de modèles (régression logistique, arbre, Random Forest, Gradient Boosting)
5. Réglage des hyperparamètres (GridSearchCV, validation croisée répétée)
6. Évaluation finale et interprétation (matrices de confusion, ROC, choix du seuil, importance des variables)
7. Analyses complémentaires : régression, fuite de données, apport du cours de portugais, équité, généralisation à un autre lycée, parcimonie
8. Conclusion et pistes de poursuite

Trois scénarios sont comparés selon le moment de la prédiction : à la rentrée (profil seul), après le 1er trimestre (+G1) et après le 2e trimestre (+G1, G2).

## Principaux résultats

- Après le 1er trimestre, le modèle retenu repère 25 des 26 élèves en échec du jeu de test.
- À la rentrée, il en repère environ 6 sur 10 ; cinq variables suffisent à obtenir ce résultat.
- La variable `absences` constitue une fuite de données (comptée sur toute l'année) et a été exclue des modèles.
- Retirer les variables sensibles (sexe, milieu, métier des parents) ne dégrade pas les performances.

## Lancer le projet

```bash
git clone <url-du-depot>
cd <nom-du-depot>
pip install -r requirements.txt
jupyter notebook projet_ml_reussite_scolaire.ipynb
```

Le notebook est déjà exécuté : les graphiques et résultats sont visibles directement sur GitHub. Une exécution complète prend quelques minutes. La graine aléatoire est fixée (42) pour la reproductibilité.

## Auteures

Céline Buob-Gandil, Lila Kacedan
