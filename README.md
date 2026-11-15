# Blueprint

**A Claude Code plugin that gives vibe-coded games and web apps a product blueprint before the code: the screens, flows and settings real studios never forget, plus phases, gates and a folder structure.**

[Tiếng Việt](README.vi.md) · License: [MIT](product-blueprint/LICENSE) · Sources: [SOURCES.md](product-blueprint/SOURCES.md)

## Why

When an AI writes all the code, it tends to jump straight into gameplay. The usual result: settings scattered over the play screen, no title screen, no New Game / Continue, a "Save" button with no decision on where saves live, no profile or admin pages, and features bolted on whenever someone remembers them, so the same files get edited over and over.

Blueprint fixes the *what* and *when done*, not the code. It writes a small design folder that any AI or person can read, and it checks the project against it.

## What it covers

- **Games, including browser games.** First-launch setup, title / main menu, one shared Settings screen (reachable from the menu and from Pause), Pause, HUD without settings on it, New / Continue / Load, autosave kept apart from manual saves, tutorial, game over, results, credits, a welcome screen to choose guest play or sign-in, guest-to-account upgrade, and multiplayer rooms (create, join, approve, kick, transfer host, lobby, reconnect, results). Browser-specific rules cover the audio unlock on the first click, auto-pause on tab switch, localStorage limits and Safari eviction, save export, and iframe embedding.
- **Web apps.** Screens per role: public pages, 404/500, sign-up, sign-in, password reset (OWASP), profile, account settings, data export, account deletion (Apple 5.1.1(v)), admin with an audit log, and empty / loading / error states on every screen.
- **Phases and gates.**
  - Games: concept → prototype → vertical slice → alpha → beta → release.
  - Web apps: discovery → alpha → beta → live, adapted from the GOV.UK Service Manual.

  Every gate has measurable criteria.
- **Structure.** `architecture.md` splits core services from modules, and its Folder map must be approved before the first line of real code. Files outside the map are flagged.
- **Scope control.** New ideas go to `ideas.md`, not into the code. A **Keep** list protects what you love, and there is a cut list before release.

## Install

In Claude Code:

```
/plugin marketplace add sefxvn16/blueprint
/plugin install product-blueprint@blueprint
```

Turn it on or off with `/plugin`. There are no hooks, no scripts and no dependency on other plugins, so disabling it never breaks a project. The files it writes are plain Markdown and JSON.

## Use

Run `/blueprint`, or just talk:

| You want to | Say something like | Mode |
|---|---|---|
| Start a new game or web app | "make a pet-raising game that runs in the browser" | `new` |
| Find what is missing, or check whether you can move to the next phase | "what screens is this game missing?" | `check` |
| Park an idea without coding it now | "could we add fishing?" | `idea` |

## What it writes in your project

```
design/README.md       spec: vision, scope, Keep, Not doing, screen list, index
design/<domain>.md     one file per domain (shell UI, gameplay, characters, levels, art & audio…)
design/features.json   features with acceptance criteria; "pass" needs evidence
design/ideas.md        ideas waiting for the next phase gate
architecture.md        stack, Folder map, core vs modules, data storage
```

It never writes code and never touches `PLAN.md`, `CLAUDE.md` or `AGENTS.md`.

## Repository layout

```
.claude-plugin/marketplace.json
product-blueprint/.claude-plugin/plugin.json
product-blueprint/skills/blueprint/SKILL.md
product-blueprint/skills/blueprint/references/{common,game,webapp}.md
product-blueprint/skills/blueprint/templates/*
product-blueprint/SOURCES.md     references, for human readers (the skill never loads it)
product-blueprint/LICENSE
```

## Language

The skill's instructions and the documents it writes are in **Vietnamese**. File names, headings, IDs and data keys are in English. Claude follows the instructions whatever language you write in, but the generated prose will be Vietnamese unless you ask otherwise.

## Known limits

- The file-size thresholds for design documents (80 / 400 lines, 25 KB) are estimates.
- Multiplayer has a room checklist (create, join, approve, kick, transfer host, lobby, leave, reconnect, results, leaderboard, reports); matchmaking with strangers and friend lists are not covered yet.
- The `new` mode has been tested in a real session. `check` was used on a real project (0.2.0 fixes: read render conditions, check that saved settings are applied, run the app, compare with the project's own design docs); `idea` has not been tested yet.
- A few browser-game rules are common practice rather than official guidance; they are marked as such in `game.md`.

## About

Blueprint is a free, independent plugin made by a hobbyist who vibe-codes games and web apps and kept hitting the same missing basics. Its rules come from public guidance by Microsoft/Xbox, Apple, Google, Valve, Anthropic, GOV.UK, OWASP, W3C, MDN, Basecamp (Shape Up) and the Scrum Guide. Ideas, not code, are also borrowed from the MIT-licensed [Claude-Code-Game-Studios](https://github.com/Donchitos/Claude-Code-Game-Studios). See [SOURCES.md](product-blueprint/SOURCES.md) for every source and how far it was read.

Issues and suggestions are welcome.

## License

[MIT](product-blueprint/LICENSE): free for any purpose, including commercial use. Keep the copyright notice.
