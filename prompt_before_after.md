# Exemples Avant/Après : Optimisation de Prompts

## 🎯 Guide de lecture

Pour chaque exemple :
- ❌ **AVANT** : Le prompt problématique
- ⚠️ **PROBLÈMES** : Ce qui ne va pas
- ✅ **APRÈS** : Le prompt optimisé
- 💡 **POURQUOI C'EST MIEUX** : Les améliorations apportées
- 📊 **IMPACT** : Différence dans la qualité de réponse

---

## Exemple 1 : Question vague sur le chargement de données

### ❌ AVANT
```
comment charger un csv en python
```

### ⚠️ PROBLÈMES
- Trop vague et générique
- Aucun contexte sur le CSV (taille, problèmes, contraintes)
- Pas d'indication sur le niveau de détail souhaité
- L'IA va donner une réponse "tutoriel débutant"

### ✅ APRÈS
```markdown
## Contexte
- Python 3.11, pandas 2.1
- CSV de 3 Go avec 50 colonnes
- Séparateur : point-virgule
- Encoding : latin-1
- Problème : RAM limitée à 8 Go

## Objectif
Charger ce CSV sans saturer la mémoire

## Question
Quelle approche recommandes-tu ? 
Options : chunksize, colonnes sélectives, ou autre ?
```

### 💡 POURQUOI C'EST MIEUX
- Contexte technique précis (versions, taille)
- Problématique claire (contrainte RAM)
- Spécificités du CSV mentionnées
- Question ciblée avec options envisagées

### 📊 IMPACT
- **Avant** : Réponse générique `pd.read_csv('file.csv')`
- **Après** : Code optimisé avec `usecols`, `dtype`, `chunksize` et comparaison des approches

---

## Exemple 2 : Debugging sans contexte

### ❌ AVANT
```
j'ai une erreur avec mon code pandas aide moi

df.merge(df2)
```

### ⚠️ PROBLÈMES
- Pas de message d'erreur fourni
- Contexte des DataFrames absent (colonnes, types)
- Code incomplet (comment sont créés df et df2 ?)
- Pas d'explication de l'objectif du merge

### ✅ APRÈS
```markdown
## Problème
Erreur lors d'un merge de deux DataFrames pandas

## Erreur complète
ValueError: You are trying to merge on object and int64 columns

## Code
```python
df_sales = pd.read_csv('sales.csv')
df_customers = pd.read_csv('customers.csv')
result = pd.merge(df_sales, df_customers, on='customer_id')

## Structure des données
df_sales :
- customer_id : dtype object, exemples : "C001", "C002", "C003"
- amount : float64
- date : datetime64

df_customers :
- customer_id : dtype int64, exemples : 1, 2, 3
- name : object
- region : object

## Objectif
Joindre les ventes avec les infos clients pour enrichir l'analyse

## Question
Comment résoudre cette incohérence de types sur la clé de jointure ?
```
### 💡 POURQUOI C'EST MIEUX
- Message d'erreur complet fourni
- Code contextuel (pas juste la ligne qui plante)
- Structure détaillée des DataFrames avec exemples de valeurs
- Objectif métier explicité
- Question précise

### 📊 IMPACT
- **Avant** : L'IA devine qu'il y a un problème de types (mais lequel ?)
- **Après** : Solution précise avec explication du problème d'incohérence format string vs int, et 3 approches de résolution

## Exemple 3 : Choix de modèle trop général

### ❌ AVANT

```
quel modèle de machine learning utiliser pour mon projet ?
```

### ⚠️ PROBLÈMES
- Aucune info sur le type de problème (classification, régression, etc.)
- Pas de détails sur les données
- Contraintes inconnues
- L'IA ne peut que lister tous les modèles possibles

### ✅ APRÈS
```markdown
## Contexte du projet
Prédiction du churn client pour une plateforme SaaS B2B

## Données
- Volume : 50k clients (historique 2 ans)
- Features : 35 colonnes
  - 20 numériques : métriques d'usage (logins/mois, features utilisées, tickets support)
  - 10 catégorielles : plan tarifaire, industrie, taille entreprise
  - 5 temporelles : ancienneté, dernière connexion, date dernier paiement
- Cible : Churn dans les 3 prochains mois (binaire)
- Déséquilibre : 80% rétention, 20% churn

## Objectifs métier
- Priorité : **Recall élevé** (on veut détecter un maximum de churners)
- Precision acceptable : > 40% (pour limiter les faux positifs)
- **Explicabilité importante** : équipe métier doit comprendre les prédictions

## Contraintes techniques
- Inférence : batch quotidien (pas de temps réel)
- Temps d'entraînement : peut aller jusqu'à quelques heures
- Déploiement : environnement Python standard (sklearn, xgboost OK)

## Question
Quels modèles recommandes-tu pour ce cas d'usage ? 
Peux-tu comparer 3-4 options avec leurs avantages/inconvénients 
en tenant compte de mes contraintes ?
```

### 💡 POURQUOI C'EST MIEUX
- Type de problème clair (classification binaire déséquilibrée)
- Caractéristiques des données détaillées
- Contraintes métier explicites (recall vs precision, explicabilité)
- Contraintes techniques précisées
- Demande structurée (comparaison de plusieurs options)

### 📊 IMPACT
- **Avant** : Liste générique de modèles sans justification
- **Après** : Recommandation ciblée (ex : XGBoost, Random Forest, LightGBM) avec analyse comparative basée sur les critères explicabilité/performance, paramètres suggérés, et plan de mise en œuvre

---

## Exemple 4 : Optimisation de code sans contexte

### ❌ AVANT
```
mon code est trop lent comment accélérer

for i in range(len(df)):
    df.loc[i, 'new'] = df.loc[i, 'a'] * 2
```

### ⚠️ PROBLÈMES
- Taille du DataFrame inconnue (1000 lignes ou 10 millions ?)
- Pas d'info sur la complexité réelle du calcul
- Environnement et ressources non précisés
- Définition de "trop lent" absente (2 secondes ou 2 heures ?)

### ✅ APRÈS
~~~markdown
## Problème de performance
Traitement trop lent sur un DataFrame pandas

## Contexte
- DataFrame : 5 millions de lignes, 30 colonnes
- Environnement : serveur 32 Go RAM, 8 CPU cores
- Temps actuel : 45 minutes
- Objectif : < 5 minutes

## Code actuel

```python
# Calcul d'un score composite basé sur plusieurs conditions
for i in range(len(df)):
    if df.loc[i, 'type'] == 'premium':
        if df.loc[i, 'usage'] > 1000:
            df.loc[i, 'score'] = df.loc[i, 'base_score'] * 1.5
        else:
            df.loc[i, 'score'] = df.loc[i, 'base_score'] * 1.2
    elif df.loc[i, 'type'] == 'standard':
        df.loc[i, 'score'] = df.loc[i, 'base_score'] * 0.9
    else:
        df.loc[i, 'score'] = df.loc[i, 'base_score']
```
## Ce que j'ai déjà essayé
- `df.apply()` avec axis=1 → encore plus lent (52 minutes)
- Réduction du DataFrame → même problème sur subset

## Question
Comment vectoriser ce calcul avec numpy/pandas ?
Y a-t-il d'autres approches (Dask, numba, parallélisation) ?

~~~

### 💡 POURQUOI C'EST MIEUX
- Échelle du problème quantifiée (5M lignes, 45 min)
- Code complet avec la logique métier
- Objectif de performance chiffré
- Tentatives précédentes documentées
- Ressources disponibles précisées
- Questions spécifiques sur les approches

### 📊 IMPACT
- **Avant** : Suggestion basique de vectorisation
- **Après** : Solution complète avec `np.select()`, comparaison de performance estimée (1000x plus rapide), alternative avec `pd.cut()` pour catégoriser, et code de benchmark

---

## Exemple 5 : Feature engineering sans direction

### ❌ AVANT
```
donne moi des idées de features pour mon modèle
```

### ⚠️ PROBLÈMES
- Type de problème inconnu
- Données disponibles non spécifiées
- Objectif métier absent
- L'IA va donner des features génériques et probablement non pertinentes

### ✅ APRÈS
```markdown
## Contexte métier
Prédiction du montant d'achat pour une campagne marketing e-commerce

## Données disponibles
**Historique client (12 mois)** :
- Démographiques : âge, région, catégorie socio-pro
- Comportement : nb visites/mois, temps sur site, nb pages vues
- Transactionnel : nb achats, montant total dépensé, panier moyen
- Engagement : ouverture emails (oui/non), clics, nb produits en wishlist
- Temporel : date première visite, date dernier achat, ancienneté

**Données produits** :
- Catégories consultées (top 3)
- Produits achetés (avec prix et catégorie)
- Produits abandonnés en panier

## Target
Montant d'achat dans les 30 prochains jours (régression)

## Insights métier
- Les clients qui réduisent leur fréquence d'achat tendent à dépenser moins
- Les achats sont très saisonniers (pics en fin de mois)
- La catégorie "premium" a des patterns différents

## Question
Suggère 15 features engineerées pertinentes qui capturent :
1. Les tendances comportementales (augmentation/baisse activité)
2. Les patterns temporels (saisonnalité, récence)
3. Les signaux d'engagement
4. Les interactions entre variables

Pour chaque feature :
- Nom explicite
- Logique métier
- Code Python (pandas/numpy)
- Hypothèse sur son pouvoir prédictif
```

### 💡 POURQUOI C'EST MIEUX
- Contexte métier clair (e-commerce, prédiction montant)
- Données disponibles exhaustivement listées
- Type de problème précisé (régression)
- Insights métier partagés (aide l'IA à contextualiser)
- Demande structurée avec critères spécifiques
- Format de réponse attendu défini

### 📊 IMPACT
- **Avant** : Features génériques (RFM, moyennes, etc.)
- **Après** : 15 features sur-mesure comme `purchase_acceleration`, `category_diversity_score`, `weekend_vs_weekday_ratio`, `days_since_last_premium_purchase`, avec code et justification métier

---

## Exemple 6 : Explication de concept trop vague

### ❌ AVANT
```
c'est quoi la régularisation ?
```

### ⚠️ PROBLÈMES
- Niveau de détail inconnu (explication pour débutant ou expert ?)
- Contexte d'utilisation absent
- Type d'explication souhaité non précisé (théorique, pratique, code ?)

### ✅ APRÈS
```markdown
## Contexte
Je suis en Master 1 Data Science, j'ai des bases en algèbre linéaire 
et en ML (régression linéaire, logistique)

## Situation
J'implémente un modèle de régression Ridge pour prédire des prix immobiliers.
Je comprends que Ridge utilise de la régularisation, mais je n'ai pas 
l'intuition de comment ça fonctionne.

## Question
Peux-tu m'expliquer la régularisation L2 (Ridge) :

1. **Intuition simple** : À quoi ça sert concrètement ?
2. **Maths** : Formulation mathématique (sans aller trop loin)
3. **Impact** : Comment ça modifie les coefficients du modèle ?
4. **Pratique** : 
   - Quand l'utiliser vs régression linéaire simple ?
   - Comment choisir le paramètre alpha ?
   - Exemple de code avec scikit-learn

5. **Comparaison** : Différence avec Lasso (L1) en quelques mots

Format : Progressif du simple au complexe, avec un exemple concret
```

### 💡 POURQUOI C'EST MIEUX
- Niveau d'expertise précisé
- Contexte d'utilisation concret (Ridge pour prix immobiliers)
- Questions structurées du général au spécifique
- Type d'explication souhaité détaillé (intuition + maths + pratique)
- Format de réponse guidé

### 📊 IMPACT
- **Avant** : Définition générique de Wikipedia
- **Après** : Explication pédagogique en 5 niveaux adaptée au niveau Master, avec analogie (pénaliser les coefficients trop grands = limiter l'overfitting), formule mathématique, graphiques comparatifs, code pratique, et recommandations de paramétrage

---

## Exemple 7 : Visualisation sans spécifications

### ❌ AVANT
```
fais moi un graphique pour ces données

ventes par région
```

### ⚠️ PROBLÈMES
- Type de graphique non spécifié
- Structure des données inconnue
- Objectif de la visualisation absent
- Aucun critère esthétique ou contrainte

### ✅ APRÈS
~~~markdown
## Contexte
Présentation executive pour le comité de direction (non-technique)

## Données
DataFrame avec 3 ans de ventes par région :
```python
# Structure
   date       | region      | ventes_k€ | nb_clients
   2022-01-01 | Nord        | 1250      | 340
   2022-01-01 | Sud         | 980       | 275
   ...
```
- 12 régions françaises
- Données mensuelles (36 mois)
- Ventes en milliers d'euros

## Objectif de la visualisation
Montrer l'évolution temporelle des ventes ET comparer les régions
pour identifier :
- Quelles régions surperforment/sous-performent
- Les tendances temporelles (croissance, saisonnalité)
- Les régions à prioriser pour 2025

## Contraintes
- Doit être compréhensible en 30 secondes
- Couleurs corporate : bleu (#1f77b4) et orange (#ff7f0e)
- Style moderne et professionnel
- Une seule visualisation (ou max 2 si complémentaires)

## Question
Quel type de graphique recommandes-tu ?
Génère le code Python (matplotlib ou seaborn) avec :
- Titre et labels clairs
- Légende appropriée
- Annotations des points clés si pertinent
~~~

### 💡 POURQUOI C'EST MIEUX
- Audience clairement définie (executives non-techniques)
- Structure des données explicitée avec exemple
- Objectif de la viz multidimensionnel
- Contraintes esthétiques et fonctionnelles
- Demande de recommandation + code

### 📊 IMPACT
- **Avant** : Graphique en barres basique générique
- **Après** : Recommandation argumentée (ex : small multiples ou heatmap temporelle), code complet avec style professionnel, annotations automatiques des insights clés, et alternative avec visualisation interactive plotly

---

## Exemple 8 : Gestion de données manquantes

### ❌ AVANT
```
comment gérer les valeurs manquantes
```

### ⚠️ PROBLÈMES
- Type de données inconnu (numériques, catégorielles, texte ?)
- Proportion de missing non précisée
- Pattern des manquants inconnu (MCAR, MAR, MNAR ?)
- Objectif final absent

### ✅ APRÈS
```markdown
## Contexte du dataset
Données médicales pour prédire le risque de diabète

## Valeurs manquantes identifiées
Analyse avec `df.isnull().sum()` :
- `glucose` : 15% missing (numérique, crucial pour prédiction)
- `blood_pressure` : 8% missing (numérique, important)
- `bmi` : 5% missing (numérique, modéré)
- `insulin` : 48% missing (numérique, beaucoup !)
- `skin_thickness` : 30% missing (numérique)

## Observations
- Les missing sur `insulin` et `skin_thickness` semblent corrélés
- Certains patients ont TOUTES les valeurs, d'autres plusieurs manquantes
- Pattern : semble MAR (Missing At Random) - liés à l'âge des patients

## Objectif
Classification binaire (diabète oui/non) avec Random Forest

## Contraintes
- Dataset modeste : 768 lignes (pas énorme)
- Besoin de garder un maximum de lignes
- Performances actuelles avec suppression des lignes : accuracy 72%

## Question
Quelle stratégie d'imputation recommandes-tu pour chaque variable ?
Options que je connais : moyenne, médiane, KNN, MICE...

Peux-tu :
1. Recommander une approche par variable
2. Justifier selon les caractéristiques (% missing, importance)
3. Donner le code Python (sklearn/pandas)
4. Expliquer l'impact sur la modélisation
```

### 💡 POURQUOI C'EST MIEUX
- Contexte métier (données médicales)
- Analyse détaillée des missing par variable
- Pattern des missing investigué
- Objectif de modélisation précisé
- Baseline performance donnée
- Demande structurée avec justifications attendues

### 📊 IMPACT
- **Avant** : Réponse générique sur les méthodes d'imputation
- **Après** : Stratégie différenciée par variable (ex : médiane pour BMI, KNN pour glucose, drop pour insulin vu le 48%, feature "insulin_missing" comme indicateur), code complet avec IterativeImputer, analyse de l'impact sur la performance, et warnings sur les biais potentiels

---

## Exemple 9 : Déploiement de modèle

### ❌ AVANT
```
comment déployer mon modèle en production
```

### ⚠️ PROBLÈMES
- Type de modèle inconnu
- Infrastructure cible non précisée
- Contraintes de latence/volume absentes
- Niveau d'expertise en déploiement inconnu

### ✅ APRÈS
```markdown
## Contexte du modèle
Modèle XGBoost de détection de fraude (classification binaire)
- Taille du modèle sérialisé : 150 Mo
- Features : 45 (mixtes : numériques et catégorielles encodées)
- Performance : recall 82%, precision 41%
- Framework : scikit-learn + XGBoost

## Infrastructure disponible
- Cloud : AWS (accès complet)
- Base de données : PostgreSQL (transactions en temps réel)
- Stack backend actuel : Python 3.11, FastAPI
- Monitoring : DataDog disponible

## Contraintes
- **Latence critique** : < 100ms par prédiction
- **Volume** : ~5000 prédictions/heure en pic
- **Disponibilité** : 99.9% SLA requis
- **Coût** : Budget limité (éviter instances trop chères)

## Preprocessing requis
Quelques transformations avant inférence :
- Encodage de 5 variables catégorielles (OneHotEncoder fitted)
- Scaling de features numériques (StandardScaler fitted)
- Feature engineering (3 ratios calculés)

## Mon niveau
Intermédiaire en ML, débutant en MLOps/déploiement

## Questions
1. Quelle architecture recommandes-tu ? (API REST, batch, streaming ?)
2. Comment gérer le preprocessing en production ?
3. Quel service AWS utiliser ? (Lambda, ECS, SageMaker ?)
4. Comment monitorer les prédictions et détecter le drift ?
5. Stratégie de versioning du modèle ?

Fournis une roadmap étape par étape avec exemples de code quand pertinent.
```

### 💡 POURQUOI C'EST MIEUX
- Modèle complètement décrit (type, taille, performance)
- Infrastructure et stack précisés
- Contraintes quantifiées (latence, volume, SLA)
- Étapes de preprocessing listées
- Niveau d'expertise indiqué
- Questions structurées couvrant tous les aspects

### 📊 IMPACT
- **Avant** : Réponse générale sur "il faut une API et Docker"
- **Après** : Architecture complète (FastAPI + Docker + ECS), code de l'API avec preprocessing intégré, stratégie de monitoring avec métriques métier (drift detection), plan de rollback, estimation de coûts AWS, et checklist de mise en production

---

## Exemple 10 : NLP - Classification de textes

### ❌ AVANT
```
comment classifier des textes en python
```

### ⚠️ PROBLÈMES
- Type de textes non précisé (courts/longs, langue, domaine)
- Nombre de classes inconnu
- Volume de données absent
- Niveau de performance attendu non défini

### ✅ APRÈS
~~~markdown
## Contexte métier
Classification automatique de tickets support client pour routage

## Données textuelles
- **Volume** : 50k tickets historiques déjà labellisés
- **Langue** : Français (France)
- **Longueur moyenne** : 50-200 mots (descriptions courtes)
- **Classes** : 5 catégories
  - Technique (35%)
  - Facturation (25%)
  - Livraison (20%)
  - SAV (15%)
  - Autre (5%)
- **Exemples** :
```
  "Bonjour, je n'arrive pas à me connecter à mon compte 
  depuis ce matin, erreur 403"
  → Catégorie : Technique

  "Ma facture du mois dernier comporte des erreurs, 
  le montant ne correspond pas"
  → Catégorie : Facturation
  ```

## Contraintes
- **Déploiement** : API temps réel, latence < 500ms
- **Performances minimales** : accuracy > 85%, recall équilibré entre classes
- **Infrastructure** : Serveur 16 Go RAM, pas de GPU
- **Évolution** : Modèle doit être réentraînable mensuellement

## Mon niveau
Bon en ML classique, débutant en NLP

## Questions
1. **Preprocessing** : Quelles étapes essentielles pour du texte français ?
2. **Approche** : Méthodes classiques (TF-IDF + classifieur) vs deep learning (transformers) ?
3. **Modèle** : Recommandation concrète avec justification
4. **Code** : Pipeline complet du preprocessing à l'entraînement
5. **Gestion du déséquilibre** : Comment gérer la classe "Autre" à 5% ?

Format : Code Python commenté étape par étape, avec explications pédagogiques
~~~

### 💡 POURQUOI C'EST MIEUX
- Cas d'usage métier clair (tickets support)
- Caractéristiques du corpus détaillées (volume, langue, longueur)
- Distribution des classes avec déséquilibre visible
- Exemples concrets de textes
- Contraintes de déploiement et performance quantifiées
- Niveau d'expertise et attentes pédagogiques précisés
- Questions structurées couvrant tout le pipeline

### 📊 IMPACT
- **Avant** : Tutoriel générique de classification de textes
- **Après** : Recommandation argumentée (TF-IDF + Logistic Regression pour commencer, CamemBERT si besoin plus de performance), pipeline complet avec spaCy pour preprocessing français, gestion du déséquilibre avec class_weight, code de validation croisée, baseline de performance, et comparaison coût/bénéfice deep learning vs classique

---

## 🎓 Patterns récurrents observés

### ✅ Ce qui rend un prompt "APRÈS" meilleur

| Aspect | Caractéristique |
|--------|-----------------|
| **Contexte technique** | Versions, environnement, ressources précisées |
| **Données** | Taille, types, exemples fournis |
| **Objectif** | Clair, mesurable, avec critères de succès |
| **Contraintes** | Quantifiées (temps, mémoire, latence) |
| **Tentatives** | Ce qui a déjà été essayé est documenté |
| **Structure** | Markdown avec sections logiques |
| **Spécificité** | Détails concrets vs généralités |
| **Format attendu** | Type de réponse souhaité explicité |

### ❌ Ce qui rend un prompt "AVANT" faible

| Problème | Impact |
|----------|--------|
| Vague | Réponse générique inutilisable |
| Manque contexte | L'IA doit deviner, risque d'erreur |
| Pas de structure | Difficile à parser, info noyée |
| Pas de chiffres | Impossible d'évaluer l'échelle |
| Pas d'objectif clair | Réponse ne répond pas au vrai besoin |
| Langage télégraphique | Perte de nuances importantes |
