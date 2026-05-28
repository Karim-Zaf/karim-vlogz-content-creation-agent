# Reel Content Generator — système d'agents IA personnalisé pour @karim.vlogz

Système local, modulaire, basé sur Claude Code. Génère un **kit créatif complet** pour un reel Instagram/TikTok à partir d'une simple description : hook overlay, caption, suggestion musicale, script voix off (si demandé), hashtags.

Inspiré de l'architecture du projet `polygon-problems-generator`.

---

## Pourquoi ce système

L'objectif : automatiser la création de contenu **tout en gardant la voix authentique de Karim**. Les agents lisent un fichier de profil créateur (`knowledge/profil-createur.md`) qui contient :
- L'identité (Tunisien, vlog voyage / découverte)
- Les 3 formats codifiés (F1 spontané / F2 voix off / F3 b-rolls + musique)
- Les règles de captions / hashtags / langues
- Des exemples annotés de 5 reels publiés (training data réel)

Chaque agent ne sort jamais de ce cadre.

---

## Structure du projet

```
reel-content-generator/
├── .claude/
│   ├── commands/
│   │   ├── generate-reel.md     ← /generate-reel — pipeline complet
│   │   ├── hook.md              ← /hook — juste les hooks
│   │   └── voiceover.md         ← /voiceover — juste le script darija
│   └── agents/
│       ├── orchestrator.md      ← coordinateur principal
│       ├── hook-agent.md        ← 3 variantes de hook overlay
│       ├── description-agent.md ← caption + hashtags
│       ├── music-agent.md       ← mood + références
│       ├── voiceover-agent.md   ← script darija (+ littéraire)
│       └── reviewer-agent.md    ← validation finale (PASS/FAIL)
├── knowledge/
│   ├── profil-createur.md       ← profil de Karim — lu par tous les agents
│   ├── hook-patterns.md         ← patterns de hooks observés
│   ├── caption-rules.md         ← règles flexibles de caption
│   ├── music-genres.md          ← moods et références musicales
│   └── voiceover-techniques.md  ← techniques voix off darija
├── templates/
│   ├── hook.txt
│   ├── description.txt
│   └── voiceover.txt
├── content/                     ← sortie générée (gitignored)
│   └── <YYYY-MM-DD>_<topic>/
├── .gitignore
└── README.md
```

---

## Utilisation

### ⚡ Le plus rapide — `/hook` (hook seul, ~30 secondes)

**Utilisation recommandée 80% du temps.** Pas de dossier, pas de fichier. Juste 3 hooks + une recommandation, directement dans le chat.

```
/hook topic=tivoli_gardens description="Parc d'attractions historique à Copenhague qui a inspiré Walt Disney pour Disneyland." format=F2
```

→ Sortie : 3 variantes (EN fact-bomb / AR / Mix EN+AR) + `🎯 Recommandation` de la meilleure variante avec la raison.

Équivalent : `/generate-reel quick=oui topic=... description=... format=...`

### Génération rapide d'une voix off — `/voiceover`

```
/voiceover topic=reffen_food_market description="Plus grand marché de street food de Scandinavie." hook="Scandinavia's largest food market 🇩🇰"
```

### Pipeline complet — `/generate-reel`

Kit créatif complet écrit sur disque : hook + caption + music + voix off + review.

```
/generate-reel topic=norway_day_copenhagen description="Fête nationale norvégienne à Copenhague, ambiance familles costumes traditionnels." format=F2 plateforme=instagram
```

**Paramètres** :
| Paramètre | Requis | Défaut | Valeurs |
|---|---|---|---|
| `topic` | oui | — | snake_case |
| `description` | oui | — | 1-3 phrases sur le contenu filmé |
| `format` | oui | — | `F1` / `F2` / `F3` |
| `quick` | non | `non` | `oui` → hook seul (équivalent `/hook`) |
| `plateforme` | non | `instagram` | `instagram` / `tiktok` / `both` |
| `voiceover` | non | auto (oui si F2) | `oui` / `non` |

**Sortie** (mode quick=non) :
```
content/2026-05-29_norway_day_copenhagen/
├── hook.txt
├── description.txt
├── music.md
├── voiceover.txt       (si F2)
└── review.md
```

**Performance attendue** :
- Mode `quick` : ~30s
- Mode full (F1/F3) : ~1-2 min (hook + caption + music en parallèle, 1 passe reviewer)
- Mode full (F2 avec voix off) : ~2-3 min

Le reviewer est **non-bloquant** : il signale des améliorations mais ne déclenche jamais de boucle de correction. Tu décides.

---

## Les 3 formats vidéo (à choisir)

| Format | Description |
|---|---|
| **F1** — Spontané vlog | Facecam, Karim parle en marchant, cuts simples + parfois b-rolls |
| **F2** — Voix off + b-rolls | B-rolls du voyage avec voix off darija enregistrée par-dessus |
| **F3** — B-rolls + hook + musique | Uniquement b-rolls + texte overlay + musique de fond, pas de voix |

---

## Les 6 agents

| Agent | Rôle | Tools |
|---|---|---|
| `orchestrator` | Coordonne le pipeline, gère le dossier de sortie | Read, Write, Bash, Task |
| `hook-agent` | Génère 3 variantes de hook overlay (EN / AR / Mix) | Read |
| `description-agent` | Génère caption (AR/EN flexible) + hashtags | Read |
| `music-agent` | Suggère mood + 1-2 références (ou `null`) | Read |
| `voiceover-agent` | Génère script darija (+ sprinkle littéraire) — F2 uniquement | Read |
| `reviewer-agent` | Avis NON-BLOQUANT 1 passe — signale améliorations, PASS par défaut | Read |

Tous les agents (sauf orchestrator) sont en `Read only` pour éviter qu'ils n'écrivent en dehors de leur scope.

---

## Knowledge — le cœur du système

Les 5 fichiers `knowledge/` sont la source de vérité. **Tous les agents les lisent au démarrage** de leur tâche.

| Fichier | Lu par |
|---|---|
| `profil-createur.md` | TOUS les agents |
| `hook-patterns.md` | hook-agent, reviewer-agent |
| `caption-rules.md` | description-agent, reviewer-agent |
| `music-genres.md` | music-agent, reviewer-agent |
| `voiceover-techniques.md` | voiceover-agent, reviewer-agent |

**Pour faire évoluer le système** : édite ces fichiers. Pas besoin de modifier les agents.

---

## Évolutions possibles (plus tard)

- Ajouter un `thumbnail-agent` pour générer des descriptions visuelles de cover
- Ajouter un `trend-agent` qui suggère des sujets selon les tendances
- Connecter à n8n / API pour publier automatiquement
- Ajouter un `analytics-agent` qui apprend des perfs des posts publiés

Pour l'instant, le système reste **minimal et focus** sur la génération du kit.

---

## Règles strictes que le système respecte

1. Karim est **tunisien tout court** (pas tunisien-andalou)
2. **Jamais de français** dans le contenu final
3. Caption max 2 lignes + 3-5 hashtags
4. Voix off en **darija** + sprinkle arabe littéraire si terme officiel
5. Aucune catchphrase imposée artificiellement
6. Ton **chill vlog discovery**, pas documentaire pesant
7. Pas de cliché "vlog voyage Instagram générique"
# karim-vlogz-content-creation-agent
