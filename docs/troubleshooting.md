# Troubleshooting

## Where the log file is

VocalCode writes a log next to its own data:

- **Windows** — `%LOCALAPPDATA%\Programs\VocalCode\vocalcode.log`
- **macOS** — `~/Library/Application Support/VocalCode/vocalcode.log`

It rotates once at startup when it passes 2 MB, so if you are reproducing a
problem, restart the app first and the log will be short.

**The log does not contain what you said.** It records events — model loaded,
key pressed, text injected, error X — never the recognized text. Attaching it to
an issue does not leak your dictation.

## Nothing happens when I hold the key

1. Open the settings window and check the status line. It should say the engine is
   ready. If it is still loading a model, wait — the first run downloads one.
2. Re-record the trigger. Use the **Record** button rather than typing a key name.
3. **macOS only:** check System Settings → Privacy & Security → **Input Monitoring**
   and **Accessibility**. VocalCode needs both, and macOS silently does nothing
   rather than telling you when one is missing. If VocalCode is already listed,
   toggle it off and on — permission entries go stale after an update.
4. Make sure only one copy is running. A second instance cannot take the global key
   hook the first one holds.

## Text is recognized but not typed anywhere

Usually the trial expired. When it does, VocalCode still recognizes speech and shows
it, but stops inserting, with a note saying so. Activate a license to restore it.

If it is not that, the target application may be running elevated on Windows while
VocalCode is not — a non-elevated process cannot send input to an elevated window.
Run both at the same level.

## The first run is downloading forever

Models are downloaded on demand rather than bundled, so the installer stays small.
If the download stalls, it is almost always the network path to the model host.
Restart the app to resume; report an issue if it will not complete and include the
log.

## A word comes out wrong every single time

Use the replacement dictionary — `heard => desired`, one per line, next to the
application. Case-insensitive, `#` for comments, re-read live. It exists exactly
for project names and jargon that no general model has been trained on.

If instead a word is wrong *sometimes*, that is recognition accuracy, and the
dictionary is the wrong tool — file an issue with the phrase.

## Punctuation is wrong

Punctuation is added by a separate model that runs on the recognized text. If the
recognition was garbled, the punctuation will be too — garbage in, odd punctuation
out. Before filing that as a punctuation bug, check whether the *words* were right.

## The one-click update did nothing

The updater is deliberately fail-closed: it verifies the published hash **and** the
installer's Authenticode signature, and if either check does not pass it silently
falls back to opening the download page instead of running anything. So "clicked
update, browser opened" means a check failed. Download and run the installer
manually — that is safe — and file an issue with the log so the failing check can
be found.

## Filing a useful issue

Include:

- OS and version
- VocalCode version (settings window)
- What you expected and what happened
- The relevant lines from the log

[Open an issue](../../../issues)
