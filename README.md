# Projet 6 - Scoring Crédit

## Objectif

L'objectif de ce projet est de développer un modèle de machine learning capable de prédire le risque de défaut de paiement d'un client à partir des données fournies par Home Credit, tout en optimisant un coût métier et en assurant l'explicabilité des prédictions.

---

## Structure du projet

```
.
├── Projet_6.ipynb
├── pyproject.toml
├── uv.lock
├── README.md
├── mlflow.db
├── mlruns/
│
├── application_train.csv
├── application_test.csv
├── bureau.csv
├── bureau_balance.csv
├── previous_application.csv
├── POS_CASH_balance.csv
├── installments_payments.csv
├── credit_card_balance.csv
├── HomeCredit_columns_description.csv
├── sample_submission.csv
│
├── LightGBM_threshold_cost_curve.png
├── LogisticRegression_threshold_cost_curve.png
├── RandomForest_threshold_cost_curve.png
├── XGBoost_threshold_cost_curve.png
└── MLP_threshold_cost_curve.png
```

---

## Installation

Ce projet utilise **uv** pour la gestion de l'environnement Python.

Créer l'environnement et installer les dépendances :

```bash
uv sync
```

---

## Exécution

Lancer le notebook :

```bash
jupyter notebook Projet_6.ipynb
```

---

## Données

Les fichiers CSV du jeu de données **Home Credit Default Risk** doivent être placés à la racine du projet.

Les fichiers utilisés sont :

- application_train.csv
- application_test.csv
- bureau.csv
- bureau_balance.csv
- previous_application.csv
- POS_CASH_balance.csv
- installments_payments.csv
- credit_card_balance.csv
- HomeCredit_columns_description.csv
- sample_submission.csv

Etant donné leur volume respectif, ces derniers ne sont pas intégré dans le dépos github,  
il faut donc les télécharger à l'adresse suivante:  
  
https://www.kaggle.com/c/home-credit-default-risk/data

---

## Méthodologie

Le notebook réalise les étapes suivantes :

- Préparation et nettoyage des données.
- Feature engineering.
- Entraînement de plusieurs modèles :
  - Logistic Regression
  - Random Forest
  - XGBoost
  - LightGBM
  - MLP
- Validation croisée.
- Optimisation des hyperparamètres.
- Optimisation du seuil métier.
- Suivi des expérimentations avec MLflow.
- Enregistrement du meilleur modèle dans le Model Registry.
- Analyse de l'explicabilité avec SHAP.

---

## Reproductibilité

Les versions exactes des dépendances sont figées grâce au fichier `uv.lock`.

Pour recréer un environnement identique :

```bash
uv sync
```
## Lancer l'interface MLflow :

```bash
mlflow ui
```

Puis ouvrir dans un navigateur :

http://127.0.0.1:5000
