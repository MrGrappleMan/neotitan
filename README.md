# Neotitan

A modern, legacy-free bootc desktop OS built with BuildStream 2, featuring the **COSMIC** desktop environment and **nmbl** (No More Boot Loader) direct UKI booting.

## Key Features

- **Desktop Environment:** COSMIC Desktop Environment (System76) driven by `greetd` + `cosmic-greeter`.
- **Bootloader Architecture:** `nmbl` (No More Boot Loader) direct booting via Unified Kernel Images (UKIs) without GRUB or systemd-boot.
- **Image Architecture:** Bootable OCI image (`bootc`) assembled hermetically from source with BuildStream 2.
- **Workstation Tuning:** Low-latency kernel scheduler kargs (`preempt=lazy`, `threadirqs`), ZSwap memory caching with zstd compression, and TCP BBR congestion control.


## Built-in feedback loop

Dakota doesn't eat tickets, it treats them as evidence.

Every user running Dakota is part of a structured loop that flows directly back into upstream GNOME, freedesktop, and the kernel. When something breaks on your hardware, you have three commands:

| Command | What it does |
|---|---|
| `ujust report` | Captures your system state and opens a pre-filled issue. One command instead of a wall of "please attach logs." |
| `ujust confirm <issue>` | Tells the team your hardware hits the same bug. Adds a hardware fingerprint to the issue — no duplicate filing. |
| `ujust verify <issue>` | After a fix ships in a nightly, confirms it works on your machine. Closes the loop with evidence. |

No telemetry. No phone-home. Every report is reviewed by you before it leaves your machine, lives in a gist you own, and can be deleted anytime.

When three users independently run `ujust verify` on a fix, that issue closes with real confidence — not just "we think this is fixed."

### The hardware layer

Each Dakota installation is designed to run as a hardware diagnostic lab for itself. When will you find your first?

[Read the full feedback loop design](docs/feedback-loop.md)

## The research behind it

Dakota is human driven with contribution workflows for agents, so if you have tokens to donate, ask it to review issues or PRs, it's useful! The humans make the final decisions. We coordinate this project via a tool called [Hive](https://github.com/kubestellar/hive) from Kubestellar, a CNCF Sandbox project.

Dakota's feedback loop model is grounded in Andy Anderson's work on autonomous AI-assisted software development. The core finding: the intelligence of a system like this lives not in any single model, but in the infrastructure of instructions, tests, metrics, and feedback loops surrounding it.

- [The AI Codebase Maturity Model](https://arxiv.org/abs/2604.09388) — the arxiv paper
- [When AI agents become contributors](https://www.cncf.io/blog/2026/05/14/when-ai-agents-become-contributors-how-kubestellar-reached-81-pr-acceptance/) — CNCF blog
- [Beyond prompting: How KubeStellar reached 81% PR acceptance](https://thenewstack.io/ai-codebase-maturity-model/) — The New Stack
- [KubeStellar Hive](https://github.com/kubestellar/hive) — the reference implementation Dakota draws from

## Help shape what gets built

**Architects and designers** — these features and epics need your input before any code is written. Design decisions, tradeoffs, and priorities:

### [Open issues needing triage &rarr;](https://github.com/projectbluefin/dakota/issues?q=is%3Aopen+label%3Aneeds-triage)

Leave a comment, challenge the design, propose alternatives. When an issue reaches consensus a maintainer marks it with `/triage accepted`.

**Engineers** — these issues have clear acceptance criteria and no open design questions. Pick one up and build it:

### [Triage-accepted queue &rarr;](https://github.com/projectbluefin/dakota/issues?q=is%3Aopen+label%3Atriage%2Faccepted+no%3Aassignee)

Assign yourself with `/assign`. See [docs/workflow.md](docs/workflow.md) for the contributor workflow.

## Image streams

|        Tag |  Stream |                                                                                                    What it is |
| ---------: | ------: | ------------------------------------------------------------------------------------------------------------: |
|  `:stable` |  Stable |                        GNOME 50 — production. On-demand promotion from `:testing` via `just release --apply`. |
| `:testing` |     Dev |                                              GNOME 50 — daily builds from `testing` branch. Boot-check gated. |
|    `:next` |  Paused |                                     GNOME master. Paused until the next GNOME beta; receives no updates. |
|     `:btw` |  Paused |                                                                                            Alias for `:next`. |

`:next` / `:btw` is paused until the next GNOME beta and no longer receives updates, including security fixes. If you are on it, switch to `:testing`. Moving from GNOME master back to the current release is a downgrade, so some settings or app data written by the newer GNOME may not carry over.

```bash
sudo bootc switch ghcr.io/projectbluefin/dakota:testing
```

## ISO Download

[dakota-live-latest.iso](https://projectbluefin.dev/dakota-live-latest.iso) · [Checksum](https://projectbluefin.dev/dakota-live-latest.iso-CHECKSUM)


## Known gaps

- Installation path is still being worked on
- Upgrades and rollbacks need more hardening

See the [open issues](https://github.com/projectbluefin/dakota/issues) for where things stand.

## Contributing or building from source

See [AGENTS.md](AGENTS.md) for the full contributor workflow, build instructions, and PR checklist.

![Dakorator](https://github.com/user-attachments/assets/ee92291d-a617-496e-abb6-9045a4c665ce)
