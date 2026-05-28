Tu génères uniquement les hooks overlay pour un reel de Karim (3 variantes), sans le reste du kit.

## Paramètres attendus

| Paramètre | Requis | Défaut | Description |
|---|---|---|---|
| `topic` | oui | — | Sujet court |
| `description` | oui | — | 1-2 phrases décrivant la vidéo |
| `format` | non | `F1` | F1, F2, ou F3 |

Arguments fournis :

$ARGUMENTS

---

## Étape 0 — Valider

Parse `topic`, `description`, `format`. Si `topic` ou `description` manquent, demande à l'utilisateur.

---

## Étape 1 — Spawn hook-agent

```
Task(
  subagent_type: "hook-agent",
  prompt: "Génère 3 hooks overlay pour le reel suivant.

Topic : <topic>
Description : <description>
Format vidéo : <format>

Lis knowledge/profil-createur.md et knowledge/hook-patterns.md avant.
Retourne exactement 3 variantes : EN fact-bomb, AR (darija ou littéraire selon mood), Mix EN+AR inséré.
Pas de catchphrase forcée. Pas de français. Pas de heritage andalou."
)
```

---

## Étape 2 — Présentation

Affiche directement les 3 variantes générées par l'agent à l'utilisateur. Pas besoin de créer de dossier `content/` pour cette commande rapide — c'est une utilisation one-shot pour brainstorming.

Si l'utilisateur veut sauvegarder, il peut copier-coller.
