# Quiz : IA Générative & Prompt Engineering
## Test rapide de compréhension (10 questions - 10 minutes)

**Instructions :** Choisissez la ou les meilleures réponses. Certaines questions peuvent avoir plusieurs bonnes réponses.

---

## Question 1 : Contexte et performance

Vous demandez à une IA "comment optimiser mon code pandas". Parmi ces informations, laquelle est la PLUS critique à ajouter ?

**A.** La version de Python utilisée  
**B.** La taille du DataFrame (nombre de lignes)  
**C.** Votre nom et celui de votre entreprise  
**D.** Le système d'exploitation

<details>
<summary><b>👉 Voir la réponse</b></summary>

**Réponse : B**

**Explication :** La taille du DataFrame est cruciale car les optimisations diffèrent radicalement selon qu'on a 1000 ou 10 millions de lignes. Les versions (A) sont utiles mais secondaires. L'OS (D) est rarement pertinent pour pandas. Le nom (C) est inutile.

**Points clés :**
- L’ordre de grandeur de la quantité de données conditionne les optimisations possibles
- Le contexte le plus critique est celui qui a un impact direct sur le problème posé (ici vitesse traitement // nombre d’opérations à réaliser = nombre de données à traiter)
</details>

---

## Question 2 : Quand chercher sur le web ?

Dans quels cas devriez-vous faire une recherche sur le web plutôt que de demander à l'IA ?

**A.** "Explique-moi ce qu'est un Random Forest"  
**B.** "Qui a gagné les dernières élections françaises ?"  
**C.** "Quels sont les meilleurs frameworks Python pour le deep learning en 2025 ?"  
**D.** "Comment faire une boucle for en Python ?"

<details>
<summary><b>👉 Voir la réponse</b></summary>

**Réponses : B et C**

**Explication :**

- **(B)** Événement récent avec une réponse factuelle qui peut avoir changé → RECHERCHE 
- **(C)** "En 2025" + "meilleurs" indique besoin d'info à jour → RECHERCHE
- **(A)** Concept fondamental stable → PAS de recherche nécessaire
- **(D)** Syntaxe de base stable → PAS de recherche nécessaire

**Principe d'or :** Faites une recherche web pour les info qui changent fréquemment (quotidien/mensuel) ou les événements datés récents. L’IA est utile (et fiable) pour poser des questions sur des concepts stables.
</details>

---

## Question 3 : Structure de prompt

Quel prompt est le MIEUX structuré pour obtenir une aide efficace ?

**A.**
```
mon code plante aide
```

**B.**
```
Python pandas merge KeyError customer_id help debug fast
```

**C.**
```markdown
## Problème
Erreur lors du merge de DataFrames

## Erreur
KeyError: 'customer_id'

## Code
[code complet]

## Structure données
df1 colonnes : [liste]
df2 colonnes : [liste]
```

**D.**
```json
{
  "error": "KeyError",
  "language": "Python",
  "help": "please fix"
}
```

<details>
<summary><b>👉 Voir la réponse</b></summary>

**Réponse : C**

**Explication :**
- **(C)** Structure claire avec markdown, erreur complète, code, et contexte → EXCELLENT
- **(A)** Trop vague, aucun contexte → MAUVAIS
- **(B)** Style "mots-clés Google", pas de structure → INSUFFISANT
- **(D)** JSON difficile à écrire manuellement, info incomplète → PAS PRATIQUE

**Leçon :** Markdown structuré avec sections claires = format optimal pour 90% des cas.
</details>

---

## Question 4 : Debugging efficace

Votre code pandas génère une erreur. Que devez-vous ABSOLUMENT inclure dans votre prompt ?

**A.** Le message d'erreur complet avec le traceback  
**B.** Le code qui génère l'erreur  
**C.** La structure de vos données (types, exemples)  
**D.** Toutes les réponses ci-dessus

<details>
<summary><b>👉 Voir la réponse</b></summary>

**Réponse : D (Toutes)**

**Explication :** Pour un debugging efficace, vous devez fournir :
1. **Le message d'erreur complet** (A) - indique précisément le problème
2. **Le code** (B) - permet de comprendre le contexte
3. **La structure des données** (C) - souvent la cause du problème (types incompatibles, colonnes manquantes, etc.)

**Sans l'un de ces éléments, l'IA devra deviner, ce qui réduit drastiquement la qualité de l'aide.**

**Template de debugging :**
```markdown
Erreur : [message complet]
Code : [snippet]
Données : [df.dtypes, exemples]
```
</details>

---

## Question 5 : Itération de prompts

Votre première question donne une réponse trop générique. Que faire ?

**A.** Abandonner et chercher sur Stack Overflow  
**B.** Redemander exactement la même chose  
**C.** Ajouter plus de contexte et préciser votre besoin  
**D.** Changer d'IA complètement

<details>
<summary><b>👉 Voir la réponse</b></summary>

**Réponse : C**

**Explication :** 
- L'itération est NORMALE et ATTENDUE en prompt engineering
- Si la réponse est trop générique, c'est que le contexte était insuffisant
- Ajoutez progressivement : détails sur vos données, contraintes, ce que vous avez déjà essayé

**Exemple d'itération :**
```
Prompt 1 : "Comment gérer les données manquantes ?"
→ Réponse générique

Prompt 2 : "J'ai 30% de missing sur la colonne 'glucose' 
dans un dataset médical de 800 lignes. Quelle imputation 
recommandes-tu pour un modèle de classification ?"
→ Réponse ciblée
```

**Ne cherchez pas le prompt parfait du premier coup !**
</details>

---

## Question 6 : Format de prompt

Pour une demande de code complexe, quel format est le PLUS efficace ?

**A.** Langage naturel non structuré (un long paragraphe)  
**B.** Markdown avec sections (Contexte, Objectif, Question)  
**C.** Format JSON strict  
**D.** Liste de mots-clés séparés par des espaces

<details>
<summary><b>👉 Voir la réponse</b></summary>

**Réponse : B**

**Explication :**
- **(B) Markdown structuré** = sweet spot parfait :
  - Rapide à écrire
  - Facile à lire
  - Structure claire pour l'IA
  - Flexible

- **(A)** Un paragraphe = difficile à parser, info noyée
- **(C)** JSON = trop rigide, pénible à écrire manuellement
- **(D)** Mots-clés = perte de nuances et de contexte

**Règle pratique :** 

- Question simple → langage naturel direct
- Question complexe → markdown avec sections
</details>

---

## Question 7 : Contexte des données

Vous voulez de l'aide sur un problème de performance. Parmi ces infos, lesquelles sont ESSENTIELLES ?

**A.** "Mon code est lent"  
**B.** "Mon DataFrame a 5 millions de lignes"  
**C.** "Mon code prend actuellement 45 minutes"  
**D.** B et C

<details>
<summary><b>👉 Voir la réponse</b></summary>

**Réponse : D (B et C)**

**Explication :**
- **(A)** "Lent" est subjectif et vague → INSUFFISANT
- **(B)** L'échelle des données est ESSENTIELLE → CRITIQUE
- **(C)** Le temps actuel quantifie le problème → CRITIQUE

**Pourquoi B et C ensemble ?**
- Sans (B), impossible de savoir si 45 min est normal ou excessif
- Sans (C), impossible de définir un objectif d'optimisation
- Ensemble, ils permettent d'évaluer l'ampleur du problème

**Toujours quantifier :**
- ❌ "Lent" → ✅ "45 minutes pour 5M lignes"
- ❌ "Beaucoup de données" → ✅ "2 Go, 3M lignes, 50 colonnes"
</details>

---

## Question 8 : Choix de modèle

Pour demander une recommandation de modèle, qu'est-ce qui est MOINS important ?

**A.** Le type de problème (classification, régression, etc.)  
**B.** La couleur préférée du data scientist  
**C.** La taille du dataset  
**D.** Les contraintes (interprétabilité, temps réel, etc.)

<details>
<summary><b>👉 Voir la réponse</b></summary>

**Réponse : B (évidemment !)**

**Explication :** Question piège facile pour vérifier votre attention 😊

**Les vrais critères essentiels :**
- **(A)** Type de problème = dicte la famille de modèles
- **(C)** Taille dataset = influence le choix (deep learning vs classique)
- **(D)** Contraintes = éliminent certaines options

**Contexte complet pour recommandation de modèle :**
```markdown
- Type : Classification binaire
- Données : 50k lignes, 30 features mixtes, déséquilibre 85:15
- Objectif : Recall > 75%
- Contraintes : Modèle explicable, latence < 200ms
```
</details>

---

## Question 9 : Gestion du copyright

Vous comptez dans vos sources un article récent sur un sujet data science. Que pouvez-vous demander à l'IA ?

**A.** "Copie-moi les 5 premiers paragraphes de cet article"  
**B.** "Résume les points clés de cet article en quelques phrases"  
**C.** "Cite-moi exactement ce que dit l'article sur la régularisation"  
**D.** "Explique-moi les concepts mentionnés dans cet article"

<details>
<summary><b>👉 Voir la réponse</b></summary>

**Réponses : B et D**

**Explication :**
- ✅ **(B)** Résumé en vos propres mots = OK
- ✅ **(D)** Explication de concepts = OK
- ❌ **(A)** Copie de paragraphes = VIOLATION COPYRIGHT
- ❌ **(C)** Citation exacte = VIOLATION COPYRIGHT

**Règle d'or : L'IA peut PARAPHRASER et EXPLIQUER, mais JAMAIS copier exactement du contenu protégé.**

**Bon usage :**
"Après avoir lu cet article sur XGBoost, peux-tu m'expliquer plus simplement le concept de gradient boosting mentionné ?"
</details>

---

## Question 10 : Validation des réponses

L'IA vous donne un code d'optimisation. Que devez-vous faire AVANT de l'utiliser ?

**A.** Le copier-coller directement en production  
**B.** Le lire et le comprendre  
**C.** Le tester sur un échantillon de données  
**D.** B et C

<details>
<summary><b>👉 Voir la réponse</b></summary>

**Réponse : D (B et C)**

**Explication :**

**Étapes obligatoires :**
1. ✅ **(B) Lire et comprendre** - Jamais de copier-coller aveugle
2. ✅ **(C) Tester** - Vérifier que ça fonctionne sur vos données
3. ✅ Valider les résultats (précision, performance, etc.)
4. ✅ Comparer avec votre code original

**❌ (A) est DANGEREUX** - L'IA peut faire des erreurs ou proposer du code inadapté à votre contexte spécifique.

**Principe fondamental :**
> **L'IA est un assistant, pas un substitut à la réflexion.**
> Vous restez responsable du code que vous utilisez.

**Workflow recommandé :**
```
IA génère code → Vous lisez → Vous comprenez 
→ Vous testez → Vous validez → Vous adaptez si besoin
```
</details>

---

## 🎯 Scoring

**9-10 bonnes réponses** : Expert en prompt engineering ! 🏆  
Vous maîtrisez les principes et êtes prêt à utiliser l'IA efficacement.

**7-8 bonnes réponses** : Très bien ! 🌟  
Vous avez compris l'essentiel, quelques points à affiner.

**5-6 bonnes réponses** : Bon début 👍  
Relisez les concepts de contexte et structuration des prompts.

**< 5 bonnes réponses** : À retravailler 📚  
Revoyez la cheat sheet et les exemples avant/après.

---

## 📝 Points clés à retenir

### Les 5 commandements du bon prompt

1. **Contextualiser** - Donnez l'environnement technique et les caractéristiques des données
2. **Quantifier** - Chiffres concrets plutôt que "lent", "gros", "beaucoup"
3. **Structurer** - Markdown avec sections claires pour les demandes complexes
4. **Itèrer** - Améliore ton prompt si la réponse est trop générique
5. **Valider** - Comprends et teste toujours le code généré

### Les 3 erreurs à éviter

1. ❌ Prompts trop vagues sans contexte
2. ❌ Copier-coller sans comprendre
3. ❌ Abandonner après une première réponse insatisfaisante

### Le principe fondamental

> **"Donnez à l'IA le contexte que vous donneriez à un collègue humain qui vous aiderait."**

