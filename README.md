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
