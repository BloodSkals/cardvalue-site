# CardValue for WikiMasters

Site public de présentation et politique de confidentialité de **CardValue for WikiMasters**.

CardValue est une extension Chrome non affiliée à WikiMasters qui :
- affiche le prix moyen du marché sur les cartes de la collection WikiMasters ;
- permet de trier la collection par prix moyen ;
- utilise un cache local pour limiter les requêtes répétées.

## Limitation connue : vitesse du premier chargement

Le premier chargement des prix peut être lent sur les grandes collections.

CardValue lit les résumés de marché exposés par WikiMasters carte par carte. Pour une collection de plusieurs centaines ou milliers de cartes, cela implique donc de nombreuses requêtes vers l'API de WikiMasters.

WikiMasters applique par ailleurs une protection contre les requêtes automatisées destinées notamment à limiter les bots et comportements de triche. Lorsque trop de requêtes sont envoyées sur une courte période, l'API peut répondre avec le code `automation_limit` :

```json
{
  "error": "Trop de requêtes automatisées. L'automatisation n'est pas autorisée — voir le règlement.",
  "code": "automation_limit"
}
```

CardValue doit donc limiter sa cadence et ne peut pas accélérer indéfiniment la récupération des prix. La vitesse dépend également du temps de réponse et de la capacité disponible des serveurs WikiMasters au moment du chargement.

Une fois les prix récupérés, CardValue les met en cache localement afin d'éviter de refaire inutilement le même travail à chaque visite.

## FAQ

### Pourquoi CardValue ne charge-t-il pas instantanément tous les prix ?

WikiMasters ne fournit pas, dans l'API actuellement utilisée par CardValue, un endpoint permettant de récupérer en une seule requête les prix de toute une collection. Les moyennes de marché doivent être demandées carte par carte.

### Pourquoi ne pas simplement envoyer beaucoup plus de requêtes en parallèle ?

WikiMasters possède une protection anti-automatisation. Une cadence trop élevée peut être refusée avec `automation_limit`. Augmenter fortement le nombre de requêtes simultanées ne rend donc pas nécessairement le chargement plus rapide et peut au contraire provoquer davantage de requêtes refusées.

### Est-ce que CardValue contourne cette protection ?

Non. CardValue utilise les données de marché accessibles à l'utilisateur connecté et doit composer avec les limites appliquées par l'API WikiMasters.

### Pourquoi les chargements suivants sont-ils plus rapides ?

Les moyennes déjà récupérées sont conservées dans un cache local pendant la durée configurée dans l'extension. Tant qu'une valeur est encore valide dans ce cache, CardValue n'a pas besoin de la demander à nouveau.

## Confidentialité

La politique de confidentialité publique est disponible dans `privacy-policy.html`.

## Support

Les demandes de support et signalements peuvent être ouverts via les Issues de ce dépôt.

## Affiliation

CardValue est indépendante et non officielle. Elle n’est ni éditée, ni approuvée, ni sponsorisée par WikiMasters.
