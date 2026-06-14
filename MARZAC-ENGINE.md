# Moteur Marzac

Copie de travail dérivée d'ECC (`affaan-m/ECC`), taillée et adaptée pour devenir l'outillage d'agents de Marzac. L'upstream reste la référence complète : ici on ne garde que ce qui sert les véhicules de Marzac (StayLabs marketing et StayLabs HK) et le board d'agents piloté par Alpha, et on ajoute une couche `marzac/` qui traduit les patterns clés d'ECC dans notre stack et nos règles.

Ce repo est une bibliothèque de références et d'outillage, pas un service. Rien ne s'exécute tout seul. On n'active aucun hook qui lance du shell sans l'avoir lu, et les secrets comme les MCP restent gérés côté hébergeur, jamais dans le repo.

## Notre contexte

- Stack : Next.js 14 + TypeScript + Supabase + Tailwind, déployé sur Vercel.
- Agents : board Alpha en Routine cloud Claude Code (clone frais à chaque run), Codex en complément.
- Éditorial : français, grounding strict, zéro tiret cadratin, prose humaine sans marqueurs d'IA, fiscal et YMYL en file de validation humaine.
- Sécurité : aucun secret dans le repo ; le repo sert de canal de données et de référence, pas de coffre.

## Ce qu'on garde d'ECC, et pourquoi

Règles : `rules/common`, `typescript`, `react`, `web`, `python`. Le reste des packs de langages ne correspond pas à notre stack.

Agents généraux et utiles : planner, architect, code-architect, code-explorer, code-reviewer, code-simplifier, refactor-cleaner, build-error-resolver, doc-updater, docs-lookup, e2e-runner, security-reviewer, tdd-guide, typescript-reviewer, react-reviewer, react-build-resolver, database-reviewer, python-reviewer, harness-optimizer, loop-operator, chief-of-staff, performance-optimizer, silent-failure-hunter, type-design-analyzer, pr-test-analyzer, seo-specialist, marketing-agent.

Skills clés, par thème :
- Coûts : cost-aware-llm-pipeline, cost-tracking, ecc-tools-cost-audit, context-budget.
- Vérification : eval-harness, agent-eval, ai-regression-testing, agent-architecture-audit.
- Orchestration : agentic-engineering, autonomous-loops, continuous-agent-loop, dmux-workflows, council, continuous-learning-v2.
- Stack : backend-patterns, frontend-patterns, frontend-design-direction, api-design, database-migrations, deployment-patterns, docker-patterns, e2e-testing, error-handling, design-system.
- Contenu et acquisition : article-writing, brand-voice, content-engine, crosspost, deep-research.
- Ops : git-workflow, github-ops, email-ops, google-workspace-ops, automation-audit-ops.

## Ce qu'on retire

Les packs de langages et frameworks hors stack (Java, Kotlin, Rust, Go, Swift, C++, C#, Dart, Flutter, Angular, Django, FastAPI, Spring, Laravel, Ruby, Perl, et leurs règles), les verticaux hors sujet (santé, homelab et réseau, blockchain et DeFi, génération média et GAN, énergie, douane), le control-plane Rust `ecc2/` et le dashboard Tkinter. Tout reste récupérable depuis l'upstream ou l'historique git.

## La couche marzac/

Trois adaptations concrètes à notre système, dans `marzac/` :
- `model-routing.md` : notre politique de modèle par agent et le garde-fou anti-bug.
- `verification-grounding.md` : notre boucle de vérification calée sur nos non-négociables éditoriaux.
- `subagent-retrieval.md` : la récupération itérative appliquée au board Alpha.

## Lien avec marzac-os

`marzac-os` reste le cerveau et le blueprint du système, en documentation. Ce repo-ci est la copie opérationnelle d'outillage qu'on adapte. Les patterns retenus ici alimentent les archétypes décrits dans marzac-os.
