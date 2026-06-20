# Fine-tuning de Whisper pour la reconnaissance vocale en wolof

Projet réalisé dans le cadre du cours *Deep Learning* (2025–2026), École
Polytechnique de Thiès.

**Auteure :** Aissatou Sow
**Supervision :** Ndeye Fatou Ngom

## Contexte

[Whisper](https://arxiv.org/abs/2212.04356) (Radford et al., OpenAI 2022)
atteint une robustesse remarquable en reconnaissance vocale zero-shot,
mais ne couvre aucune des langues africaines à faibles ressources comme
le wolof, absent des 99 langues de son pré-entraînement. Ce projet
fine-tune `whisper-small` sur un corpus audio wolof afin de combler
partiellement ce manque, et évalue le gain de performance obtenu.

## Résultats

Fine-tuning de `openai/whisper-small` sur
[`galsenai/wolof-audio-data`](https://huggingface.co/datasets/galsenai/wolof-audio-data)
(23 045 exemples d'entraînement, 500 pas, point de contrôle retenu : 300) :

| Métrique | Zero-shot | Fine-tuné | Amélioration |
|---|---|---|---|
| WER | 189,01 % | 84,56 % | −55,3 % (relatif) |
| CER | 166,43 % | 40,34 % | −75,8 % (relatif) |
| BLEU | 0,16 % | 14,33 % | +14,17 pts |
| F1 (token) | 3,32 % | 38,93 % | +35,61 pts |

Détails complets, méthodologie, analyse critique de l'article de
référence et limites méthodologiques : voir le rapport (PDF).

## Contenu du dépôt

- `whisper_finetuning_train.ipynb` — préparation des données, fine-tuning
  (0 → 300 pas)
- `whisper_wolof_finetuning_eval.ipynb` — reprise de l'entraînement
  (300 → 500 pas), évaluation zero-shot vs fine-tuné, analyse d'erreurs,
  démo Gradio
- `rapport_whisper_wolof.pdf` — rapport complet

## Modèle et données

- Modèle de base : [`openai/whisper-small`](https://huggingface.co/openai/whisper-small)
- Données : [`galsenai/wolof-audio-data`](https://huggingface.co/datasets/galsenai/wolof-audio-data)
- Le modèle fine-tuné n'est pas hébergé dans ce dépôt (poids ≈ 1 Go) ;
  voir les notebooks pour reproduire l'entraînement.
