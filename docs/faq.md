# FAQ

## Does my voice go to a server?

Speech recognition runs on your own machine, and recognition audio or transcripts
are not uploaded. After the selected model downloads, recognition works without a
network connection.

Other functions do connect: initial trial setup sends a stable pseudonymous device
fingerprint and receives a signed device-bound receipt; model and update downloads;
manual activation with a licence key and the same fingerprint; checkout polling with
that fingerprint; and periodic validation of a paid licence before its 30-day signed
receipt expires. None of those requests includes recognition audio or transcripts.
Explicitly copying a History entry or enabling optional Paste text does use the
system clipboard; clipboard-history or sync tools may retain that text even after
VocalCode restores the previous clipboard.
See the [privacy notice](https://vocalcode.app/privacy/) for the complete data flow.

## Is it a subscription?

No. The launch price is $4.99 once, plus applicable tax, with no recurring fee.
One licence covers up to 3 devices. A paid licence periodically revalidates online,
and updates within the current major version are included. There is a 30-day trial
with everything enabled. Starting it requires one online request; its signed receipt
is then checked offline.

## Which languages?

English and 24 other European languages through Parakeet TDT v3, and Chinese
through Paraformer. You pick one on first run — see
[Languages and models](languages-and-models.md) for why it asks instead of
detecting automatically.

## Does it need a GPU?

No. The shipped recognition paths run on CPU; a GPU is not used or required.
Responsiveness varies with hardware, audio length, language and model. VocalCode
does not currently publish a quantitative latency promise.

## Does it work in every application?

No system-wide injector works in every field. VocalCode types into the active text
field in most desktop apps and is not tied to one editor. Windows cannot inject
into a process running with higher administrator privileges. Password/secure
fields, browser-rendered controls and some apps may reject synthetic input or
prevent reliable target identification. macOS also requires Accessibility and Input
Monitoring permission.

## How is it different from Claude Code's `/voice`?

`/voice` is included for supported Claude.ai accounts and does not consume messages
or tokens. It is the direct choice when you are already inside Claude Code and are
comfortable with cloud audio processing. It is unavailable when Claude Code runs
on an API key, Amazon Bedrock, Google Cloud's Agent Platform or Microsoft Foundry,
and it only puts text into Claude Code inputs.

VocalCode recognition runs locally, needs no app account, and types into most
desktop applications subject to the limitations above. The
[full comparison](https://vocalcode.app/vs/claude-code-voice/) cites Anthropic's own
documentation for every claim it makes about `/voice`.

## Can I use a key combination like Ctrl+Shift?

Not yet. The trigger is currently a single key or mouse button. The reason is that
VocalCode *consumes* the bound input globally so it does not also trigger whatever
that key normally does — and doing that correctly for modifier combinations,
including AltGr, is a different problem than it looks. It is on the list.

## The key I bound stopped doing its normal thing

That is intended. If you bind mouse button X2, it no longer does browser-Forward
anywhere. Pick a key you do not otherwise use — the side mouse buttons, CapsLock,
or an F-key are the usual choices. Rebinding releases the old key.

## It typed a technical term wrong

Use the replacement dictionary in Settings: `heard => desired`, one rule per line.
It is stored in VocalCode's per-user data directory, is case-insensitive, supports
`#` comments, and applies Settings changes to the next utterance. If you edit the
plain-text file directly, reopen VocalCode so the running engine reloads it. This
is intended for project names, library names and other domain-specific terms.

## I changed the language and nothing happened

Give the app time to download and load the newly selected model. Language changes
are applied while VocalCode is running; a restart is not required. If the status
reports an error, check the model-download troubleshooting steps and log.

## Where do I get my license key back?

https://vocalcode.app/thanks/ — enter the email you paid with. For privacy, the
page gives the same response whether or not an address exists; if a matching
purchase exists, the key is mailed to that address. If no message arrives, contact
**support@vocalcode.app**.

## Is the installer signed?

Yes. The Windows installer is Authenticode-signed and the macOS build is notarized.
The one-click updater checks both the published file hash and the signature before
it will run an installer.

## Is VocalCode the same as VoiceCode?

No. They are unrelated products whose names are one letter apart, which causes real confusion.

**VoiceCode** ([voicecode.dev](https://www.voicecode.dev/)) is an AI voice interface for editors — you
describe an edit in plain English and it writes the code, shown as a diff to accept. It supports VS Code,
Cursor, Neovim, JetBrains and Zed, and is in private beta at the time of writing.

**VocalCode** is a push-to-talk dictation utility. It types *what you said* into the active field in most
desktop apps. It does not interpret intent or generate code — the code comes from your AI agent or from you.
It does not automatically read or index a project; the optional Teach command reads only text you explicitly
select and stores the resulting replacement rule locally.

A longer side-by-side is at [vocalcode.app/vs/voicecode/](https://vocalcode.app/vs/voicecode/).
