# Languages and models

## What ships

| Language group | Model | Notes |
|---|---|---|
| English + 24 other European languages | **Parakeet TDT v3** (NVIDIA, via sherpa-onnx) | Fast on CPU. No Chinese. |
| Chinese | **Paraformer** | Bilingual zh/en, simplified output. |
| — | **CT-Transformer punctuation** | Runs on the recognized text, both language groups. |

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

An engine that is right 95% of the time and silently wrong the rest is worse than
one that asks a question once. So it asks once, and if the setting is missing or
unrecognized it asks again rather than guessing.

Changing the language later takes effect on the next launch, because the recognition
model is constructed once at startup.

## Why not one big multilingual model

Whisper large-v3 is excellent and was tried. On CPU without CUDA it is unusably
slow, and the prebuilt runtime we ship has no CUDA path. Whisper base is fast but
drops content in Chinese. So the current pair — a fast European model and a fast
Chinese model — beats one general model at the sizes that actually run on a laptop.

## Languages that were built and then withdrawn

Japanese, Korean, Thai, Vietnamese, Russian and Cantonese were wired up and then
pulled before release. The Japanese model returned only the content after the final
pause — say two sentences, lose the first — which is a structural problem with how
that model segments, not a tuning knob.

The rule applied: **no language ships until a native speaker has verified it.** A
language that half-works is worse than one that is absent, because the person who
needs it has already paid by the time they find out.

Some models were also excluded on licensing grounds rather than quality. A model
under a bespoke, non-Apache/MIT license is not usable in a paid product regardless
of how well it performs.

## Where models come from

Models are served from VocalCode's own storage rather than hot-linked from a
third-party host, so a model that works today keeps working. The registry has a test
asserting that every model URL points at our own domain — an upstream host quietly
returning 401 has broken this kind of thing before.
