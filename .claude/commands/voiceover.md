Tu génères uniquement un script de voix off (darija) pour un reel format F2 de Karim, sans le reste du kit.

## Paramètres attendus

| Paramètre | Requis | Défaut | Description |
|---|---|---|---|
| `topic` | oui | — | Sujet court |
| `description` | oui | — | 1-3 phrases décrivant le contenu / les b-rolls |
| `hook` | non | — | Si Karim a déjà un hook overlay choisi, le fournir pour éviter répétition |

Arguments fournis :

$ARGUMENTS

---

## Étape 0 — Valider

Parse `topic`, `description`, `hook`. Si `topic` ou `description` manquent, demande à l'utilisateur.

---

## Étape 1 — Spawn voiceover-agent

```
Task(
  subagent_type: "voiceover-agent",
  prompt: "Génère un script voix off F2 pour ce reel.

Topic : <topic>
Description : <description>
Hook overlay déjà choisi (NE PAS RÉPÉTER) : <hook ou 'aucun fourni'>

Lis knowledge/profil-createur.md et knowledge/voiceover-techniques.md avant.
Full darija + sprinkle arabe littéraire si terme officiel.
25-40 secondes parlées. Fact bomb au milieu.
Pas de catchphrase forcée. Pas de français. Pas de heritage andalou."
)
```

---

## Étape 2 — Présentation

Affiche le script darija + traduction FR optionnelle à l'utilisateur. Pas de dossier `content/` créé pour cette commande rapide.
