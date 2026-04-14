# Projet ML - Estimation du Risque d'Exposition des Bâtiments Historiques en Tunisie
Farah Fassi — G3

## Problématique

Comment estimer le risque d'exposition à la dégradation des bâtiments historiques tunisiens à partir de données ouvertes ?

##  Objectif

Construire un **Indice de Risque d'Exposition (IRE)** et un modèle de machine learning capable de classifier les bâtiments selon leur niveau de risque : **Stable**, **Élevé** ou **Critique**.

##  Structure du projet

**Niveaux de risque :**
| Catégorie | Score IRE |
|-----------|-----------|
| Stable | < 40 |
| Modéré | 40 - 60 |
| Élevé | 60 - 75 |
| Critique | > 75 |

##  Modélisation Machine Learning

### Approche : Classification supervisée

**Features utilisées :**
- `surface_m2` - Surface du bâtiment
- `lat`, `lon` - Coordonnées géographiques
- `humidite` - Humidité moyenne par ville
- `densite_pop` - Densité de population
- `protection_unesco` - Présence de classement UNESCO

**Modèles comparés :**
1. Régression Logistique
2. Random Forest
3. XGBoost (optimisé avec Optuna)

### Résultats

| Modèle | Accuracy | F1-Score (macro) |
|--------|----------|------------------|
| Régression Logistique | ~0.85 | ~0.82 |
| Random Forest | ~0.92 | ~0.90 |
| **XGBoost** | **0.998** | **0.988** |

### Meilleur modèle : XGBoost

**Performances par classe :**
| Classe | Précision | Recall | F1-Score | Support |
|--------|-----------|--------|----------|---------|
| Stable | 1.00 | 0.96 | 0.98 | 23 |
| Critique | 1.00 | 1.00 | 1.00 | 540 |

## Principaux enseignements (SHAP)

Les facteurs les plus importants pour la prédiction du risque sont :

1. **La surface** (`surface_m2`) - Les grands bâtiments sont plus vulnérables
2. **La localisation** (`lat`, `lon`) - Les zones côtières humides présentent plus de risques
3. **La densité de population** - Les zones urbaines denses augmentent la pression

##  Carte de risque interactive

Une carte Folium a été générée (`carte_risque_finale.html`) permettant de visualiser :

- Chaque bâtiment avec son niveau de risque (couleur)
- Informations détaillées au survol (nom, ville, IRE, risque)
- Légende intégrée des niveaux de risque

##  Visualisations clés

1. **Distribution de l'IRE** - Histogramme des scores
2. **IRE par ville** - Comparaison des moyennes
3. **Clustering K-Means** - Validation des catégories (k=4)
4. **Matrice de confusion** - Performance du modèle
5. **SHAP importance** - Impact des features

##  Recommandations pour l'INP

1. **Priorité immédiate** → Bâtiments classés "Critique" dans les zones humides de Tunis et Sousse
2. **Surveillance accrue** → Grands bâtiments non protégés (score surface élevé)
3. **Classement urgent** → Bâtiments IRE > 70 sans protection UNESCO

##  Technologies utilisées

| Librairie | Utilisation |
|-----------|-------------|
| Python 3.13 | Langage principal |
| Pandas/NumPy | Manipulation des données |
| Scikit-learn | ML (Random Forest, Logistic Regression) |
| XGBoost | Modélisation optimisée |
| Optuna | Optimisation des hyperparamètres |
| SHAP | Interprétabilité des modèles |
| Folium | Cartes interactives |
| Matplotlib/Seaborn | Visualisations |
| OSMnx | Collecte OpenStreetMap |

##  Exécution du projet

### Prérequis
```bash
pip install osmnx geopandas folium scikit-learn xgboost shap optuna matplotlib seaborn pandas numpy
