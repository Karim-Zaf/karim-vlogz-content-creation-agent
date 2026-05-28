# Music genres — moods et références pour reels

> Guide de génération musicale pour le `music-agent`. Karim est **assez ouvert** musicalement. Parfois pas de musique du tout.

---

## Règle générale

Le music-agent doit toujours retourner :
1. **Un mood principal** (1 à 2 mots clés)
2. **1 ou 2 références concrètes** (artiste, morceau, ou style)
3. **Optionnellement** : `null` si "pas de musique" est plus pertinent

**Format de sortie** :
```
Mood : [mot-clé]
Énergie : [low / mid / high]
Références : [artiste/genre 1], [artiste/genre 2]
Alternative : [genre alternatif si Karim veut varier]
Note : [contexte court, 1 phrase max]
```

---

## Les 4 moods principaux

### 1. Chill / lo-fi
Pour F1 spontané, ambiance détendue, vlog journée tranquille.

**Références** :
- Lo-fi instrumental (FKJ, Toonorth, Joey Pecoraro)
- Lofi hip-hop chill beats
- Soft jazz instrumental
- Bossa nova chill

**Quand l'utiliser** : marche dans une ville le jour, café, parc, vlog moment léger.

### 2. Cinematic emotional
Pour F2 voix off ou F3 b-rolls quand le sujet est grand, beau, historique, ou émotionnel.

**Références confirmées par Karim** :
- **Dean Valentine — Vladimir's Theme** (utilisé pour Norway Day ✅)

**Autres références à proposer** :
- Joe Hisaishi instrumental
- Ludovico Einaudi piano
- Max Richter ambient
- Trending cinematic Instagram audios

**Quand l'utiliser** : monument historique, fête nationale, paysage grandiose, fin de voyage récap.

### 3. Upbeat / trending
Pour F3 court avec hook punchy, ou pour surfer une tendance Instagram/TikTok du moment.

**Références** :
- Audio trending Instagram (chercher dans la lib audio à la création)
- Pop instrumental upbeat
- Electronic chill avec drop léger
- Afrobeat / arabic pop fusion (à explorer pour matcher l'identité tunisienne)

**Quand l'utiliser** : transitions rapides, plusieurs lieux dans un reel, énergie de découverte.

### 4. Quiet / no music (ambient natural)
Parfois la meilleure musique = pas de musique. Laisser le son ambiant du lieu (vent, foule, voix, mer).

**Quand l'utiliser** :
- F1 facecam où la voix de Karim porte tout
- Audio d'origine du lieu = signature (marché, port, foule de festival)
- Quand la musique distrait du moment vécu

**Format retour** :
```
Mood : null / audio d'origine
Note : laisser le son ambiant porter, pas de musique ajoutée
```

---

## Mapping mood → format vidéo

| Format | Moods recommandés |
|---|---|
| F1 spontané facecam | chill OU no music (audio d'origine) |
| F2 voix off + b-rolls | cinematic emotional OU chill |
| F3 b-rolls + hook + musique | upbeat trending OU cinematic emotional |

---

## Cas particuliers

### Sujet historique / heritage
→ **cinematic emotional** (Dean Valentine type), ou pas de musique si la voix off est dense en info.

### Sujet nocturne / city at night
→ **chill** (lo-fi) ou **cinematic emotional** doux.

### Sujet identitaire tunisien
→ Considérer **musique arabe instrumentale moderne** (oud chill, arabic lo-fi).

### Festival / événement public
→ **No music**, garder l'audio d'origine du lieu (foule, fanfare, célébration).

---

## Anti-patterns musique

- ❌ Musique avec paroles fortes qui dominent la voix off
- ❌ Drop EDM agressif sur vlog discovery chill
- ❌ Musique cliché "voyage Instagram générique"
- ❌ Track trop populaire/saturée qui banalise le contenu
- ❌ Volume musique > volume voix off (toujours mixer la musique en dessous)
- ❌ Changer de musique 3 fois dans un reel de 30s

---

## Sortie type de l'agent

```
Mood : cinematic emotional
Énergie : mid
Références : Dean Valentine — Vladimir's Theme (déjà utilisé), Joe Hisaishi instrumental
Alternative : Max Richter ambient
Note : sujet historique/officiel → cinematic > chill ; voix off arabe littéraire compatible.
```

ou

```
Mood : null (audio d'origine)
Note : marché de rue / foule, garder le son ambiant qui porte l'authenticité du lieu.
```
