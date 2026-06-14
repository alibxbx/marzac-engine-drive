# Récupération itérative pour les sous-agents

Adaptation du pattern de récupération itérative d'ECC au board Alpha. Le problème : en Routine, un sous-agent qui aspire tout le contexte coûte cher en tokens et dilue son attention. La parade est de ne récupérer que le nécessaire, et d'élargir seulement si besoin.

## Le principe

Alpha ne déverse pas le repo dans chaque sous-agent. Il lit le rapport agrégé déposé pour les agents (`data/seo-latest.json` : deltas SEO, bloc PostHog, leads récents), situe le goulot, puis délègue des tâches précises. Chaque sous-agent part étroit : lecture ciblée par recherche et motif plutôt que survol complet, et il n'ouvre un fichier en entier que s'il en a vraiment besoin.

## Pourquoi ça compte

Moins de contexte chargé veut dire moins de tokens et une sortie plus focalisée. Couplé au routage par modèle, l'effet se cumule : un agent Haiku qui ne lit que trois fichiers ciblés coûte une fraction d'un agent qui hérite d'Opus et avale tout le dépôt. La règle tient en une phrase : commencer au plus serré, élargir seulement sur preuve que c'est nécessaire.
