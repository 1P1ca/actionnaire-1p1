# Parcours de valeur actionnaire — architecture MVP

## Objectif

Un module autonome qui qualifie une situation d’actionnaire-dirigeant, produit une lecture structurée et transforme les signaux en architecture cible, priorités et feuille de route. Il peut être monté sous un parcours du site existant sans toucher aux pages actuelles.

## Workflow

1. Contexte : rôle, horizon, secteur et taille.
2. Questionnaire : 12 questions, échelle 1 à 5, réparties entre personnel, financier, entreprise, 4C et décision.
3. Analyse : moyenne globale, maturité, confiance indicative, 4C et trois écarts.
4. Décision : P0/P1/P2 générées par le niveau global et les dépendances.
5. Action : feuille de route 30/60/90 jours et 12 mois.
6. Rapport : vue imprimable / PDF du navigateur.

## Modèle de données proposé

```js
Assessment {
  id, createdAt, locale,
  profile: { role, horizon, sector, employees },
  answers: [{ questionId, dimension, value }],
  scores: { overall, confidence, maturity, human, customer, structural, social },
  gaps: { profit, value, wealth },
  priorities: [{ level, title, rationale }],
  roadmap: [{ phase, outcome, actions }]
}
```

Le MVP garde les réponses localement dans le navigateur. Une prochaine version peut ajouter un formulaire de consentement, une API sécurisée, des comptes, l’export PDF serveur et une transmission CRM.

## Scoring et règles

- Chaque réponse est notée de 1 à 5 et normalisée sur 100.
- Maturité globale : Identify (0–41), Protect (42–57), Build (58–72), Harvest (73–87), Manage (88–100).
- 4C : moyenne des questions Human, Customer, Structural et Social.
- Profit Gap : signal qualitatif dérivé de la dimension entreprise.
- Value Gap : signal dérivé des 4C.
- Wealth Gap : signal dérivé des dimensions personnelle et financière.
- P0 : risque, dépendance ou manque d’alignement à traiter en premier.
- P1 : levier de transférabilité qui augmente les options.
- P2 : intégration patrimoine / gouvernance / amélioration continue.

Ces règles servent à orienter une discussion. Elles ne remplacent pas une évaluation, une modélisation financière ou un avis professionnel.

## Intégration au site existant

Le MVP est volontairement statique et sans dépendance : `index.html`, `styles.css` et `app.js`. Il peut être servi sous `/parcours`, placé dans un iframe contrôlé ou converti en composant du site principal. Le logo existant est réutilisé. Les fichiers de référence dans `sources/` demeurent inchangés.
