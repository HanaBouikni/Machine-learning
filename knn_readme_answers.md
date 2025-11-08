# TP KNN - Classification d'Emails Spam
## Réponses aux Questions

---

## Q1. Plot the training data
**Réponse:** Le graphique de visualisation a été généré et sauvegardé dans `training_data_plot.png`.

- **Points bleus (cercles)** : Emails normaux (label 0)
- **Points rouges (carrés)** : Emails spam (label 1)
- **Point vert (étoile)** : Nouvel email à classifier [2 links, 1 spam keyword]

---

## Q3. Questions

### 1. What does each feature represent in this dataset?

**Réponse:**
- **Feature 1 (X[:,0])** : **Number of links in the email** (Nombre de liens dans l'email)
- **Feature 2 (X[:,1])** : **Number of spam-related keywords** (Nombre de mots-clés liés au spam)

Ces deux caractéristiques simples sont utilisées pour distinguer les emails normaux des emails spam.

---

### 2. For K=1, 3, 5 → which prediction is correct compared to the true label?

**Réponse:**

Le nouvel email à classifier a les caractéristiques : **[2 links, 1 spam keyword]**  
Le vrai label (y_true) est : **1 (Spam)**

| K | Prédiction | Label | Correct ? | MAE |
|---|------------|-------|-----------|-----|
| **K=1** | 0 (Normal) | 1 (Spam) | ❌ INCORRECT | 1.0 |
| **K=3** | 1 (Spam) | 1 (Spam) | ✅ CORRECT | 0.0 |
| **K=5** | 1 (Spam) | 1 (Spam) | ✅ CORRECT | 0.0 |

**Conclusion:** Les prédictions pour **K=3 et K=5 sont correctes**.

**Explication:**
- **K=1** : Le voisin le plus proche est probablement [1, 2] (label 0), donc prédiction incorrecte
- **K=3** : La majorité des 3 plus proches voisins sont des emails spam, donc prédiction correcte
- **K=5** : La majorité des 5 plus proches voisins sont des emails spam, donc prédiction correcte

---

### 3. Which K has the lowest MAE?

**Réponse:**

**K=3 et K=5 ont le MAE le plus bas : 0.0**

Le MAE (Mean Absolute Error) mesure l'erreur moyenne absolue entre les prédictions et les vraies valeurs:
- K=1 : MAE = 1.0 (erreur maximale car mauvaise prédiction)
- K=3 : MAE = 0.0 (prédiction parfaite)
- K=5 : MAE = 0.0 (prédiction parfaite)

---

### 4. Why can choosing a large value of K (such as K = 5) in K-Nearest Neighbors lead to incorrect or less accurate predictions?

**Réponse:**

Choisir une **grande valeur de K** peut mener à des prédictions incorrectes ou moins précises pour plusieurs raisons :

#### **1. Surlis­sage (Over-smoothing)**
- Avec un K élevé, l'algorithme considère trop de voisins, ce qui peut diluer l'influence des points les plus proches et pertinents
- Le modèle devient trop généralisé et perd en précision sur les détails locaux

#### **2. Inclusion de voisins non pertinents**
- Dans un dataset déséquilibré ou avec des frontières de décision complexes, un K élevé peut inclure des points de l'autre classe qui sont loin
- Par exemple, si un email normal est entouré majoritairement d'emails spam mais qu'à grande distance il y a beaucoup d'emails normaux, K=5 pourrait mal le classifier

#### **3. Perte de sensibilité aux variations locales**
- Les patterns locaux et les nuances dans les données sont ignorés
- Le modèle devient moins capable de capturer les frontières de décision complexes

#### **4. Impact de la classe majoritaire**
- Dans un dataset déséquilibré, un K élevé favorise toujours la classe majoritaire
- Cela peut mener à une mauvaise classification des classes minoritaires

#### **5. Augmentation du biais**
- Trade-off biais-variance : 
  - **K petit (ex: K=1)** : faible biais, haute variance (overfitting)
  - **K grand (ex: K=5)** : haut biais, faible variance (underfitting)

**Dans notre cas spécifique:** Avec seulement 7 points d'entraînement, K=5 fonctionne bien, mais dans des datasets plus grands et complexes, un K trop élevé peut significativement réduire la précision.

**Règle générale:** La valeur optimale de K est généralement trouvée par validation croisée, en testant plusieurs valeurs et en choisissant celle qui donne les meilleures performances sur un ensemble de validation.

---
