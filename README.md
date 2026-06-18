# fraud-detection-iard

#  Détection de Fraude en Assurance Auto — Classification supervisée (Python)

Classification supervisée sur un portefeuille de sinistres auto —
comparaison de modèles Machine Learning avec gestion du déséquilibre des classes.

---

## Contexte métier

La fraude à l'assurance auto représente entre 5 et 10% des sinistres déclarés.
Traditionnellement détectée manuellement par des experts, elle peut être
identifiée automatiquement en apprenant les patterns caractéristiques
à partir de l'historique des sinistres.

**Objectif :** prédire si un sinistre est frauduleux à partir des informations
disponibles au moment de la déclaration.

---

## Dataset

- **Source :** Auto Insurance Claims Data (Kaggle)
- **Volume :** 1 000 sinistres auto, 40 variables
- **Variable cible :** `fraud_reported` — Y (fraude) / N (non-fraude)
- **Déséquilibre :** 75% non-fraude / 25% fraude

---

## Pipeline

### 1. Exploration
- Distribution de la variable cible → identification du déséquilibre
- Taux de fraude par variable catégorielle
- Matrice de corrélation → détection de la multicolinéarité

### 2. Preprocessing
- Suppression des colonnes non informatives (identifiants, dates, redondances)
- Imputation des valeurs manquantes (mode pour catégorielles, médiane pour numériques)
- Label Encoding des variables catégorielles
- Séparation train/test 80/20 stratifiée
- **SMOTE appliqué sur le train set uniquement** → rééquilibrage 50/50
- Normalisation StandardScaler

### 3. Modèles comparés

| Modèle | Famille | Rôle |
|:---|:---|:---|
| Régression Logistique | Linéaire | Baseline interprétable |
| Random Forest | Ensemble - bagging | Robuste, feature importance |
| XGBoost | Ensemble - boosting | Performance maximale |

### 4. Evaluation
- Métrique prioritaire : **Recall** (minimiser les fraudes non détectées)
- AUC-ROC, Precision, F1-Score
- Matrices de confusion
- Courbes ROC comparatives
- Feature importance

---

## Résultats

| Modèle | Recall | AUC-ROC | Fraudes manquées |
|:---|:---|:---|:---|
| Régression Logistique | 0.571 | 0.792 | 21 sur 49 |
| Random Forest | 0.612 | 0.832 | 19 sur 49 |
| XGBoost | 0.673 | 0.812 | 16 sur 49 |

**Meilleur modèle retenu : XGBoost**
- Meilleur Recall (0.673) → détecte le plus de fraudes
- Manque seulement 16 sinistres frauduleux sur 49

> En contexte assurantiel, le Recall est la métrique prioritaire :
> manquer une fraude a un coût financier direct pour l'assureur.

---

## Variables les plus prédictives

Les deux modèles d'ensemble s'accordent sur le top 2 :

1. **`incident_severity`** : les fraudeurs déclarent systématiquement
   des dommages graves pour maximiser le remboursement
2. **`insured_hobbies`** : certains loisirs déclarés sont statistiquement
   très corrélés à la fraude — signal non intuitif détecté automatiquement

---

## Points méthodologiques clés

- **SMOTE uniquement sur le train set** : appliquer SMOTE avant la séparation
  contaminerait le test set et gonflerait artificiellement les performances
- **Recall > Accuracy** : avec 75% de non-fraudes, un modèle naïf aurait
  75% d'accuracy en prédisant toujours non-fraude
- **Seuil calibrable** : le seuil de 0.5 est ajustable selon le coût relatif
  d'un faux négatif vs faux positif — décision métier, pas technique

---

## Stack technique

![Python](https://img.shields.io/badge/Python-3.10-blue)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.2-orange)
![XGBoost](https://img.shields.io/badge/XGBoost-1.7-green)

- **Langage :** Python
- **Librairies :** Scikit-learn, XGBoost, Imbalanced-learn, Pandas, Matplotlib, Seaborn
- **Environnement :** Jupyter Notebook (Anaconda)

---

## Installation

```bash
pip install scikit-learn xgboost imbalanced-learn pandas matplotlib seaborn
```

## Utilisation

Ouvrir `fraud_detection.ipynb` dans Jupyter Notebook et exécuter les cellules
dans l'ordre — le notebook est structuré en 4 modules progressifs.

---

## Auteur

**Hasina Raveloson**
M2 Actuariat — ISUP Sorbonne
[LinkedIn](https://linkedin.com/in/hasina-raveloson) · [GitHub](https://github.com/Raveloson-Sarobidy)
