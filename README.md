# Muse_CS

Muse Character Scripting — a lean fork of Kilo_CS v0.3 (profebral-beep,
GPL-3.0, credit and licence kept). Same idea, same workspace shape, rewritten
to Muse's specs: fewer rules, every rule checkable, nothing hidden.

## For humans

Copy these folders somewhere your bot can reach — a synced folder works.
Tell your bot: "Read `__init__/__init__.md` and start Muse."
Say "stop Muse" to deload it. Say "mood check" any time to see its state.

Before you grant shell access, read `__init__/muse_cs/desk.md`.
It is the only module that can touch a real machine, and it ships with no
shell grant — you turn that on yourself in `__init__.md`, or you don't.

## Layout

```
/__init__   the system (logic, grants, muse_cs modules)
 /CORE      add-ons, loaded only if named in core.md's allowlist
 /JOBS      jobs and projects
 /NOTES     shared logging and state
 /MISSED    personal trash (moving a file here counts as edit)
```

Flash Cards is the one add-on included. Inkarnate was dropped — it belonged
to a specific desktop. The card images are not in this repo: they are
byte-identical to Kilo_CS's, so pull them from
https://github.com/profebral-beep/Kilo_CS (CORE/Flash Cards) into the same
folders the deck manifests name. AI-generated (Grok Imagine), C2PA intact.
