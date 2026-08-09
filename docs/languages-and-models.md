# Languages and models

## What ships

| Language group | Model | Notes |
|---|---|---|
| English + 24 other European languages | **Parakeet TDT v3** (NVIDIA, via sherpa-onnx) | CPU recognition; no Chinese. Emits its own punctuation. |
| Chinese | **Paraformer** | Bilingual zh/en, simplified output. |
| Paraformer path only | **CT-Transformer punctuation** | Restores punctuation after Paraformer recognition. |

Models are **not** bundled in the installer. You pick a language on first run and
the matching model downloads then. That keeps the download small and means you do
not carry a Chinese model you will never open.

## Why it asks instead of detecting the language

Per-utterance automatic routing was built, shipped, and then **deliberately
removed**.

The idea was reasonable: look at the audio, decide whether it is Chinese, send it to
the right engine. In practice one person saying similar things would land on either
side of the threshold, and the engine would switch between utterances. Sometimes it
picked wrong and produced confident nonsense — Parakeet, given Chinese audio, does
not return nothing, it returns plausible English.

Silent routing errors are harder to notice than an explicit choice. VocalCode asks
once and, if the saved setting is missing or unrecognized, asks again rather than
guessing.

Changing the language later downloads (if necessary) and loads the selected model
while VocalCode is running; a restart is not required.

## Why not one big multilingual model

The release deliberately has two audited model paths rather than promising that one
model performs equally across all languages. The shipped runtime is CPU-only. We do
not currently publish quantitative accuracy or latency comparisons; the
[measurement policy](https://vocalcode.app/benchmark/) lists the evidence required
before such a claim can be published.

## Languages that were built and then withdrawn

Japanese, Korean, Thai, Vietnamese, Russian and Cantonese are not offered by this
release. Old or unknown model identifiers fail before download, and their dormant
objects are not served from the model CDN.

Model inclusion requires documented provenance, integrity hashes, a licence that
permits commercial redistribution, and an evaluation suitable for the claimed
scope. A model is excluded when any of those conditions is missing; adding a
download route is not enough.

## Where models come from

Models are served from VocalCode's own storage rather than hot-linked at runtime.
The registry pins the expected size and SHA-256 for every offered object and rejects
a mismatched download before use.

- **Parakeet TDT v3:** derived from
  [`nvidia/parakeet-tdt-0.6b-v3`](https://huggingface.co/nvidia/parakeet-tdt-0.6b-v3)
  (CC BY 4.0) through the pinned sherpa-onnx conversion identified in the release
  notices.
- **Paraformer:** the pinned sherpa-onnx conversion of
  [`iic/speech_paraformer-large-vad-punc_asr_nat-zh-cn-16k-common-vocab8404-onnx`](https://www.modelscope.cn/models/iic/speech_paraformer-large-vad-punc_asr_nat-zh-cn-16k-common-vocab8404-onnx)
  (Apache 2.0).
- **CT-Transformer punctuation:** the pinned sherpa-onnx conversion used only by
  the Paraformer path (Apache 2.0).

Exact revisions, hashes, attribution and licence texts ship with the application in
`THIRD-PARTY-NOTICES.txt` and `THIRD-PARTY-LICENSES`.
