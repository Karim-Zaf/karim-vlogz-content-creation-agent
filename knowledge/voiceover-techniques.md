# Voiceover techniques — script voix off de Karim

> Guide pour le `voiceover-agent`. La voix off de Karim est **full darija tunisien**, avec parfois un peu d'arabe littéraire pour les termes officiels.

---

## Règle fondamentale

**Langue** : darija tunisien par défaut, sprinkle d'arabe littéraire UNIQUEMENT pour :
- Noms officiels (`عيد الإستقلال` au lieu de "fête de l'indépendance")
- Termes historiques précis
- Noms d'institutions, monuments officiels

**Ton** : conversationnel, naturel, comme si Karim parlait à un pote. **PAS de ton documentaire formel, PAS de ton de présentateur télé.**

---

## Durée cible

- **Total script** : 25 à 40 secondes parlées (matche la durée typique d'un reel)
- **Phrases courtes** : 3 à 8 mots chacune
- **Pauses naturelles** entre phrases (respirations, transitions)

## Structure d'un script F2 (voix off + b-rolls)

### Phase 1 — Accroche (0 à 5 secondes)
Hook parlé qui complète l'overlay textuel mais ne le répète pas.

**Formules d'ouverture observées/proposées** :
- `ياو...` (yo...)
- `تخيّل معايا...` (imagine avec moi...)
- `شدّ روحك...` (tiens-toi bien...)
- `صراحة...` (honnêtement...)
- `أنا توا في [lieu]` (je suis là à [lieu])

### Phase 2 — Développement (5 à 25 secondes)
2 à 4 phrases qui racontent ce qu'on voit, ce qui surprend, ce qui est unique.

**Pattern fact-bomb au milieu** :
Placer LE fait remarquable du sujet vers la moitié du reel = trigger save. C'est le "moment où le viewer pense oh shit faut que je sauvegarde".

**Exemple structure** :
- Phrase 1 : situer le lieu / l'action
- Phrase 2 : fact bomb (chiffre, anecdote historique, contraste)
- Phrase 3 : observation personnelle / ressenti chill

### Phase 3 — Outro / Punchline (25 à 35 secondes)
Phrase de clôture courte. Peut être :
- Une question ouverte qui pousse au commentaire
- Une observation conclusive chill
- Une mini-réflexion personnelle
- **PAS de catchphrase imposée** ("صدفة ؟ لا." est une idée non validée — l'agent ne l'impose PAS sauf si le sujet s'y prête vraiment)

## Tics de langage darija (à utiliser naturellement, pas tous d'un coup)

| Formule | Sens | Quand |
|---|---|---|
| `ياو` | yo / eh | Ouverture, surprise |
| `تخيّل معايا` | imagine avec moi | Pour faire ressentir une scène |
| `شدّ روحك` | tiens-toi bien | Avant un fact remarquable |
| `صراحة` | honnêtement | Avis personnel |
| `حقيقة` | en vrai | Insistance |
| `الحاجة الكبيرة هاي` | le truc énorme c'est | Annonce fact bomb |
| `صدفة ؟ لا` | coïncidence ? non | Punchline conclusive (à utiliser avec parcimonie) |
| `حاسس روحي` | je me sens | Ressenti |
| `ما تخيّبش` | ça déçoit pas | Validation positive d'un lieu |

## Tics arabe littéraire (à doser, max 2-3 mots par script)

À insérer UNIQUEMENT sur :
- `عيد الإستقلال` (fête de l'indépendance)
- `العصر [...]` (l'époque [...])
- `الحضارة [...]` (la civilisation [...])
- `التاريخ` (l'histoire) — quand contexte officiel
- Noms propres officiels

**Reste 100% darija autour de ces termes.**

## Anti-patterns voix off

- ❌ Ton de présentateur télé / documentaire formel
- ❌ Phrases longues complexes (>10 mots)
- ❌ Arabe littéraire en continu (ça devient lourd)
- ❌ Lire des chiffres compliqués mot à mot
- ❌ Catchphrase IA générique ("dans ce reel je vais vous montrer...")
- ❌ Voix off qui dit la MÊME chose que l'overlay (redondance)
- ❌ Énumération sèche de faits (toujours injecter un ressenti)
- ❌ Conclusion moralisatrice ("voilà la leçon...")
- ❌ Faux suspense ("vous n'allez pas croire ce qui s'est passé ensuite...")

## Format de sortie

L'agent retourne un bloc lisible **sans timecodes**, juste le script en darija prêt à enregistrer.

**Exemple** :
```
ياو... أنا في Nørrebro، شارع واحد بركة في كوبنهاغن.
تخيّل معايا... 60 ثقافة، شارع واحد، نفس الحي.
هاو الحاجة الكبيرة : لا أحد يحس روحه غريب هنا، الكل يحس روحه في بلاده.
صراحة... شي حاجة ما تنشاف كان هنا.
```

L'agent peut **optionnellement** ajouter une traduction française entre crochets en dessous pour que Karim valide le sens, mais ce n'est PAS dans le fichier final voix off.

## Cohérence avec hook overlay

- Le hook overlay et la voix off doivent **se compléter**, pas se répéter
- Si hook = `60 cultures, 1 street, Denmark` → la voix off ne redit pas "60 cultures sur une rue" mais raconte l'histoire de cette rue
- Le hook donne le titre, la voix off donne le récit

## Adaptation par format

| Format | Voix off ? |
|---|---|
| F1 spontané | Pas de voix off — Karim parle face caméra directement |
| F2 voix off + b-rolls | **Voix off complète selon ce guide** |
| F3 b-rolls + hook + musique | Pas de voix off — overlay + musique seuls |
