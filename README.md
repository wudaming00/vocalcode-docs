# VocalCode

[![Latest release](https://img.shields.io/github/v/release/wudaming00/vocalcode-docs?label=release)](https://github.com/wudaming00/vocalcode-docs/releases/latest)
[![Windows 10/11](https://img.shields.io/badge/Windows-10%20%7C%2011-0078D4?logo=windows)](https://vocalcode.app/VocalCodeSetup.exe)
[![Apple silicon](https://img.shields.io/badge/macOS-Apple%20silicon-111111?logo=apple)](https://vocalcode.app/VocalCode-1.0.0.dmg)
[![On-device recognition](https://img.shields.io/badge/speech-on--device-FF974D)](https://vocalcode.app/privacy/)
[![Approved on SaaSHub](https://cdn-b.saashub.com/img/badges/approved-color.png?v=1)](https://www.saashub.com/vocalcode?utm_source=badge&utm_campaign=badge&utm_content=vocalcode&badge_variant=color&badge_kind=approved)

**Push-to-talk voice input for coding with AI.** Hold a key, talk, release — clean
text lands in the active field in most desktop apps. Recognition runs on your own
machine after the selected model downloads. Windows 10/11 (64-bit) and macOS 11+
on Apple silicon. $4.99 once, plus applicable tax; no subscription or app account.

**[vocalcode.app](https://vocalcode.app/)** · [Download for Windows](https://vocalcode.app/VocalCodeSetup.exe) · [Download for macOS](https://vocalcode.app/VocalCode-1.0.0.dmg)

![VocalCode — push-to-talk voice input for AI coding](https://vocalcode.app/og.png)

This is the public home for VocalCode's documentation and issue tracker. The
application itself is closed-source; everything here is docs, answers, and a place
to file bugs.

---

## What it actually does

You are typing a prompt to Claude Code, Cursor, Codex — some agent that wants
paragraphs, not keywords. Typing paragraphs is slow. So:

1. **Hold** your bound key or mouse button.
2. **Talk.**
3. **Release.** The transcribed text is cleaned and typed into the active field.

A second binding sends it. That is the whole product. It is not a note-taking app,
not a meeting transcriber, and not a general voice assistant.

Text insertion works in most desktop apps, not literally every field. Windows
cannot inject into a process running with higher administrator privileges;
password/secure fields and some apps may reject synthetic input. macOS requires
the permissions listed under Install below.

## Other options

Free and broader products may be a better fit. These VocalCode-written comparison
pages link to each product's current documentation and distinguish model notes
from product tests:

- [vs Claude Code's built-in `/voice`](https://vocalcode.app/vs/claude-code-voice/)
- [vs Wispr Flow](https://vocalcode.app/vs/wispr-flow/)
- [vs Handy](https://vocalcode.app/vs/handy/)
- [vs VoiceCode](https://vocalcode.app/vs/voicecode/) — different tool, near-identical name
- [A Superwhisper alternative for Windows](https://vocalcode.app/superwhisper-alternative-windows/)

VocalCode currently publishes a
[measurement policy and model notes](https://vocalcode.app/benchmark/), not a
quantitative accuracy, latency or competitor scorecard.

## Facts

| | |
|---|---|
| **Platforms** | Windows 10/11 (64-bit); macOS 11+ on Apple silicon (arm64) |
| **Current version** | 1.0.0 |
| **Price** | $4.99 one-time launch price, plus applicable tax; no subscription |
| **Trial** | 30 days, full functionality. Initial setup needs one online request with a stable pseudonymous device fingerprint; the signed receipt is then checked offline. |
| **Recognition** | On your machine; no recognition audio or transcript is uploaded. Works offline after model download. |
| **Network** | Initial trial setup, model/update downloads, checkout, activation and periodic paid-licence validation use the internet. |
| **Clipboard** | Optional Paste text and explicit History copies use the system clipboard. Clipboard history or sync tools may retain transcript text even after VocalCode restores the previous clipboard. |
| **Languages** | English and 24 other European languages; Chinese |
| **Models** | Parakeet TDT v3 (English/European), Paraformer (Chinese/English) |
| **Installer size** | Small — models download on first run rather than shipping in the installer |
| **Signing** | Windows installer is Authenticode-signed; macOS build is notarized |
| **Licensing** | One payment, up to 3 devices; a paid licence revalidates online before its 30-day signed receipt expires |

### What it does to the text

Before text is inserted:

- **Acronym collapsing** — "m c p" becomes `MCP`, "a p i" becomes `API`.
- **Punctuation** — Parakeet emits its own punctuation. The Paraformer path runs a
  local CT-Transformer punctuation model after recognition.
- **Your replacement dictionary** — `heard => desired` rules for project-specific
  terms. Changes saved in Settings apply to the next utterance. If you edit the
  plain-text file directly, reopen VocalCode so the running engine reloads it.

## Install

**Windows** — download [VocalCodeSetup.exe](https://vocalcode.app/VocalCodeSetup.exe)
and run it. Setup stays per-user and does not request administrator elevation. It
ships the reviewed Microsoft Visual C++ runtime beside VocalCode and installs the
signed WebView2 runtime per-user when it is absent. On first launch you pick a
language, and the matching model downloads.

**Windows, with [Scoop](https://scoop.sh/):** VocalCode is currently distributed
through this repository's own bucket while the app is too new for Scoop Extras:

```powershell
scoop bucket add vocalcode https://github.com/wudaming00/vocalcode-docs
scoop install vocalcode
```

The manifest follows the signed, versioned installer published for 1.0.0. The
official installer above remains the simplest path on a clean Windows machine
because it can install Microsoft's WebView2 Runtime when Windows does not have it.

**macOS** — download [the Apple-silicon .dmg](https://vocalcode.app/VocalCode-1.0.0.dmg)
and drag it to Applications. VocalCode requests **Microphone**, **Accessibility**
and **Input Monitoring**. They provide audio capture, configured talk-control
detection, focused-target checks and local insertion through native macOS input events.

Updates are checked against [latest.json](https://vocalcode.app/latest.json). On
Windows, the one-click updater verifies both the file hash and the installer's
Authenticode signature before running anything.

## Documentation

- [FAQ](docs/faq.md)
- [Troubleshooting](docs/troubleshooting.md) — including where the log file lives
- [Languages and models](docs/languages-and-models.md)
- [Press and directory kit](docs/press-kit.md) — reviewed descriptions, product facts and media links

## Reporting a bug

[Open an issue](https://github.com/wudaming00/vocalcode-docs/issues). Useful reports include your OS, the VocalCode
version, and the relevant part of the log file — see
[Troubleshooting](docs/troubleshooting.md) for where to find it.

The log is designed not to record recognized text. It can contain errors, local
paths, usernames or hardware identifiers, so review the relevant lines before
posting them publicly.

## Contact

- Issues and feature requests: [this repository's issues](https://github.com/wudaming00/vocalcode-docs/issues)
- Questions and launch feedback: [GitHub Discussions](https://github.com/wudaming00/vocalcode-docs/discussions)
- Purchases, licenses, refunds: **support@vocalcode.app**
- Lost your license key: [recover it here](https://vocalcode.app/thanks/)
