## Photo personnelle

<img src="akharazfatimazahra.jpeg" style="height:464px;margin-right:432px"/>

**Numéro d'étudiant** : 24010341

**Classe** : CAC1

[compte_rendu_heart_disease.md](https://github.com/user-attachments/files/24082548/compte_rendu_heart_disease.md)
# 📘 GRAND GUIDE : ANATOMIE D'UN PROJET DATA SCIENCE — HEART DISEASE EDITION

---

## 1. 🎯 Contexte Métier et Mission

### Le Problème (Business Case)
Les maladies cardiovasculaires sont l’une des premières causes de mortalité dans le monde. Leur détection précoce repose souvent sur l’analyse d’indicateurs cliniques : ECG, pression artérielle, cholestérol, etc.

**Objectif :** Construire un modèle prédictif capable d’estimer la probabilité qu’un patient souffre d’une maladie cardiaque.

**Enjeu critique :**
- **Faux Négatif (FN)** : considérer un patient malade comme sain → risque vital.
- **Faux Positif (FP)** : considérer un patient sain comme malade → stress + examens coûteux.

Dans ce contexte, **le Recall (Sensibilité)** est la métrique prioritaire.

### Les Données (Input)
Nous utilisons le **Heart Disease UCI Dataset**.

- **X (features)** : âge, sexe, pression sanguine, cholestérol, fréquence cardiaque maximale, douleurs thoraciques, résultats ECG, etc.
- **y (target)** : indicateur binaire (0 = pas de maladie, 1 = maladie).

---

## 2. 🧪 Le Code Python (Laboratoire)

Ce code se base sur votre script avec :
- Nettoyage des données
- Préparation des variables
- Split Train/Test
- Modélisation via **Random Forest Classifier**

```python
from sklearn.ensemble import RandomForestClassifier
model = RandomForestClassifier(n_estimators=100, random_state=42)
model.fit(X_train, y_train)
```

L’algorithme utilisé est donc **Random Forest**, robuste et performant pour les données tabulaires.

---

## 3. 🔧 Analyse Approfondie : Nettoyage (Data Wrangling)

### Pourquoi nettoyer ?
Les valeurs `NaN` perturbent complètement les calculs matriciels. Elles doivent donc être imputées.

### Stratégie adoptée
- Variables numériques : imputation par **médiane** (résistant aux valeurs extrêmes)
- Variables catégorielles : imputation par **mode**
- Conversion des colonnes booléennes (`fbs`, `exang`)

### Attention au Data Leakage
L’imputation doit idéalement se faire **après** le split (Train puis Test), pas avant.

---

## 4. 🔍 Analyse Exploratoire (EDA)

Les analyses effectuées dans votre script incluent :
- **Heatmap de corrélations**
- **Histogrammes**
- **Scatter plots** (relations entre features et maladie)

### Observations principales
- `thalach` (fréquence max) est négativement corrélé avec la maladie.
- `oldpeak`, `ca`, et `exang` sont fortement associés à la présence de maladie.
- Certaines variables présentent une forte asymétrie.

---

## 5. 🔬 Analyse Méthodologique (Split)

Le split utilisé :

```python
train_test_split(X, y, test_size=0.2, random_state=42, stratify=y)
```

### Rappels importants :
- **80/20** est un standard équilibré.
- `random_state=42` assure la reproductibilité.
- `stratify=y` maintient la proportion malade/sain dans les deux ensembles.

---

## 6. 🌲 Focus Théorique : Random Forest

Cet algorithme fonctionne selon trois mécanismes :

### A. Les arbres de décision (faibles mais rapides)
Un arbre seul a une **haute variance** : il surapprend facilement.

### B. Le bagging (stabilisation)
Chaque arbre s’entraîne sur :
- un **échantillon bootstrap** (patients tirés aléatoirement avec remise),
- un **sous-ensemble aléatoire de colonnes**.

Cela crée une diversité d’arbres → robustesse.

### C. Le vote majoritaire
Chaque arbre “vote”.  
Le modèle final suit l’opinion majoritaire → meilleure généralisation.

---

## 7. 📊 Évaluation du Modèle (L'Heure de Vérité)

### Matrice de Confusion
Les 4 types de prédictions sont analysés :
- **TP** : malade bien détecté
- **TN** : sain correctement identifié
- **FP** : faux alarmes
- **FN** : patients malades non détectés → critique

### Métriques
L’accuracy seule est trompeuse.  
On privilégie :
- **Recall** (éviter les FN),
- **Precision** (fiabilité des alertes),
- **F1-score** : compromis global.

---

## 🎯 Conclusion Finale

Ce projet montre que :
- la compréhension métier est essentielle,
- la Data Science est un processus structuré,
- le Random Forest convient bien aux données médicales tabulaires,
- l’évaluation doit se concentrer sur la sécurité (Recall),
- une bonne pipeline (nettoyage → EDA → split → modèle → audit) garantit la fiabilité du système.

Ce rapport constitue une base solide pour un projet académique ou une application médicale plus poussée.
