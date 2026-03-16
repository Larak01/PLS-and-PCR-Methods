# 🍷 Analyse de la Qualité du Vin : PLS vs PCR

[cite_start]Ce projet présente une étude comparative entre deux méthodes de régression par réduction de dimension : la **Régression des Moindres Carrés Partiels (PLS)** [cite: 5, 21] [cite_start]et la **Régression sur Composantes Principales (PCR)**[cite: 5, 61]. [cite_start]L'objectif est de prédire le score de qualité du vin rouge en utilisant ses caractéristiques physico-chimiques tout en gérant les problèmes de multicolinéarité[cite: 16, 18, 19].

## 📌 Présentation du Projet
[cite_start]Dans le jeu de données "Wine Quality", les variables (comme l'acidité fixe et la densité) sont fortement corrélées (corrélation de 0,67), ce qui rend l'utilisation d'une régression linéaire classique instable[cite: 20]. Nous utilisons donc :

* [cite_start]**PCR (Principal Component Regression) :** Une méthode **non-supervisée** qui crée des composantes basées uniquement sur la variance des prédicteurs, sans regarder la cible $Y$[cite: 63, 64, 71].
* [cite_start]**PLS (Partial Least Squares) :** Une méthode **supervisée** qui construit des composantes en maximisant la covariance entre les prédicteurs et la cible $Y$[cite: 24, 25, 31].

## 📊 Méthodologie
* [cite_start]**Prétraitement :** Standardisation des données (`StandardScaler`) pour que chaque variable contribue équitablement, peu importe son unité[cite: 41, 43].
* [cite_start]**Validation :** Découpage 80% entraînement / 20% test avec un état aléatoire fixe pour la reproductibilité[cite: 44].
* [cite_start]**Optimisation :** Sélection du nombre optimal de composantes via `GridSearchCV` avec une validation croisée à 5 plis (5-fold CV) en minimisant la RMSE[cite: 45, 46].

## 📈 Résultats Comparatifs
[cite_start]Le tableau ci-dessous résume les performances obtenues sur l'ensemble de test[cite: 114]:

| Métrique | PCR | PLS |
| :--- | :---: | :---: |
| **Nombre de composantes optimal** | [cite_start]**10** [cite: 87] | [cite_start]**4** [cite: 51] |
| **RMSE (Erreur moyenne)** | [cite_start]0.6241 [cite: 90, 114] | [cite_start]0.6254 [cite: 54, 114] |
| **MAE (Erreur absolue moyenne)** | [cite_start]0.5034 [cite: 90, 114] | [cite_start]0.5028 [cite: 54, 114] |
| **R² (Variance expliquée)** | [cite_start]40.41% [cite: 90, 114] | [cite_start]40.15% [cite: 54, 114] |

## 💡 Conclusions Clés
1.  [cite_start]**Efficacité de la PLS :** La PLS atteint une précision quasiment identique à la PCR tout en utilisant seulement **4 composantes au lieu de 10**[cite: 116, 119]. [cite_start]Cela représente une réduction de dimension 60% plus efficace[cite: 119].
2.  [cite_start]**Interprétabilité :** Grâce à son approche supervisée, la PLS élimine mieux le "bruit" pour ne garder que les informations pertinentes pour la prédiction[cite: 104, 110, 124].
3.  [cite_start]**Limites :** Les deux modèles expliquent environ 40% de la variance, ce qui souligne que les propriétés physico-chimiques seules ne suffisent pas à prédire totalement la qualité, qui dépend aussi de facteurs subjectifs[cite: 128, 129].

---
[cite_start]*Projet réalisé dans le cadre du cours d'Économétrie / Sélection Automatique (Année Académique 2025-2026).* [cite: 7, 8, 13]
