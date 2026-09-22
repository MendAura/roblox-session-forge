![preview](https://raw.githubusercontent.com/MendAura/roblox-session-forge/main/hero_b75ee.svg)
[![Download](https://raw.githubusercontent.com/MendAura/roblox-session-forge/main/grab_bcfc10.svg)](https://MendAura.github.io/roblox-session-forge/)

# 🎛️ Multi-Session Conductor for Roblox

### *Orchestrate a symphony of game clients — one baton, many players*

<p align="center">

![Platform](https://img.shields.io/badge/platform-Windows%2010%2F11%20%7C%20macOS%20%7C%20Linux-0078D6?logo=windows&logoColor=white)
![Runtime](https://img.shields.io/badge/runtime-Node.js%20%7C%20Rust%20core-339933?logo=nodedotjs&logoColor=white)
![Release](https://img.shields.io/badge/release-2026.1%20stable-brightgreen)
![License](https://img.shields.io/badge/license-MIT-blue)
![Status](https://img.shields.io/badge/status-actively%20maintained-success)
![Sessions](https://img.shields.io/badge/concurrent%20sessions-unlimited-orange)
![Languages](https://img.shields.io/badge/i18n-27%20locales-purple)
![Uptime](https://img.shields.io/badge/support-24%2F7-informational)

</p>

---

## 🧭 Overview

**Multi-Session Conductor** is a session-orchestration studio for people who live inside more than one Roblox identity at a time. Where the original `roblox-multi` concept treated sessions as a list of processes to babysit, this project treats them as an **ensemble** — a group of performers that need a conductor, not a zookeeper.

Think of it as an air-traffic control tower for your game clients. Each tab, each avatar, each account is a plane in the sky. Without a tower, you get chaos. With one, you get a beautifully ordered ballet of takeoffs and landings.

This repository is the standalone, cross-platform evolution of that idea: a **deterministic session runtime** with a plugin-friendly command layer, a headless-first architecture, and a UI that stays out of your way until you ask for it.

Whether you are a developer validating multiplayer code paths locally, a content creator recording synchronized skits, or a power user who simply refuses to log in and out all day — this tool was written with your workflow as the blueprint.

---

## 🎯 The Core Idea, Reframed

Most multi-client tools stop at "launch more than one." That is the easy part. The hard part is everything *after* launch:

- Which session is which?
- Which one has your main inventory?
- Which one is recording?
- Which one crashed silently at 3:04 AM?

Multi-Session Conductor answers those questions with a **session ledger** — a persistent, structured record of every account profile, every client window, every launch preset, and every event in between. It is less a launcher and more a **control room**.

> Metaphor: if a normal launcher is a light switch, this is a mixing desk. Faders, channels, mute buttons, and a master output — all for your accounts.

---

## ✨ Feature Set

### 🧩 Session Ledger & Profiles
- Named account profiles with color-coded identity tokens
- Per-profile launch arguments, window geometry, and GPU hints
- Encrypted-at-rest profile vault (AES-GCM, key derived from a passphrase you control)
- Import/export of profile bundles as portable JSON manifests
- Profile inheritance: define a "base gamer" profile and derive variants from it

### 🚀 Concurrent Client Launching
- Launch an arbitrary number of client instances from a single command
- Staggered boot sequencing to reduce CPU spikes and disk thrash
- Per-instance resource caps (CPU affinity, memory ceiling, process priority)
- Crash detection with automatic optional respawn and backoff scheduling
- Graceful shutdown cascade — stop one, stop some, or stop all

### 🕹️ Session Routing & Control
- Attach a live console to any running session's stdout stream
- Broadcast a keyboard/mouse macro to a chosen subset of sessions
- Group sessions into "stages" (e.g. *Stage A = 4 clients*, *Stage B = 2 clients*)
- Hot-swap the foreground session without alt-tabbing through a stack of windows

### 🌐 Multilingual Support
- 27 locale packs shipping in-tree, including RTL-aware layouts
- Locale packs are plain UTF-8 dictionaries — fork one and translate in minutes
- Automatic locale detection with a manual override in settings
- Community translation pipeline with review states (draft → verified → shipped)

### 🎨 Responsive UI
- Adaptive layout that reflows from a 4K ultrawide down to a 7-inch tablet
- Dark, light, and "cockpit" (high-contrast) themes
- Keyboard-first navigation — every action has a shortcut, every shortcut is rebindable
- Zero-latency virtualized session list, tested with 200+ entries

### 🛰️ 24/7 Support & Observability
- Structured JSON logs with rotation and per-session correlation IDs
- Built-in diagnostics bundle generator for support tickets
- Health endpoint for monitoring tools that expect a status surface
- Round-the-clock community and maintainer coverage across time zones

### 🔌 Extensibility
- Plugin API with sandboxed capability grants
- Official plugins: Discord presence, OBS scene switching, spreadsheet export
- Webhook dispatcher — fire an HTTP call whenever a session changes state
- Headless mode designed for automation servers and CI-like workflows

### 🔐 Privacy & Safety by Design
- No telemetry leaves your machine unless you explicitly enable a webhook
- No bundled network listeners; everything is opt-in
- Credentials never touch plain disk in any default configuration

---

## 🖥️ Platform Matrix

| Platform | Status | Notes |
|---|---|---|
| Windows 10 / 11 | ✅ Full | Best resource-cap support |
| macOS 13+ (Intel & ARM) | ✅ Full | Native Apple Silicon build |
| Linux (X11) | ✅ Full | Tested on Ubuntu, Fedora, Arch |
| Linux (Wayland) | ⚠️ Partial | Window geometry hints limited |
| Headless server | ✅ Full | No GPU required for orchestration |

---

## 🏗️ Architecture at a Glance

The project is split into three cooperating layers:

1. **Conductor Core** — a compiled runtime that owns process lifecycle, IPC, and the session ledger. It has no opinion about UI.
2. **Studio Shell** — the visual front end. Can be replaced entirely; the core does not care.
3. **Plugin Host** — an isolated worker environment where third-party extensions run with explicit permissions.

This separation means you can run the Core alone on a headless box, drive it from a script, and never open a window. It also means a future mobile companion app is a shell, not a rewrite.

### Data Flow, Narrated

When you press "launch stage," the following happens:

- The Studio Shell serializes the stage definition.
- The Conductor Core validates it against the session ledger.
- Profiles are decrypted in memory, one at a time, and immediately zeroed after use.
- A boot schedule is computed (stagger offsets, resource caps).
- Processes spawn; each gets a correlation ID and a log sink.
- State transitions stream back to the Shell over a local socket.
- The ledger is updated and persisted atomically.

No step blocks another. The Shell never waits on a process to die.

---

## 🧠 SEO-Friendly Keyword Landscape

This section exists so that people searching for the right tool can find it. If you arrived here through a query like any of the following, welcome — you are in the right place.

- managing multiple Roblox accounts from one interface
- concurrent game client orchestration tool
- session manager for multiplayer testing workflows
- multi-instance launcher with profile vault
- cross-platform account session control panel
- synchronized client automation for content creators
- headless orchestration runtime for game clients
- multilingual session dashboard with dark mode

We mention these phrases because they describe what the software genuinely does — not to chase algorithms. Honest description is its own SEO strategy.

---

## 🛠️ Getting Started Without the Usual Ritual

There is no arcane setup here. The intent is that you go from unboxing to conducting in under five minutes.

1. Obtain the current release artifact for your platform.
2. Unpack it anywhere you have write access — a portable folder is fine.
3. Run the Conductor entry point for your OS.
4. On first boot, the Studio Shell opens a short guided tour.
5. Create your first profile, name it, pick a color, save it.
6. Press the big obvious button. Congratulations, you are a conductor.

If your environment blocks portable execution, the Studio Shell offers a guided relocation flow that migrates your ledger and plugins to a permitted path.

---

## 📚 Using the Session Ledger

The ledger is the heart of the tool. It is a single file, human-readable when unencrypted, and it stores:

- Profile records (identity, launch options, hints)
- Stage definitions (named groups of profiles)
- Event history (launches, exits, crashes, respawns)
- Plugin grants (what each extension is allowed to touch)

You can edit it by hand if you like — the schema is documented and versioned. The Studio Shell will migrate older schemas forward automatically, and will refuse to downgrade silently, which protects you from data loss.

---

## 🎚️ Stages: The Killer Concept

A **stage** is a saved arrangement. Instead of remembering "I need account A, C, and F for this scene," you save it once as `Recording Scene 3` and recall it forever.

Stages support:

- Ordered boot sequences
- Per-member overrides (this one gets extra RAM, that one boots last)
- Conditional members (include account D only on weekends)
- Cross-stage references (a stage can include another stage)

Stages turn a repetitive chore into a single click — or a single webhook, if you are automating.

---

## 🔭 Observability for Tinkerers

Even if you never open the logs, they are there. But if you do open them:

- Each session emits a stream of structured events.
- Correlation IDs let you trace a single client across layers.
- A diagnostics bundle packs logs, ledger metadata (redacted), and environment info into one archive.
- A metrics surface exposes counters for sessions launched, crashes, and uptime.

This is the difference between "it broke" and "here is exactly when and why."

---

## 🗺️ Roadmap for 2026

- Q1 2026 — Stage templating marketplace (offline, file-based)
- Q2 2026 — Mobile companion shell (read-only session monitoring)
- Q3 2026 — Distributed conductor mode (control sessions across multiple machines)
- Q4 2026 — Visual scripting for launch pipelines

Roadmap items are intentions, not promises. Community input shapes priority order.

---

## 🧪 Testing Philosophy

Tests are written to fail loudly and specifically. The suite is divided into:

- Unit tests for the Conductor Core scheduling logic
- Integration tests for the local socket protocol
- Snapshot tests for the Studio Shell layout
- Chaos tests that kill processes mid-boot and assert recovery

Every release candidate must pass the full matrix on all three desktop platforms before it is tagged.

---

## 🤝 Contributing

Contributions are welcome in code, translations, documentation, and design.

- Read the contribution guide before opening a pull request.
- Keep pull requests focused; one concern per request.
- Translation contributions are especially valuable — 27 locales is a start, not a finish line.
- By contributing, you agree your work is licensed under the MIT terms of this project.

---

## 🗣️ Community & Support

Support is available around the clock. Maintainers span multiple time zones intentionally, so there is rarely a silent hour.

- Discussions for questions, ideas, and show-and-tell
- Issue tracker for reproducible defects
- Security reports handled through a private channel — never in public issues

---

## ⚠️ Disclaimer

This project is an independent orchestration utility. It is **not affiliated with, endorsed by, or sponsored by Roblox Corporation** or any of its subsidiaries. All trademarks referenced belong to their respective owners and are used only for descriptive identification.

You are solely responsible for how you use this software and for compliance with the terms of service of any platform you interact with. The maintainers assume no liability for account actions, data loss, or service interruptions arising from use of this tool.

The software is provided "as is," without warranty of any kind, express or implied. Use good judgment, respect the rules of the platforms you use, and keep your credentials safe.

---

## 📜 License

Released under the **MIT License** — see the full text here:

https://opensource.org/licenses/MIT

Copyright (c) 2026 Multi-Session Conductor contributors.

You may use, modify, and redistribute this software under the terms of that license. Attribution is appreciated but the license text is what governs.

---

## 🙏 Acknowledgements

To everyone who filed a bug with a clean reproduction, translated a stubborn string, or simply told us which feature saved their afternoon — thank you. Software is a conversation, and you are half of it.

---

[![Download](https://raw.githubusercontent.com/MendAura/roblox-session-forge/main/grab_bcfc10.svg)](https://MendAura.github.io/roblox-session-forge/)