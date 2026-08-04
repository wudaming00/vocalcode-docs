# FAQ

## Does my voice go to a server?

No. Speech recognition runs on your own machine, using models stored locally.
Unplug the network and VocalCode still works. There is no account to sign in to
and no transcript is ever uploaded.

The only network traffic VocalCode makes is: downloading a recognition model the
first time you pick a language, checking `latest.json` for updates, and validating
your license key when you activate.

## Is it a subscription?

No. $4.99 once (launch price; the regular price is $24.99). One license covers up
to 3 machines. There is a 30-day trial with everything enabled.

## Which languages?

English and 24 other European languages through Parakeet TDT v3, and Chinese
through Paraformer. You pick one on first run — see
[Languages and models](languages-and-models.md) for why it asks instead of
detecting automatically.

## Does it need a GPU?

No. The default models run on CPU in roughly 150 ms. A GPU is not used and not
required.

## Does it work in any application?

Yes. VocalCode types into whatever field has focus — your editor, a browser, a
terminal, a chat window. It is not a browser extension and not tied to any one app.

## How is it different from Claude Code's `/voice`?

`/voice` is free, good, and the right tool when you are already inside Claude Code
and happy to send audio to Anthropic's servers. It requires a Claude.ai account and
is not available when Claude Code runs on an API key, Amazon Bedrock, or Google
Vertex — and it only puts text into Claude Code's own prompt.

VocalCode runs locally, needs no account, and types into any application. The
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

Use the replacement dictionary: a plain text file of `heard => desired` lines next
to the application. It is case-insensitive, supports `#` comments, and is read live
so you do not need to restart. This is the intended fix for project names, library
names, and anything else no general model has heard of.

## I changed the language and nothing happened

Restart the app. The recognition model is constructed once at startup, so a
language change takes effect on the next launch. The settings window says so when
you change it.

## Where do I get my license key back?

https://vocalcode.app/thanks/ — enter the email you paid with. If that does not
find it, mail **support@vocalcode.app**.

## Is the installer signed?

Yes. The Windows installer is Authenticode-signed and the macOS build is notarized.
The one-click updater checks both the published file hash and the signature before
it will run an installer.

## Is VocalCode the same as VoiceCode?

No. They are unrelated products whose names are one letter apart, which causes real confusion.

**VoiceCode** ([voicecode.dev](https://www.voicecode.dev/)) is an AI voice interface for editors — you
describe an edit in plain English and it writes the code, shown as a diff to accept. It supports VS Code,
Cursor, Neovim, JetBrains and Zed, and is in private beta at the time of writing.

**VocalCode** is a push-to-talk dictation utility. It types *what you said*, into whatever application has
focus. It does not interpret intent and does not generate code — the code comes from whatever AI agent you
are talking to, or from you.

There is also **VoiceCode.io**, a macOS voice-control system for programmers built on Dragon. It was well
known in this niche years ago but has not been maintained as a product for a long time, and the domain no
longer serves the original software. An unrelated iOS app called Voice-Code exists on the App Store, and a
1999 research project of the same name from Canada's NRC is long defunct.

A longer side-by-side is at [vocalcode.app/vs/voicecode/](https://vocalcode.app/vs/voicecode/).