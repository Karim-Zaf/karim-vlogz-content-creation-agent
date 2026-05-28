Tu lances le pipeline de génération de kit créatif pour un reel de Karim (@karim.vlogz).

**Deux modes** :
- `quick=oui` → hook seul, affiché dans le chat, pas de fichiers (équivalent à `/hook`)
- `quick=non` (défaut) → kit complet écrit dans `content/<date>_<topic>/`

## Paramètres attendus

| Paramètre | Requis | Défaut | Description |
|---|---|---|---|
| `topic` | oui | — | Sujet court (ex: `norway_day_copenhagen`, snake_case) |
| `description` | oui | — | 1 à 3 phrases décrivant la vidéo |
| `format` | oui | — | `F1` (spontané facecam), `F2` (voix off + b-rolls), `F3` (b-rolls + hook + musique) |
| `quick` | non | `non` | `oui` → hook seul. `non` → pipeline complet |
| `plateforme` | non | `instagram` | `instagram`, `tiktok`, ou `both` |
| `voiceover` | non | auto | `oui` ou `non`. Auto = oui si F2 et quick=non |

Arguments fournis par l'utilisateur :

$ARGUMENTS

---

## Étape 0 — Valider les paramètres

Parse les arguments et extrais : `topic`, `description`, `format`, `quick` (défaut `non`), `plateforme` (défaut `instagram`), `voiceover` (défaut auto).

Si `topic`, `description` ou `format` manquent → **arrête et demande**. N'invente rien.

Lis :

```
Read knowledge/profil-createur.md
```

---

## ROUTE A — mode `quick=oui` (hook seul, ultra-rapide)

Si `quick=oui` :

1. Lance UNIQUEMENT hook-agent :

```
Task(
  subagent_type: "hook-agent",
  prompt: "Génère 3 hooks overlay + recommande la meilleure.

Topic : <topic>
Description : <description>
Format vidéo : <format>

Lis knowledge/profil-createur.md et knowledge/hook-patterns.md avant.
Retourne 3 variantes (EN fact-bomb, AR, Mix EN+AR) + ## 🎯 Recommandation.
Considère qu'une seule phrase darija punchy peut battre les 3 variantes."
)
```

2. Affiche le résultat directement dans le chat.
3. **PAS de dossier**, **PAS de fichiers**, **PAS de reviewer**.
4. Termine : "À toi de choisir, Karim."

**STOP ici si quick=oui.**

---

## ROUTE B — mode `quick=non` (pipeline complet)

### Étape 1 — Créer le dossier de sortie

```bash
mkdir -p content/<YYYY-MM-DD>_<topic>
```

### Étape 2 — Lancer hook + caption + music EN PARALLÈLE

**Important** : 1 seul message avec 3 Task calls en parallèle.

- `hook-agent` → écrit dans `hook.txt`
- `description-agent` → écrit dans `description.txt`
- `music-agent` → écrit dans `music.md`

### Étape 3 — Voix off (séquentiel, si applicable)

Skip si `voiceover = non` OU si `format ∈ {F1, F3}`.

Récupère le hook **recommandé** (Variante taggée 🎯) et passe-le à voiceover-agent.

Écris dans `voiceover.txt`.

### Étape 4 — Reviewer (1 PASSE UNIQUEMENT, non-bloquant)

```
Task(
  subagent_type: "reviewer-agent",
  prompt: "Review NON-BLOQUANTE du kit suivant.

=== HOOK === <contenu de hook.txt>
=== CAPTION === <contenu de description.txt>
=== MUSIC === <contenu de music.md>
=== VOICEOVER === <contenu de voiceover.txt ou 'N/A'>

Format : <format>
Plateforme : <plateforme>

PASS par défaut. FAIL uniquement si vrai blocker (français, andalou, caption >3 lignes, 6+ hashtags)."
)
```

Écris dans `review.md`.

### Étape 5 — Rapport final

Affiche :
- Dossier : `content/<YYYY-MM-DD>_<topic>/`
- Hook recommandé (variante 🎯)
- Récap 1 ligne pour caption / music / voix off
- Verdict reviewer
- "À toi de juger, Karim."

---

## Règles d'orchestration strictes

- ❌ **JAMAIS de boucle de correction.** Reviewer = 1 passe.
- ❌ **JAMAIS relancer un agent pour corriger un détail cosmétique.**
- ✅ **Toujours afficher le résultat même si reviewer signale des améliorations.**
- ✅ **Toujours hook+caption+music en parallèle dans un seul message.**
- ✅ **Toujours respecter `quick=oui` = hook seul, rien d'autre.**
