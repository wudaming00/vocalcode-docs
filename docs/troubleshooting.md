# Troubleshooting

## Where the log file is

VocalCode writes a log next to its own data:

- **Windows** — `%LOCALAPPDATA%\VocalCode\vocalcode.log`
- **macOS** — `~/Library/Application Support/VocalCode/vocalcode.log`

The active log and one previous generation are each capped at 2 MiB. Rotation is
checked on every write, so a process left running for weeks cannot grow the logs
without bound.

The log is designed not to record recognized text. It can contain errors, local
paths, usernames or hardware identifiers. Review the relevant lines before
attaching them to a public issue.

## Nothing happens when I hold the key

1. Open the settings window and check the status line. It should say the engine is
   ready. If it is still loading a model, wait — the first run downloads one.
2. Re-record the trigger. Use the **Record** button rather than typing a key name.
3. **macOS only:** check System Settings → Privacy & Security for **Microphone**,
   **Input Monitoring** and **Accessibility**. They cover audio, configured
   talk-control detection, focused-target checks and native text insertion.
   Follow the in-app status for the missing permission and restart VocalCode when
   macOS says the permission change requires it.
4. Make sure only one copy is running. A second instance cannot take the global key
   hook the first one holds.

## Text is recognized but not typed anywhere

First check the licence status. A fresh installation says **Connect once to start the
30-day trial** until it receives its signed device-bound trial receipt; connect once
and retry. If the signed trial has expired, recognition and insertion are blocked.
Activate a licence to restore them.

If it is not that, the target application may be running elevated on Windows while
VocalCode is not — a non-elevated process cannot send input to an elevated window.
Run both at the same integrity level. Password/secure fields and some applications
also reject synthetic input.

## The model download does not finish

Models are downloaded on demand rather than bundled, so the installer stays small.
If the download stalls, check the network path, available disk space and the error
shown in Settings. Restarting retries the download; partial bytes are never installed.
Report an issue if it still will not complete and include the relevant log lines.

## A word comes out wrong every single time

Use the replacement dictionary in Settings — `heard => desired`, one per line.
It is stored in the per-user VocalCode data directory, is case-insensitive, supports
`#` comments and blank lines. Settings changes apply to the next utterance; after
editing the file directly, reopen VocalCode so the running engine reloads it. It is
intended for project names and jargon.

If instead a word is wrong *sometimes*, that is recognition accuracy, and the
dictionary is the wrong tool — file an issue with the phrase.

## Punctuation is wrong

The Parakeet path emits its own punctuation. The Paraformer path runs a separate
local CT-Transformer punctuation model. If the words themselves are wrong, a
punctuation report will not isolate the recognition problem, so include both the
words and punctuation you expected when filing an issue.

## The one-click update did nothing

The updater is deliberately fail-closed: it verifies the manifest, full-file
SHA-256, publisher signature and internal version before installing. It reports a
download/start failure in Settings; when automatic verification is unavailable it
may open the download page instead of running a file. Download the installer only
from `https://vocalcode.app/` and file an issue with the relevant log lines so the
failed check can be identified.

## Filing a useful issue

Include:

- OS and version
- VocalCode version (settings window)
- What you expected and what happened
- The relevant lines from the log

[Open an issue](https://github.com/wudaming00/vocalcode-docs/issues)
