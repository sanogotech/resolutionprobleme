# Resolution probleme avec Méthodologie combinée : Brainstorming, Diagramme d’Ishikawa, Pareto, 5 Pourquoi


# 🎯 **Méthodologie combinée pour l’analyse des dysfonctionnements : Brainstorming – Ishikawa – Pareto – 5 Pourquoi**

---

## 🔰 Introduction : Pourquoi combiner ces 4 méthodes ?

Dans des systèmes critiques (e-commerce comme **JUMIA**, applications médicales, plateformes d’énergie, etc.), un dysfonctionnement peut avoir des conséquences majeures : pertes financières, atteinte à la réputation, mise en danger de vies humaines, etc.

Les causes sont souvent **multiples et interconnectées** :

* Techniques (bug, obsolescence, surcharge),
* Humaines (erreur, formation insuffisante),
* Organisationnelles (mauvais processus, communication déficiente),
* Environnementales (cyberattaque, coupure électrique, etc.)

👉 **Aucune méthode seule** ne permet de les cerner **complètement**.

### ✅ **Combinaison méthodologique = efficacité accrue** :

| Méthode                  | Rôle principal                                 | Force                                 | Métaphore         |
| ------------------------ | ---------------------------------------------- | ------------------------------------- | ----------------- |
| **Brainstorming**        | Explorer toutes les idées possibles            | Générateur large d’hypothèses         | Filet de pêche    |
| **Diagramme d’Ishikawa** | Organiser les idées en catégories de causes    | Vision systémique                     | Carte mentale     |
| **Pareto**               | Prioriser les causes les plus fréquentes       | Concentration sur l’essentiel (80/20) | Loupe stratégique |
| **5 Pourquoi**           | Analyser en profondeur les causes prioritaires | Trouver la cause racine               | Pelure d’oignon   |

---

## 🧭 **Enchaînement optimal : La démarche en 4 étapes**

| Étape              | Objectif                                     | Outil                       | Bonnes pratiques                                                                                                                       | Sortie attendue               |
| ------------------ | -------------------------------------------- | --------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------- |
| 1. **Explorer**    | Identifier un maximum de causes potentielles | 🎯 Brainstorming            | - Équipe multidisciplinaire<br>- Pas de jugement d’idées<br>- Durée courte (15–30 min)                                                 | Liste exhaustive de causes    |
| 2. **Structurer**  | Classer les causes par famille               | 📊 Diagramme d’Ishikawa     | - 6M : Méthode, Main-d'œuvre, Matériel, Milieu, Mesure, Management<br>- Utiliser un tableau blanc ou un outil digital (Miro, Jamboard) | Arbre logique de causes       |
| 3. **Prioriser**   | Focaliser sur les causes majeures            | 📈 Loi de Pareto (80/20)    | - Collecter des données (logs, tickets, incidents)<br>- Classer les fréquences<br>- Graphe Pareto                                      | Top 20 % des causes à creuser |
| 4. **Approfondir** | Identifier les causes racines                | 🔎 Technique des 5 Pourquoi | - Utiliser une cause prioritaire par analyse<br>- S’en tenir aux faits<br>- Arrêter lorsqu’on atteint une cause systémique             | Causes racines documentées    |

---

## 🧪 **Cas pratique : Application e-commerce (type JUMIA)**

### 📌 Problème : Clients signalent que le paiement par mobile money échoue fréquemment.

### 🔹 Étape 1 – Brainstorming

**Participants** : DevOps, Support client, Product Owner, Responsable sécurité
**Idées émises** :

* Panne serveur,
* Expiration du token API,
* Mauvaise implémentation des callbacks,
* Mauvais réseau client,
* Mauvaise gestion des erreurs…

### 🔹 Étape 2 – Diagramme d’Ishikawa

| Catégorie        | Sous-causes identifiées                            |
| ---------------- | -------------------------------------------------- |
| **Méthode**      | Absence de tests automatisés, pas de retry logique |
| **Main-d’œuvre** | Manque de formation sur l’API du fournisseur       |
| **Matériel**     | Temps de réponse du serveur > 3s                   |
| **Milieu**       | Forte affluence (Black Friday), surcharge réseau   |
| **Mesure**       | Pas de logs côté paiement                          |
| **Management**   | Manque de pilotage du SLA fournisseur              |

📌 **Diagramme Ishikawa visuel :** *(à faire sur Miro, ou dessiné sur tableau)*

---

### 🔹 Étape 3 – Pareto : Analyse chiffrée des 100 derniers échecs

| Cause                          | Nombre d’occurrences | % cumulé |
| ------------------------------ | -------------------- | -------- |
| Expiration de token API        | 35                   | 35%      |
| Erreur callback non gérée      | 25                   | 60%      |
| Temps de réponse élevé         | 20                   | 80%      |
| Mauvaise gestion réseau client | 10                   | 90%      |
| Logs insuffisants              | 10                   | 100%     |

📊 **Graphique Pareto** :

* 80 % des échecs viennent de 3 causes
* Focus sur : token expiré, erreur callback, lenteur serveur

---

### 🔹 Étape 4 – 5 Pourquoi : *Exemple sur « Token API expiré »*

| Pourquoi ?                                           | Réponse                                                         |
| ---------------------------------------------------- | --------------------------------------------------------------- |
| 1. Pourquoi le token expire-t-il ?                   | Il a une durée de validité de 30 min.                           |
| 2. Pourquoi n’est-il pas renouvelé automatiquement ? | Le code de renouvellement n’est pas déclenché après expiration. |
| 3. Pourquoi le code n’est-il pas déclenché ?         | Il manque une condition dans la fonction d’authentification.    |
| 4. Pourquoi cette condition est-elle manquante ?     | La logique a été codée manuellement sans tests.                 |
| 5. Pourquoi n’y avait-il pas de tests ?              | Absence de processus CI pour les intégrations API.              |

🎯 **Cause racine :** Absence de processus de validation automatisée pour les intégrations tierces.

---

## ✅ Bonnes pratiques pour déployer la méthode en entreprise

| Pratique                                      | Description                                                                     |
| --------------------------------------------- | ------------------------------------------------------------------------------- |
| **Former les équipes à la pensée systémique** | Encourage la compréhension en profondeur au-delà des symptômes                  |
| **Documenter chaque étape**                   | Utiliser des templates partagés pour chaque outil                               |
| **Croiser les regards (pluridisciplinarité)** | Dev, support, métier, qualité…                                                  |
| **Visualiser et partager**                    | Diagrammes, graphe Pareto et résultats 5P affichés ou partagés dans les équipes |
| **Standardiser la démarche**                  | Intégrer les 4 étapes dans les procédures d’analyse incident                    |
| **Mesurer les impacts**                       | Taux de récurrence incidents avant/après, temps moyen de résolution, etc.       |

---

## 📋 Outils numériques recommandés

| Outil                     | Utilité                                    | Type               |
| ------------------------- | ------------------------------------------ | ------------------ |
| **Miro / Mural**          | Diagramme d’Ishikawa collaboratif          | Cloud collaboratif |
| **Trello / Notion**       | Suivi des 5 Pourquoi / actions correctives | Organisation       |
| **Excel / Google Sheets** | Graphe Pareto automatisé                   | Tableur            |
| **Retool / Power BI**     | Analyse quantitative des incidents         | DataViz            |

---

## 📘 Synthèse comparative des 4 méthodes

| Méthode       | Valeur ajoutée                         | Risques si utilisée seule           |
| ------------- | -------------------------------------- | ----------------------------------- |
| Brainstorming | Ouvre l’esprit à toutes les hypothèses | Trop vague, non hiérarchisé         |
| Ishikawa      | Structure et catégorise les causes     | Nécessite rigueur, peut être biaisé |
| Pareto        | Met l’accent sur les causes critiques  | Ignore les effets rares mais graves |
| 5 Pourquoi    | Creuse les causes racines              | Peut être subjectif ou simpliste    |

---

## 🏁 Conclusion

La **synergie entre Brainstorming, Ishikawa, Pareto et 5 Pourquoi** constitue une **approche robuste** de résolution de problèmes complexes.
Utilisée avec rigueur, cette méthodologie permet non seulement de **réagir efficacement**, mais aussi de **prévenir durablement** la récurrence des incidents.

✅ **Adopter cette approche dans vos équipes, c’est :**

* Réduire les temps de résolution,
* Mieux capitaliser les erreurs passées,
* Améliorer la qualité, la sécurité et l’expérience utilisateur.

---

Souhaitez-vous un **template prêt à l’emploi** (tableau Notion, Google Sheets, PDF interactif) pour déployer cette méthode dans votre organisation ?
