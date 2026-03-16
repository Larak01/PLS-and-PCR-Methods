# 🍷 Analyse de la Qualité du Vin : PLS vs PCR

Ce projet présente une étude comparative entre deux méthodes de régression par réduction de dimension : la **Régression des Moindres Carrés Partiels (PLS)** et la **Régression sur Composantes Principales (PCR)**. L'objectif est de prédire le score de qualité du vin rouge en utilisant ses caractéristiques physico-chimiques tout en gérant les problèmes de multicolinéarité.

## 📌 Présentation du Projet
Dans le jeu de données "Wine Quality", les variables (comme l'acidité fixe et la densité) sont fortement corrélées (corrélation de 0,67), ce qui rend l'utilisation d'une régression linéaire classique instable. Nous utilisons donc :

* **PCR (Principal Component Regression) :** Une méthode **non-supervisée** qui crée des composantes basées uniquement sur la variance des prédicteurs, sans regarder la cible Y.
* **PLS (Partial Least Squares) :** Une méthode **supervisée** qui construit des composantes en maximisant la covariance entre les prédicteurs et la cible Y.

## 📊 Méthodologie
* **Prétraitement :** Standardisation des données (`StandardScaler`) pour que chaque variable contribue équitablement, peu importe son unité.
* **Validation :** Découpage 80% entraînement / 20% test avec un état aléatoire fixe pour la reproductibilité.
* **Optimisation :** Sélection du nombre optimal de composantes via `GridSearchCV` avec une validation croisée à 5 plis (5-fold CV) en minimisant la RMSE.

## 📈 Résultats Comparatifs
Le tableau ci-dessous résume les performances obtenues sur l'ensemble de test :

| Métrique | PCR | PLS |
| :--- | :---: | :---: |
| **Nombre de composantes optimal** | **10** | **4** |
| **RMSE (Erreur moyenne)** | 0.6241 | 0.6254 |
| **MAE (Erreur absolue moyenne)** | 0.5034 | 0.5028 |
| **R² (Variance expliquée)** | 40.41% | 40.15% |

## 💡 Conclusions Clés
1.  **Efficacité de la PLS :** La PLS atteint une précision quasiment identique à la PCR tout en utilisant seulement **4 composantes au lieu de 10**. Cela représente une réduction de dimension 60% plus efficace.
2.  **Interprétabilité :** Grâce à son approche supervisée, la PLS élimine mieux le "bruit" pour ne garder que les informations pertinentes pour la prédiction.
3.  **Limites :** Les deux modèles expliquent environ 40% de la variance, ce qui souligne que les propriétés physico-chimiques seules ne suffisent pas à prédire totalement la qualité, qui dépend aussi de facteurs subjectifs.

---
*Projet réalisé dans le cadre du cours d'Économétrie / Sélection Automatique (Année Académique 2025-2026).*
