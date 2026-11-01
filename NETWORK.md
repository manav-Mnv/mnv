# How the mnv.model project network works

The "Every project, wired up" section of mnv.model (`/model/#latent`) is a small three-layer neural network. Its outputs are my real public GitHub projects.

## Sources

I went through all 38 public repos on github.com/manav-Mnv on 1 Nov 2026, including the README of every featured project. Private repos are not shown or named. The page only states facts taken from repo descriptions and READMEs. Where a demo is illustrative, the page says so.

## The three layers

| Layer | Nodes | What it means |
|---|---|---|
| Input: skills | LLM agents + MCP, Graphs + Cypher, Python, Web + backend, Swift + SwiftUI, ARKit + RealityKit, On-device ML, Kotlin + Android | What I build with |
| Hidden: themes | Agents that show their work, Money + risk, Memory, Care + wellbeing, Campus tools, Learning in public | Why I build it |
| Output: projects | 15 projects (below) | What I shipped |

## How the edges are made

- **Theme to project:** a project connects to each theme it belongs to. The line gets thicker with the project's weight: Hound and LUME are 1.0, Fragments 0.7, and the rest are 0.35 to 0.6.
- **Skill to theme:** these lines are not drawn by hand. Each one is the sum of the weights of every project that uses that skill inside that theme. For example, Swift to Memory = LUME (1.0) + The Room (0.6) = 1.6. Skills I use more often for a theme get thicker lines automatically.
- **Forward pass button:** a pulse travels every skill-to-theme edge, then every theme-to-project edge, and the strongest output (Hound) lights up at the end.
- **Tapping a node:** this highlights its full path. A project shows its themes and skills, a theme shows every project it fires, and a skill shows the projects that use it.

## What joins the two big projects

**Memory** is the hidden unit that Hound and LUME share:

- Hound keeps every case, analyst lesson and playbook as nodes in the graph. They are attached to the same people and accounts as the transactions, so remembering is just following the graph.
- LUME turns your own memories into 3D museum stands placed around you, each in the direction where it happened.
- The Room's on-device AI journal sits on the same unit.

## The 15 projects, in priority order

| # | Project | Repo(s) | Themes | Skills |
|---|---|---|---|---|
| 1 | **Hound**: AML agents on FalkorDB, Graph Hacks 2026 | hound-aml | Agents, Money, Memory | LLM agents, Graphs, Python, Web |
| 2 | **LUME**: AR memory journal, Swift Student Challenge | L-U-M-E | Memory, Care | Swift, ARKit |
| 3 | Fragments: draw-yourself-in story, WWDC26 | Fragments | Care | Swift |
| 4 | The Room: student mental wellness app, IndeHub 2026 | the-room | Care, Memory | Swift, On-device ML, Web |
| 5 | IntelliCredit AI: credit appraisal memos | intelli-credit-ai-1.0, ICT-webpage | Money, Agents | Python, LLM agents, Web |
| 6 | Code Review OpenEnv: RL environment for review agents | code-review-env- | Agents, Learning | Python, LLM agents |
| 7 | Puma (EDGE): campus event platform | puma, edge-web | Campus | Web |
| 8 | Apple Lab kiosk: face-recognition attendance | aatce-apple-lab, swifters, attendance | Campus | Swift, On-device ML, Web |
| 9 | EchoNav: offline navigation for blind users | EchoNav | Care | Kotlin, On-device ML |
| 10 | PO: on-device emotion-aware companion | PO | Care | Kotlin, On-device ML |
| 11 | BLOOM: wellness web app in English and Hindi | bloom-v1.2 | Care | Web, LLM agents |
| 12 | SwiftSteps: teach Swift to beginners | swift-2026-1, SwiftStepss.swiftpm | Learning | Swift |
| 13 | Routiner: 6-week SwiftUI teaching course | routiner | Learning, Campus | Swift |
| 14 | Hub bot: WhatsApp bot for Tinkering Hub clubs | whatsapp-hub-bot | Campus | Web |
| 15 | AI research log: path into AI research | ai-research-journey | Learning | Python |

These are listed as one line under the network rather than as nodes: suinft, PatternFusionX, proactive-node-clone, Book, M-N-V---webpage, dev-portfolio and buttons.

These are left out: forks (bloom-whispers-nexus, swift-argument-parser, India-Accelerator-OpenXAI-2025), learning and practice repos (ToDoList01, GetSet, GCF_sem2, Marquee_Traning_2026), small fun sites (bdy-web), the profile README repo, and this site itself.

## Where to change it

All the data is in `model/index.html`, in the `SKILLS`, `THEMES` and `PROJECTS` arrays under "project network". To add a project, add one object to `PROJECTS` with its weight `w`, its themes `th` and its skills `sk`. The edges and layout update on their own.
