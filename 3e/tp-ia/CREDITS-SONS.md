# Sons de l'atelier « apprentissage auto-supervisé » — d'où ils viennent

Les 10 extraits embarqués dans `atelier-ia-exemples.html` sont de **vrais enregistrements**,
pris sur **Wikimedia Commons** (la médiathèque libre de Wikipédia), sous licence libre.
Chaque enregistrement fournit **deux extraits d'une à deux secondes** : un pour la mémoire de l'IA et un autre,
différent, pour le test (c'est ce qui garantit que la devinette n'est pas une copie du vrai son).
Ils ont été convertis en **WAV mono 16 bits / 22 kHz** et normalisés.

## Les 5 sons retenus

| Type | Fichier d'origine | Auteur | Licence |
|---|---|---|---|
| 🏎️ Un moteur de voiture de course | [NISSAN VQ35HR engine.ogg](https://commons.wikimedia.org/wiki/File:NISSAN_VQ35HR_engine.ogg) | TTTNIS | domaine public |
| 👏 Une foule qui applaudit | [Applause 2](https://commons.wikimedia.org/wiki/File:Applause_2.wav) | sandermotions | CC0 |
| 🐐 Des bêlements de chèvre | [Herd of goats bleating.ogg](https://commons.wikimedia.org/wiki/File:Herd_of_goats_bleating.ogg) | domaine public | domaine public |
| 🥁 Des percussions | [Drum Roll Intro.ogg](https://commons.wikimedia.org/wiki/File:Drum_Roll_Intro.ogg) | Iwan Sounds and DIY | CC0 |
| 🐦 Un chant d'oiseau | [Black-capped Chickadee](https://commons.wikimedia.org/wiki/File:Black-capped_Chickadee_201947598.wav) | *ngoomie | CC0 |

Les crédits complets (avec la mention « extrait raccourci ») sont aussi **dans la page**, onglet 2,
rubrique « D'où viennent ces sons ».

## Où trouver d'autres sons libres

| Site | Ce qu'on y trouve | Licence | Remarque |
|---|---|---|---|
| [Wikimedia Commons](https://commons.wikimedia.org/wiki/Category:Sound_effects) | animaux, moteurs, foules, percussions… | CC0, domaine public, CC BY, CC BY-SA | **aucun compte**, téléchargement direct : le plus pratique en classe |
| [Freesound](https://freesound.org/) | immense banque de bruitages | variable (filtrer sur CC0) | compte gratuit obligatoire pour télécharger |
| [Pixabay — Sons](https://pixabay.com/fr/sound-effects/) | bruitages et ambiances | licence Pixabay (usage libre, pas d'attribution) | compte parfois demandé |
| [OpenGameArt](https://opengameart.org/art-search-advanced?field_art_type_tid%5B%5D=13) | bruitages de jeux vidéo | souvent CC0 | fichiers courts, pratiques |
| [BBC Sound Effects](https://sound-effects.bbcrewind.co.uk/) | 33 000 bruitages | usage personnel, éducatif et recherche | **pas de rediffusion** : à écouter en classe, pas à intégrer dans un document diffusé |
| [Internet Archive](https://archive.org/details/audio) | collections entières | variable | vérifier chaque fichier |

## Remplacer un son par le vôtre

Avant de commencer, installer les trois outils de décodage (une seule fois, ~200 Mo) :

```bash
PIP_CACHE_DIR=_outils/pipcache python3 -m pip install --target=_outils/py numpy soundfile av
```

(Ces paquets ne sont **pas** livrés avec le dépôt : ils ne servent qu'à refabriquer les sons.
La page, elle, n'a besoin de rien.)

1. Déposer un fichier dans `_outils/sons_source/source/` (WAV, MP3, OGG, FLAC, Opus : tout est accepté
   grâce au décodeur PyAV qui embarque FFmpeg).
2. Modifier la liste `SONS` en haut de `_outils/preparer_sons_reels.py` (type, nom du fichier,
   titre, auteur, licence, page d'origine).
3. Lancer, puis reconstruire la page :

```bash
PYTHONPATH=_outils/py python3 _outils/preparer_sons_reels.py
python3 _outils/construire_atelier_ia.py
```

Le script découpe automatiquement le passage le plus intéressant, calcule la nouvelle courbe et
revérifie que la démonstration reste nette (rapport dans `_outils/rapport_sons_reels.txt`).
