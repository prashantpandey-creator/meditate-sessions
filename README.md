# meditate

**One long Claude Code session becomes a 100 MB tangle of unrelated work.
`meditate` reads it without loading it, finds the separate threads inside,
and hands you a paste-able prompt to resume any one of them.**

```sh
curl -fsSL https://raw.githubusercontent.com/prashantpandey-creator/meditate-sessions/main/get.sh | sh
```

Then:

```sh
meditate sessions
```

```
329 sessions across 17 projects

  sprawl   126  117.1MB    83u  ch:0   [vedic-puran]  Game work elements resume
  sprawl    90   39.3MB   296u  ch:12  [vedic-puran]  chart engine + pricing
  sprawl    78   29.2MB   238u  ch:12  [vedic-puran]  reader latency
```

Sprawl is how many distinct threads are tangled in one session. The top row
is the one you keep scrolling through to find where you were.

## The commands

| | |
|---|---|
| `meditate sessions` | every session, ranked by how tangled it is |
| `meditate split <id>` | one session, broken into its threads |
| `meditate threads` | what is still open across everything you split |
| `meditate open` | a Terminal per live thread, cd'd and prompted (macOS) |
| `meditate archive` | what's finished and can be set down (dry run) |
| `meditate repo` | the optional repo lens |
| `meditate test` | run the suite |

## How it reads a 100 MB transcript

By streaming it. A transcript never enters a context window — there is no
model call anywhere in this tool, and no network call at all. Each session
comes back as a capped record: title, sprawl, where the topic changed, the
human intents with tool noise stripped, and the files it touched.

That is also why it is fast and why it costs nothing to run.

## What it will not do

It never moves, renames or deletes a transcript or a project file. Every
delete site in the source is enumerated in `test_product.py` and a new one
fails the suite. It writes to two places: your project's memory directory
and `~/.meditation/`. `archive` is a dry run unless you pass `--apply`, and
archiving is reversible.

`install.sh` links one command and installs one skill. No background
service, no launch agent, no permissions requested. `uninstall.sh` undoes
exactly that and leaves your readings alone.

## Verify it yourself before you trust it

```sh
meditate test
```

6 modules, 2105 lines, no dependency outside the Python standard
library. Python 3.9+, macOS and Linux. Every module is checked to import
with nothing else on the path, and the suite ships with the code.

## Licence

MIT. Use it, fork it, ship it inside your own thing, at work or at home.
The repo is public so it can be found and shared; that is the point of it.
