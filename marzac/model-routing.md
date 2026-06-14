# Routage par modèle

Adaptation de la skill `cost-aware-llm-pipeline` d'ECC à notre board. Principe général : Opus pour le jugement et la synthèse, Sonnet pour produire et implémenter, Haiku pour explorer et trier. Haiku coûte environ quinze fois moins qu'Opus, et sur les tâches sans raisonnement profond l'écart de qualité est négligeable.

## La politique par agent (board StayLabs)

- Opus : Alpha seul, le cerveau qui lit les données, arbitre et délègue.
- Sonnet : production et orchestration de pôle. beta, beta-1 (stratège), beta-2 (rédacteur), gamma, gamma-2 (conversion), sigma, delta, tau, tau-1 (dev), tau-2 (UX).
- Haiku : tâches légères et veille. beta-3 (audit on-page), gamma-1 (rapport quotidien), sigma-1 et sigma-2 (veille), delta-1 et delta-2 (finance).

## Le garde-fou anti-bug

Le champ `model` d'une fiche d'agent est, par défaut, hérité de la session si absent : en Routine Opus, une fiche sans modèle tourne donc en Opus. Pire, un bug remonté fait que le champ `model` est parfois ignoré et le sous-agent retombe sur le modèle parent ; seul le modèle passé explicitement à l'appel a alors un effet.

Donc deux niveaux de protection :
1. Chaque fiche `.claude/agents/*.md` porte un `model` explicite (jamais d'héritage silencieux).
2. Au moment de déléguer via Task, Alpha précise le modèle de l'agent lancé, pour que le cas bugué retombe sur le bon palier.

Le sélecteur de modèle de la Routine ne pilote que la session principale, c'est à dire Alpha. La différenciation par agent vit dans les fiches committées, relues à chaque clone frais. Rien à changer dans la config de la Routine.
