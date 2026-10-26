# 🐔 Analyse de données d'élevage avicole : statistiques, ACP et méthodes d'ensemble

Projet réalisé dans le cadre du Master Data Science (UPEC), module *Analyse et Traitement de Données Numériques*.

**Objectif** : analyser les données d'un élevage de poulets (poids, alimentation, conditions d'enclos, survie, coûts), détecter les valeurs aberrantes, réduire la dimension des données et tester des modèles pour prédire la survie et le gain de poids.

## 🎯 Résultats clés

- **Valeurs aberrantes** : la méthode de l'écart interquartile (IQR) ne détecte aucune valeur aberrante, alors que le Z-score avec un seuil de 1 en signale plus de 80 par variable. Ce seuil est trop strict : on utilise habituellement 3.
- **Tests statistiques** : aucune variable ne suit une loi normale (Shapiro-Wilk, p < 0,001). Le poids ne diffère pas significativement selon le groupe d'âge (test t : p = 0,88 ; ANOVA : p = 0,72).
- **Réduction de dimension** : comparaison de l'ACP (calculée à la main à partir de la matrice de covariance) et de l'ACP à noyau (linéaire, RBF, polynomial). Le noyau RBF sépare mieux les profils.
- **Prédiction de la survie** (taux ≥ 90 %) par forêt aléatoire : accuracy et F1-score de 60 %, avec analyse de l'importance des variables.
- **Prédiction du gain de poids** : AdaBoost (R² = −0,21) et Gradient Boosting (R² = −0,56) ne font pas mieux qu'une prédiction par la moyenne.

## 📊 Données

200 poulets décrits par 8 variables : poids (g), nourriture consommée (g/jour), température et humidité de l'enclos, âge (jours), gain de poids (g/jour), taux de survie (%) et coût d'élevage (FCFA).

## 🛠️ Démarche

1. **Statistiques descriptives** : moyenne, médiane, variance, écart-type, quartiles, histogrammes et boxplots.
2. **Détection des valeurs aberrantes** : comparaison du Z-score et de l'IQR, boxplot annoté.
3. **Tests statistiques** : normalité (Shapiro-Wilk), test t de Student et ANOVA entre groupes d'âge.
4. **ACP** : centrage, matrice de covariance, valeurs et vecteurs propres, variance expliquée et projection sur deux composantes.
5. **ACP à noyau** (KernelPCA) sur données standardisées, avec trois noyaux.
6. **Méthodes d'ensemble** : forêt aléatoire pour la survie, AdaBoost et Gradient Boosting pour le gain de poids.

## 🔍 Analyse critique et limites

- **ACP sans standardisation** : les deux premières composantes expliquent 99,9 % de la variance, mais surtout parce que le coût (en FCFA) et le poids (en grammes) ont des valeurs beaucoup plus grandes que les autres variables. Standardiser les données avant l'ACP, comme pour l'ACP à noyau, donnerait une image plus juste.
- **Petit jeu de données** (200 lignes) et un seul découpage entraînement / test : les scores sont instables. Une validation croisée serait plus fiable.
- **Peu de signal prédictif** : les variables disponibles expliquent mal la survie et le gain de poids. Les R² négatifs montrent que les modèles de boosting apprennent du bruit.

## 🧰 Outils

Python · pandas · NumPy · SciPy · scikit-learn · Matplotlib · seaborn · Jupyter

## 📁 Fichiers

```
├── analyse_elevage.ipynb       # Notebook complet
├── rapport_analyse.pdf         # Rapport d'analyse
└── donnees_elevage_poulet.csv  # Données
```

## 👩‍💻 Autrice

**Ndeye Aminata Gadiaga**
[LinkedIn](https://linkedin.com/in/ndeye-aminata-gadiaga-26a97725b) · [GitHub](https://github.com/AMINATA1999)
