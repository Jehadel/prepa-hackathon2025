# Hackathon 2025 - Ynov Campus Aix

## Généralités

La production de code est aujourd’hui massivement impactée par l’IA générative.

Le consensus général est de recommander aux **juniors** de **ne pas se reposer** trop tôt sur ces outils pour ne pas freiner leur apprentissage. Néanmoins on ne peut pas ignorer les usages, ce document contient donc quelques recommandations dans une démarche de « réduction des risques ».

En premier lieu, il faut penser ces outils en terme d’impacts :

- De manière générale, il convient de bien mesurer les impacts de ces outils de manière globale:
  - considération éthiques et systémiques
  - impacts au niveau individuels (dispositionnels, cognitifs, …)

- Au niveau d’un projet, l’usage doit être réfléchi en fonction des impacts sur :
  - La qualité du code collectif (p. ex. patchwork de bouts de code hétérogènes)
  - La compréhension partagée du projet (p. ex. sous traiter toutes les tâches à l’IA fait que personne ne construit une vision commune)
  - Les implications en matière de maintenance (plus vrai sur les projets à long terme)

### Considérations éthiques : s’interroger

Derrière leur efficacité et leur apparente facilité d’utilisation, les outils IA ont tendance à invisibiliser de nombreuses considérations. Ils sont pourtant loin d’être neutres et de manière générale on doit toujours s’interroger selon différentes dimensions ?

1. **Conception** :
   - Qui a conçu cet outil ? Avec quelles données ? Quelle intention ? Comment ?
2. **Usage** :
   - Quel est le rôle de l’humain ? Quelles décisions l’outil prend-il ? Qui le contrôle ?
3. **Systémique** :
   - Quelle dépendance crée-t-il ? Quel impact environnemental, social ? Quelles alternatives sont possibles ?
4. **Individuel** :
   - Quel impact sur ma pratique ? Provoque-t-il une « fainéantise cognitive » ? Est-ce que je conserve mon esprit critique ?

Par exemple réfléchir sur :

- créer un agent conversationnel (chatbot)  ? 
- utiliser l’IA pour générer des images ?

### Panorama : quand utiliser l’IA en data science?

Hors code, l’IA est pratique pour :

* Exploration et compréhension :
  * Rappel de points de cours : « Quelle est la différence entre une régression linéaire et une régression logistique ? »
  * Trouver de l’inspiration dans les recherches de solutions : « Quelles seraient les méthodes pour générer des données manquantes dans une série temporelle ? »
  * Comparer des approches
* Éclairer des points de la connaissance métier
  + P.ex. « Comment ces molécules impactent-elle le goût du vin ? »
  + **Attention aux hallucinations** : l’IA sert à *défricher*, toujours recouper avec des recherches sur d’autres sources que l’IA (articles, ouvrages…)
* Plus largement : très bien pour tout ce qui est manipulation de texte : résumer, reformuler, réagencer… mettre à profit ces capacités pour la doc, compte rendu de réunion, etc. *avec parcimonie* eu égard aux considérations éthiques précédentes.

Plus particulièrement concernant le code :

- Génération de code dit « boilerplate »
  - Chargement et nettoyage de données
  - Visualisations standards
  - Pipelines de preprocessing
- Optimisation
  - Proposer des optimisations de performance
  - Refactoring (relisez bien le code proposé avant de valider une refactorisation)
- Debugging
  - Idéalement, l’IA peut devenir votre « canard en plastique » (comprendre le problème en lui expliquant, sans avoir besoin de sa réponse)
  - Attention : l’IA peut vous permettre de gagner du temps en la matière, mais vous ne progresserez qu’en debuggant vous même ! Il vaut mieux utiliser l’IA pour vous aider à comprendre l’origine d’une erreur que vous aurez corrigé vous-même. Par ailleurs attention car selon la situation, risque de s’enfoncer dans une boucle infinie de recherche (contexte).
- Une utilisation à laquelle vous serez moins confrontés est aussi la compréhension de l’architecture d’un projet ou de code d’un projet que vous rejoignez. Certains outils permettent aussi de comprendre l’historique (commit).

### Limites

* C’est à vous de valider la pertinence des solutions *suggérées* par l’IA, n’achetez pas comptant sans évaluation et recul critique !
* L’IA doit vous aider à comprendre, pas comprendre à votre place ! (ce qui n’arrivera pas)
* Même si les capacités des modèles sur ce point s’améliorent, l’IA est nulle en calcul (en fait elle ne calcule pas), donc vérifiez toujours les formules utilisées (hallucinations) et les calculs s’il y en a (erreurs)
* **Confidentialité des données** : ne jamais partager de données sensibles ou propriétaires (méfiance même si vous anonymisez des données, utilisez plutôt des dumb data)

### Exemples

Voici quelques exemple de prompts qui permettent de répondre efficacement à quelques une des situations évoquées ci-dessus. Nous verrons plus bas comment structurer les prompts de manière encore plus précise.

#### 1. Explication de concepts

```
Explique-moi la régularisation L1 vs L2 en régression :
1. La différence mathématique
2. L'impact sur les coefficients
3. Quand utiliser l'une ou l'autre
4. Un exemple de code avec scikit-learn

Réponds de manière concise, adapté à un niveau Master.
```

#### 2. Exploration rapide d'un dataset

Dans les données que vous avez récupérées pour un projet, vous avez un CSV sur les ventes d'une entreprise et devez rapidement comprendre sa structure.

```
J'ai un dataset de ventes avec ces colonnes : 
date, product_id, category, quantity, price, region, customer_id

Peux-tu me générer du code Python pour :
1. Charger les données et afficher les infos de base
2. Vérifier les valeurs manquantes
3. Calculer des statistiques descriptives par catégorie
4. Créer 3 visualisations pertinentes pour comprendre les données

Utilise pandas, matplotlib et seaborn
```

**Attention !**  Le code qui sera généré sera un bon point de départ, mais il faut le relire et l’adapter (à votre projet, à votre existant, etc.). Par exemple :

* les visualisations peuvent ne pas être adaptées du tout à votre problématiques plus globale (projet), car vous n’avez donné aucune directive (c’est purement exploratoire)
* c’est à vous de réfléchir ensuite et d’ajouter des analyses en fonction de ce que **vous** aurez tiré de cette première exploration

#### 3. Optimisation

Vous avez fait une boucle `for` (bouh !) et fort logiquement elle met 10 mn pour traiter 100 000 lignes.

```
Ce code est très lent sur un DataFrame de 100k lignes. 
Comment l'optimiser avec pandas ?

def calculate_discount(row):
    if row['quantity'] > 100:
        return row['price'] * 0.2
    elif row['quantity'] > 50:
        return row['price'] * 0.1
    else:
        return 0

df['discount'] = df.apply(calculate_discount, axis=1)
```

* cet exemple est purement théorique : vous savez bien sûr déjà que la boucle `for` c’est le mal, et qu’il vaut mieux vectoriser
* vérifiez tout de même toujours les gains annoncés avec une balise `%%timeit`

#### 4. Debugging

Votre merge de DataFrames plante, et vous ne comprenez rien au message d’erreur.

```
J'ai cette erreur en Python avec pandas :

KeyError: "None of [Index(['customer_id'], dtype='object')] are in the [columns]"

Mon code :
df1 = pd.read_csv('sales.csv')
df2 = pd.read_csv('customers.csv')
result = pd.merge(df1, df2, on='customer_id')

Les colonnes de df1 sont : ['date', 'product', 'customerid', 'amount']
Les colonnes de df2 sont : ['customer_id', 'name', 'region']

Pourquoi cette erreur et comment la corriger ?
```

## How  to / Bonnes pratiques

### La base

#### Ce qu’il faut faire :

- Décomposer les problèmes complexes en sous-questions
- Fournir du contexte (librairies utilisées, versions, erreurs complètes)
- Demander plusieurs alternatives et les comparer
- Utiliser l'IA pour la documentation et les commentaires

#### Ce qu’il ne faut pas faire :

- Copier-coller sans comprendre
- Utiliser l'IA pour des décisions méthodologiques critiques sans validation
- Négliger les aspects éthiques et de confidentialité des données
- Se reposer uniquement sur l'IA pour l'apprentissage

### Structurer le prompt

Trop souvent j’ai vu des étudiant-e-s rédiger des prompts au fil de l’eau, sur un mode conversationnel, n’ajoutant certains éléments de contexte pourtant capitaux qu’après coup, ce qui change totalement la perspective et la réponse de l’IA.

Vous ne **pouvez pas** écrire des prompts tels que ceux-ci :

+ « Fais moi une analyse de donnée à partir des ces fichiers »
+ « Ce code ne marche pas »
+ « Quel modèle utiliser avec ces données ? »

Pour être efficace, vous devez bien penser et donc structurer votre prompt. Un prompt bien structuré correspond à ce modèle :

```
[Contexte] + [Tâche précise] + [Contraintes/Format] + [Outils souhaités]
```

**Exemple :**

> J'ai un dataset de 50k lignes avec des données de transactions. Génère du code Python pour détecter les valeurs aberrantes dans les colonnes numériques en utilisant la méthode IQR. Utilise pandas et crée une visualisation avec matplotlib. 

On commence **toujours** par donner le contexte. Pourquoi le contexte est-il si important ?

#### Fonctionnement des IA génératives

##### Importance du contexte

Les modèles de langage comme Claude ou ChatGPT fonctionnent sur un principe fondamental : prédire le texte le plus pertinent en fonction du contexte fourni. Pour schématiser très grossièrement, elle prédisent « juste »  la suite de mots la plus probable en « réponse » (output) au texte que vous lui donnez en input (prompt). Si vous mettez en input un texte très vague, en matière de probabilité il y a plein d’output possibles qui pourront être délivrés, soit génériques, soit inappropriées. Si au contraire vous mettez en input un texte très précis, vous limitez les « degrés de liberté » et donc vous obtiendrez en output une réponse également précise qui colle d’autant à votre question. 

Analogie : Imaginez que vous demandez à un collègue de vous aider sur un bug, mais que vous lui dites juste "mon code ne marche pas". Il va devoir vous poser 10 questions avant de pouvoir aider :
    • Quel langage ?
    • Quelle erreur ?
    • Quel est l'objectif du code ?
    • Quelles bibliothèques utilisez-vous ?
    • Etc.
Avec une IA, c'est pareil, sauf que l'IA ne peut pas vous poser de questions (ou difficilement), elle va donc faire une réponse probable, qui risque de ne pas être adaptée car il n‘y aura pas le contexte nécessaire pour la guider.

Pour résumer :

```
Contexte vague → Réponse générique
Contexte précis → Réponse ciblée et utile
```

 ##### La "context window" : la mémoire de travail de l'IA

En psychologie cognitive, la mémoire de travail (*working memory*) est un concept extrêmement important. Il s’agit « d’un système, de capacité limitée, qui assure une double fonction de traitement et de stockage temporaire de l’information ». [Lien article Widipédia]

De manière analogue, les IA ont une **fenêtre de contexte** limitée (bien que très grande maintenant) :

- P. ex. Claude Sonnet 4.5 : environ 200 000 tokens (~150 000 mots)
- Cette fenêtre contient TOUT : vos messages précédents, le message actuel, les réponses de l'IA

**Implications pratiques :**

- L'IA "se souvient" de toute la conversation en cours
- Mais elle n'a aucune mémoire entre deux conversations différentes
- Plus vous donnez de contexte pertinent, mieux elle peut vous aider
- Plus la conversation avance, plus l’IA a de contexte et donc plus ses réponses seront « précises » (en regard de ce contexte)

```
Comment charger un .csv en Python ?
```

réponse générique la plus probable -> `pd.read_csv()` si vous avez de la chance (ou une autre bibliothèque…)

```
Je dois charger un CSV de 5 Go avec 50 colonnes dont 30 sont inutiles.
Le CSV utilise le séparateur ';' et l'encoding 'latin-1'.
Je n'ai que 8 Go de RAM disponible.
Comment charger efficacement ce fichier en Python avec pandas ?
```

réponse précise plus probable -> vous parlera de sélection de colonne (`usecols`), de `chunck`, de `dtypes`, etc.

#### Préciser un contexte

Le contexte peut concerner différentes dimensions :

1. Contexte « technique » :
   + langages et leurs versions de ceux-ci (Python 3.11, R 4.3)
   + bibliothèques et leurs versions
   + Environnement d’exécution (Jupyter, script, cloud)
   + Système d'exploitation
2. Contexte « data » :
   - Taille du dataset (lignes × colonnes)
   - Types de colonnes (numériques, catégorielles, dates, texte)
   - Échelle (Ko, Mo, Go)
   - Problèmes connus (valeurs manquantes, outliers, déséquilibre)
   - Structure (flat, hiérarchique, time-series)
3. Contexte « métier » :
   - Problème à résoudre (classification, régression, clustering, etc.)
   - Métrique d'évaluation prioritaire
   - Contraintes métier (interprétabilité, temps réel, coût d'erreur)
   - Cas d'usage final
4. Contexte « problème » :
   - Message d'erreur **complet ** (avec traceback)
   - Idéalement code minimal qui reproduit l'erreur
   - Ce que vous attendiez vs ce qui se passe
   - Ce que vous avez déjà essayé
5. Contexte « contraintes » :
   - Contraintes de ressources (RAM, CPU, temps d'exécution)
   - Contraintes de déploiement (production, batch, temps réel)
   - Contraintes organisationnelles (bibliothèques autorisées, sécurité)
6. Contexte « expertise » :
   - Votre niveau sur le sujet (étudiant de master, junior, etc.)
   - Niveau de détail souhaité (expllications nécessaires, ajout de commentaires dans le code)
   - Type d'explication attendue (on peut aussi demander d’éviter les concepts trop obscurs )
7. Contexte « historique » :
   - vous pouvez très bien référencer des questions/réponses précédentes dans la conversation
   - ajouter des éléments de contextes pour préciser encore plus (approche itérative : on démarre sur un problème plus large et on précise pour guider l’IA)
   - ne pas hésiter à corriger le contexte si on perçoit une déviation ou une mauvaise spécification

#### Itérer sur votre promtp

Personne n’attend que vous écriviez le prompt parfait du premier coup (l’IA est bien plus patiente que beaucoup de vos collègues). Au contraire, cela peut l’aider (et vous aider) à construire un contexte très précis et adapté :

1. **Premier prompt** : Question large avec contexte minimal
2. **Analyse de la réponse** : Est-elle trop générique ? Manque-t-elle des éléments ?
3. **Deuxième prompt** : Précisez le contexte manquant
4. **Affinage** : Continuez jusqu'à obtenir ce dont vous avez besoin

Par contre, une fois que vous avez un contexte bien défini pour votre projet, n’hésitez pas à le sauvegarder quelque part : ça vous vous permettra de relancer une nouvelle conversation sur un autre problème rencontrer dans votre projet en pouvant le spécifier dès le début.

Une bonne méthode pour gagner du temps et écrire un bon prompt est de se demander comment on exposerait notre prompt à un collègue (ou mieux : comment on écrirait un e-mail à un collègue distant pour décrire le problème). C’est un peu la technique du « canard en plastique » déjà évoquée plus haut.

Ne pas hésiter à donner des exemples précis si on a du mal à décrire des choses de manière abstraite (ce n’est pas toujours facile) :

```
Je dois nettoyer des données textuelles qui concernent des produits en vente avec des promotions et des informations de livraison
```

versus :

```
J'ai des descriptions produits à nettoyer, exemples :
    • "NOUVEAU!! Chaise de bureau -50% promo "
    • "table basse moderne (livraison GRATUITE) "
    • "Canapé d'angle ❤️ 3 places ###PROMO### "
Objectif : Retirer emojis, promotions, normaliser les espaces
```

#### Formater la présentation du contexte

Vous pouvez vous créer des templates de prompts bien structurés. Perdez l’habitude de rédiger « comme on parle », mais donnez un plan à votre prompt, ça vous aidera aussi à clarifier vos idées, votre démarche (et c’est pratique pour la doc, les compte-rendus, le readme…)

```
[CONTEXTE]
- Environnement : [tech stack]
- Données : [caractéristiques]
- Objectif : [but final]
- Contraintes : [limitations]

[DEMANDE]
[Question ou tâche précise]

[FORMAT SOUHAITÉ]
[Code/Explication/Les deux]
```

Bien sûr vous devez adapter cette présentation au type de problème que vous rencontrez : pour les debugs par exemple, intégrez une section [CODE QUI POSE PROBLÈME] et une section [BUG] (avec une description du problème, le traceback, etc.) et [DÉJÀ ESSAYÉ], etc.

C’est une excellente pratique qui vous aide vous aussi à bien penser et clarifier votre démarche, un peu comme certains développeurs (dont votre serviteur) préparent l’écriture de leur code en écrivant les commentaires ou les fichiers readme en amont.

Note : évitez le « surformatage » : inutile de se perdre dans des détails de mise en forme / mise en page, le formatage sert seulement à découper votre texte de manière logique, afin de faciliter le traitement par l’IA

#### Créer une « context presentation/doc »

Comme dit précédemment, une fois que vous avez un contexte parfaitement adapté à votre projet créer un document que vous pourrez copier/coller au début de toute nouvelle conversation liée au projet. C’est particulièrement utile pour des projets longs.

```
# Contexte Projet [Nom]

## Stack technique
- Langage et bibliothèques :
- Environnement : (vous pouvez aussi donner des infos sur déploiement)

## Données
- Source : (base, api, fichiers, etc.)
- Volume : 
- Features : 
- Cible : 

## Objectifs
- (Prédire, visualiser, …) 
- KPI/Métrique (Précision…) : 
- Modèle (feature, explicable…)

## Contraintes
- RAM serveur :
- Temps batch : (temps max voulu)
- Latence inférence :
- Réglementaire : (RGPD, etc.)

## Déjà implémenté
- (on peut donner réf. vers fichiers, performance obtenue, modèles utilisés, etc.)
```

Créez-vous également une cheatsheet de templates liés à différents problème : un template pour le debugging, un template pour gérer du boilerplate (exploration données, etc.)

#### IA et IDE

Pour des projets, on évite d’utiliser des Chatbot. Il y a différentes solutions IA : Copilot, Claude Code, Windsurf, Cursor, Zed… (de nouvelles tous les jours)

L’immense avantage et que ces IA disposent directement du contexte du projet.

De plus cela vous offre des options de formatage supplémentaires : vous pouvez utiliser les commentaires et docstrings pour guider l’IA :

```
# CONTEXTE: Dataset de 100k lignes, feature engineering
# OBJECTIF: Créer une feature "days_since_last_purchase"
# DONNÉES: df avec colonnes 'customer_id', 'purchase_date'

def create_recency_feature(df):
    """
    Calcule le nombre de jours depuis le dernier achat pour chaque client.
    
    Args:
        df: DataFrame avec 'customer_id' et 'purchase_date'
    
    Returns:
        DataFrame avec nouvelle colonne 'days_since_last_purchase'
    """
    # compléter ici
```

Dans ce cas une bonne pratique qui aide beaucoup l’IA est de donner des noms très explicites aux fonctions et aux variables.

On commence à s’éloigner du scope de cette présentation qui consiste à donner les bonnes pratiques de base dans l’usage de l’IA.

#### Pratiques non-recommandées

##### Donner (trop) de contexte non pertinent

```
Je travaille pour une entreprise de 500 personnes créée en 1995, nous avons 3 bureaux en France, mon manager s'appelle Trucmuche... [300 mots de contexte business] ...comment charger un CSV avec pandas ?
```

##### Référer à du contexte implicite

```
Je travaille sur un data set de 500k lignes et 25 colonnes dont une colonne date, mais l’extraction ne donne pas le format attendu
```

Vous n’indiquez pas :

* le format de date (originel / attendu)
* quelle est l’erreur (l’écart entre ce que vous obtenez et ce que vous souhaitez obtenir)
* comment vous réalisez l’extraction, et quel est le problème posé

##### Contexte « dispersé »

```
Message 1 : comment extraire des données de ces fichiers… 
[…]
Message 4 : je dois faire une régression logistique…
[…]
Message 7 :je travaille avec R et pas avec Python…
[…]
Message 12 : les colonnes 5 à 12 ne sont pas nettoyées…
```

Vous indiquez le contexte, mais dans plusieurs messages séparés, et sans logique (sans aller du général au particulier par exemple)

##### Contexte « évolutif »

```
Message 1 : Convertir les dates d’un dataframe de 1000 lignes…
[…]
Message 10 : Peux-tu optimiser le code qui est soudainement devenu lent ?
```

Mais en fait entre le message 1 et le message 10 vous avez changé de dataset (1000 lignes -> 100k lignes) sans en informer votre agent.

#### À retenir :

* Au minimum (pour des questions génériques, rapides < 50 mots ) indiquer :
  * le langage, les librairies et les versions utilisées
  * un objectif général / problème
  * demander un code / analyser une erreur… etc. 
* Si on est sérieux, pour un problème plus précis (questions entre 50 et 200 mots), on structure le contexte :
  * on liste l’environnement technique complet (stack)
  * on caractérise les données (structure, format, taille…)
  * on indique des contraintes (des choses à faire / à ne pas faire)
  * on décrit un objectif / problème précis à atteindre / résoudre
* Si on veut optimiser l’assistance sur un projet complet (on ne parle plus de question ici), en plus du contexte structuré, on rajoute :
  * des exemples concrets de données
  * les contraintes métiers, le détail des techniques que l’on veut utiliser
  * ce qu’on a déjà essayé et le résultat obtenu (et en quoi il convient / il doit être amélioré)
* Si on utilise l’IA dans un IDE : 
  * mettre le maximum de contexte dans le projet (readme, etc.)
  * donner des noms de fonctions, variables, très explicite
  * utiliser les commentaires et les docstrings détaillées pour guider l’IA 

### Structurer le prompt (2): formatage

Nous venons de voir que nous pouvons structurer nos prompt, y compris en utilisant des techniques de formatages telles que le Markdown, et pourquoi pas du JSON, etc. ?

**Les IA modernes comprennent le langage naturel.** Ce qui compte avant tout, c'est :

1. **La clarté** du contenu
2. **L'organisation logique** des informations
3. **La complétude** du contexte

La mise en forme (markdown, JSON, etc.) est donc un **outil au service de la clarté** (mais pas une fin en soi).

Vous pouvez donc rédiger vos prompts avec :

#### Du langage naturel stucturé (recommandé)

- Le plus naturel à écrire
- Facile à lire et maintenir
- Flexible
- Fonctionne très bien avec tous les modèles

**Quand l'utiliser :** Par défaut, pour 90% des cas. Plutôt pour des questions courtes et simples.

Vous trouverez beaucoup d’exemple dans cette page

#### Du Markdown (recommandé ++)

En fait les IA ont été entraînée sur pas mal de texte avec un formatage en markdown. Elles sont donc très familière de ce format ! 

- Excellente lisibilité
- Structure visuelle claire
- Les IA sont entraînées sur beaucoup de markdown
- Sépare visuellement les sections

**Quand l'utiliser :** 

- Prompts complexes avec plusieurs sections
- Documentation de contexte
- Demandes multi-étapes

Pour des demandes moyennement complexes, on peut utiliser du markdown « allégé » (juste des titres `#` et `##` ) et du markdown plus structuré (titres/sections avec plusieurs niveaux, listes…) pour des demandes plus complexes, qu’on sera amené à réutiliser (contexte plus complet)

En particulier vous pouvez utiliser :

- les titres (headers markdown : `#`, `##`, … ) pour séparer les sections

- vous pouvez utiliser aussi des séparateurs : `---`

  L’IA identifiera ces marqueurs comme des séparateurs logiques

- listes à puces

- listes numérotés

  La structure est facile à saisir, facile à parser, et à séparer sémantiquement

- les blocs de code (avec ``` ou « triple backtips »)

  L’IA identifiera bien où commence et fini le code, pour séparer le texte, les question avec le code, et c’est plus clair pour nous

- Définir des labels (MOTCLEF : [description])

  Les mots clefs sont facile à identifier et agiront comme des marqueurs forts

* On peut aussi introduire des exemples (« exemples : » + liste d’exemples)

#### Pratiques non-recommandées :

* **JSON** 
  On peut très bien rédiger des requêtes en JSON, qui, bien qu’il soit fortement structuré, est peu lisible pour un utilisateur humain. C’est un format qui sera plutôt utilisé lorsque l’on génère des prompts automatiquement pour des API qui utilisent ce format. C’est un cas d’usage qui ne nous concerne donc pas ici.	
* **Une suite de mots clefs**
  Oui, j’ai vu des gens faire ça. C’est à l’encontre de toutes les pratiques que nous vous avons vu précédemment : difficulté à saisir le contexte, manque de précision dans les demandes/objectifs, etc.

#### Checklist : "Mon prompt est-il bien formaté ?"

```markdown
☐ Le contexte est séparé visuellement de la question
☐ Les sections sont identifiables (headers ou labels)
☐ Le code est dans des blocs délimités avec ```
☐ Les listes sont utilisées pour énumérer (pas de pavés)
☐ La hiérarchie de l'information est claire
☐ Je n'ai pas sur-formaté (pas de tableaux ASCII, etc.)
☐ Le prompt est scannable en 5 secondes
☐ Quelqu'un d'autre pourrait comprendre en lisant rapidement
```