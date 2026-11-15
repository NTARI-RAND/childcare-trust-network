> Traduction communautaire (brouillon) — politique NTARI P2-002, Diffusion multilingue mondiale. Source : CONFORMANCE.md (original anglais, instantané du 2026-10-05). Brouillon communautaire assisté par machine, en attente de relecture par le mainteneur régional conformément à P2-002 §3.1. Les spécifications techniques essentielles restent en anglais conformément au §2.2.
>
> Vous avez remarqué une erreur de traduction ? N'hésitez pas à la corriger
> vous-même : forkez le dépôt https://github.com/NTARI-RAND/childcare-trust-network et
> ouvrez une pull request. Les corrections de traduction sont des
> contributions précieuses, tout autant que le code.

> L'original anglais est normatif. Cette traduction est proposée pour la lecture, non pour l'interprétation : là où elle diverge de `CONFORMANCE.md`, l'anglais prévaut. Les mots-clés normatifs (MUST, MUST NOT, SHOULD, SHOULD NOT, MAY), les noms de champs, les libellés et les identifiants sont conservés en anglais, car ils constituent le contrat de conformité.

# CTN — Autodescription de conformité

*Auto-attestée jusqu'à ce qu'une suite de tests cite ces identifiants (registre : `JFA/jfa-conformance-suite.py`). CTN en est au stade de proposition ; « respecté par conception » signifie que la spécification (`CLAUDE.md`) énonce la règle et le critère d'acceptation — le code doit encore la faire respecter.*

**Forme :** l'économie du soin à enjeux élevés de la partie VI de l'architecture — distribution complète des évaluations, couche de sécurité axée d'abord sur la prévention et prévalant sur toute autre règle.

| ID | Invariant | Statut |
|---|---|---|
| COV-1 | Aucune moyenne ; distribution complète | **Respecté par conception** — section « Ne pas faire de moyenne », critère d'acceptation par grep ; délégué à la CI lors de la construction |
| COV-2 | La note la plus basse est le manquement | **Respecté par conception** — `-1` signifie préjudice, `harm_flagged`, commentaire obligatoire |
| COV-3 | Symétrique ; toute affirmation peut recevoir une réponse | **Partiel** — évaluation multidirectionnelle, oui ; contestation/droit de réponse : question ouverte (OQ-6) |
| COV-4 | Détermine si, jamais combien | **Respecté par conception** — trois signaux honnêtes (vérification, distribution, ancienneté), jamais fusionnés |
| REC-1 | En ajout seul | **Respecté par conception** — événements d'évaluation immuables ; attestation par témoins : question ouverte (OQ-7) |
| REC-2 | Pardonner, ne jamais cacher | **Respecté par conception** — les contestations signalent et contextualisent, n'effacent jamais |
| REC-3 | Aucune donnée personnelle (PII) dans les communs | **Respecté par conception** — les données des enfants n'entrent jamais dans le magasin d'événements ni dans aucune sortie de réputation |
| REC-9 | Types de relations | **Ouvert** (OQ-8) |
| ECO-4/5 | Séquestre d'abord ; gagné, jamais acheté, si le crédit entre un jour en jeu | **Choix par défaut adopté** (OQ-5) |
| GOV-9 | Document vivant des questions ouvertes | **Respecté** — `OPEN-QUESTIONS.md` est livré avec ce document fondateur |
| GOV-10 | Communs copyleft | **Respecté** — AGPL-3.0, indiqué dans la spécification |

**Préséance nommée :** le volet de sécurité des enfants prévaut sur le pacte en cas de conflit — le précédent des enjeux élevés de la partie VI, adopté délibérément, les garanties procédurales régissant la durabilité des conséquences plutôt que la protection immédiate.

**Ligne d'honnêteté :** CTN n'a pas de registre attesté par témoins ; toute affirmation de conduite qu'il formule aujourd'hui est auto-attestée (problème ouvert 2 de l'architecture).
