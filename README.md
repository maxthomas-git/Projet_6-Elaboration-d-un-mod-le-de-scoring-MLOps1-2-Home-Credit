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


## Serving du modèle avec MLflow

Le modèle final est enregistré dans le **MLflow Model Registry**. Il peut être servi localement à l'aide de MLflow.

### Lancer le serveur

Depuis la racine du projet :

```bash
mlflow models serve \
-m "models:/LightGBM/latest" \
--host 127.0.0.1 \
--port 5001 \
--env-manager local
```

Le serveur est alors accessible à l'adresse :

```
http://127.0.0.1:5001
```

### Tester le modèle servi

Depuis le notebook, une requête peut être envoyée au serveur avec un échantillon du jeu de test :

Exécuter le notebook jusqu'à l'enregistrement du modèle dans le Registry avant de lancer:

```python
sample = X_test.iloc[[270]]

payload = {
    "dataframe_split": {
        "columns": sample.columns.tolist(),
        "data": sample.values.tolist()
    }
}

response = requests.post(
    "http://127.0.0.1:5001/invocations",
    json=payload
)

print(response.status_code)
print(response.json())
```

Exemple de réponse :

```
200
{'predictions': [1]}
```

Ce test valide le bon déploiement du modèle et son utilisation via l'API REST de MLflow.
