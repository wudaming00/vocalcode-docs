# VocalCode

**Push-to-talk voice input for coding with AI.** Hold a key, talk, release — clean
text lands wherever your cursor already is. Recognition runs on your own machine,
in about 150 ms. Windows and macOS. One-time purchase, no subscription, no account.

**[vocalcode.app](https://vocalcode.app/)** · [Download for Windows](https://vocalcode.app/VocalCodeSetup.exe) · [Download for macOS](https://vocalcode.app/VocalCode-0.5.0.dmg)

This is the public home for VocalCode's documentation and issue tracker. The
application itself is closed-source; everything here is docs, answers, and a place
to file bugs.

---

## What it actually does

You are typing a prompt to Claude Code, Cursor, Codex — some agent that wants
paragraphs, not keywords. Typing paragraphs is slow. So:

1. **Hold** your bound key or mouse button.
2. **Talk.**
3. **Release.** The transcribed text is typed into the focused field, punctuated.

A second binding sends it. That is the whole product. It is not a note-taking app,
not a meeting transcriber, and not a general voice assistant.

## Why not just use the free things

There are good free options, and for some jobs they are the right answer. The
honest version:

| | Where it runs | Works in any app | Cost |
|---|---|---|---|
| **Claude Code `/voice`** | Anthropic's servers | No — only in Claude Code | Free, needs a Claude.ai account |
| **Windows Voice Typing** | Microsoft's servers | Mostly | Free |
| **Wispr Flow** | Cloud | Yes | Subscription |
| **Superwhisper** | On device | Yes | Free tier; the better models are Pro |
| **VocalCode** | On device | Yes | $4.99 once |

Longer, sourced versions of each comparison — written by us, citing the other
product's own documentation:

- [vs Claude Code's built-in `/voice`](https://vocalcode.app/vs/claude-code-voice/)
- [vs Wispr Flow](https://vocalcode.app/vs/wispr-flow/)
- [vs Handy](https://vocalcode.app/vs/handy/)
- [vs VoiceCode](https://vocalcode.app/vs/voicecode/) — different tool, near-identical name
- [A Superwhisper alternative for Windows](https://vocalcode.app/superwhisper-alternative-windows/)

And the numbers behind the accuracy claims, with the method and the cases we lose:
[vocalcode.app/benchmark](https://vocalcode.app/benchmark/).

## Facts

| | |
|---|---|
| **Platforms** | Windows 10, Windows 11, macOS 11 or later |
| **Current version** | 0.5.0 |
| **Price** | $4.99 one-time (launch price; regular $24.99) |
| **Trial** | 30 days, full functionality |
| **Recognition** | Entirely on your machine. No audio leaves it. Works with no network. |
| **Latency** | ~150 ms from key release to text, on CPU. No GPU required. |
| **Languages** | English and 24 other European languages; Chinese |
| **Models** | Parakeet TDT v3 (English/European), Paraformer (Chinese) |
| **Installer size** | Small — models download on first run rather than shipping in the installer |
| **Signing** | Windows installer is Authenticode-signed; macOS build is notarized |
| **Licensing** | One license, up to 3 machines |

### What it does to the text

Raw speech recognition output is not what you want in a prompt. Three passes run
before anything is typed:

- **Acronym collapsing** — "m c p" becomes `MCP`, "a p i" becomes `API`.
- **Punctuation restoration** — a separate model adds commas, periods and question
  marks. Full-width punctuation for Chinese, ASCII for English, including in mixed
  text.
- **Your replacement dictionary** — a plain text file of `heard => desired` lines
  for the terms your project uses that no general model will ever get right. Edit
  it while the app is running.

## Install

**Windows** — download [VocalCodeSetup.exe](https://vocalcode.app/VocalCodeSetup.exe)
and run it. Per-user install, no admin required. On first launch you pick a
language, and the matching model downloads.

**Windows, with [Scoop](https://scoop.sh/)** — the package is not in the Extras
bucket (its maintainers judged it too new to meet their inclusion criteria), so it
lives in a bucket here:

```
scoop bucket add vocalcode https://github.com/wudaming00/vocalcode-docs
scoop install vocalcode
```

Scoop unpacks the installer rather than running it, and `scoop update vocalcode`
follows the same `latest.json` the app's own updater does.

**macOS** — download [the .dmg](https://vocalcode.app/VocalCode-0.5.0.dmg), drag to
Applications. macOS will ask for **Accessibility** and **Input Monitoring**
permission — both are required: the first lets VocalCode type into other apps, the
second lets it see your push-to-talk key.

Updates are checked against [latest.json](https://vocalcode.app/latest.json). On
Windows, the one-click updater verifies both the file hash and the installer's
Authenticode signature before running anything.

## Documentation

- [FAQ](docs/faq.md)
- [Troubleshooting](docs/troubleshooting.md) — including where the log file lives
- [Languages and models](docs/languages-and-models.md)

## Reporting a bug

[Open an issue](../../issues). Useful reports include your OS, the VocalCode
version, and the relevant part of the log file — see
[Troubleshooting](docs/troubleshooting.md) for where to find it.

**The log never contains what you said.** It records events, not transcripts. That
is deliberate: "what you say stays on the machine" is the whole pitch, and a log
full of dictated text would quietly break it.

## Contact

- Issues and feature requests: [this repository's issues](../../issues)
- Purchases, licenses, refunds: **support@vocalcode.app**
- Lost your license key: [recover it here](https://vocalcode.app/thanks/)
