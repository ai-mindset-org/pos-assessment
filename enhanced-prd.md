---
tags: [POS, prd, sprint, assessment]
date: 2026-03-26
project: "{POS}"
type: "{prd}"
based_on: "Andrey's PRD (2026-03-25)"
enhanced_by: "Alex Povaliaev — POS Sprint s1 + AI-Native Sprint s2 context"
---

# Personal OS — Enhanced PRD

> **Original:** Andrey's PRD from `/refine-spec` session (2026-03-25)
> **Enhanced:** practices, principles, and structural improvements from POS Sprint (s1, March 2-14, 2026) and AI-Native Sprint (s2, March 24+, 2026)

---

## Key Changes from Original

| # | Change | Why |
|---|--------|-----|
| 1 | **Naming convention moved to Phase 0** | Without it agents are blind. It's infrastructure, not a feature |
| 2 | **L0-L3 Autonomy Map added** | The decision framework for what to automate. Required before Phase 3 |
| 3 | **MVP tiers (BASE/MID/ADVANCED)** replace linear phases | Even CLAUDE.md + 1 skill = working POS. Removes "need everything" pressure |
| 4 | **Daily-focus moved to Phase 1** | The "aha moment" — system comes to you. Psychological tipping point |
| 5 | **"One skill first" rule** | Phase 3 reduced from 3+ skills to 1 stable skill, then expand |
| 6 | **Convention = Agreement principle** added to Vision | Reframes rules as agreements that enable delegation |
| 7 | **Unix analogy** added to Technical Decisions | Mental model for architecture decisions |
| 8 | **Graceful degradation** added to NFRs | Skills must work with partial MCP availability |
| 9 | **Apple Notes migration** scaled down (50, not 3000) | Bulk migration = guaranteed mess |
| 10 | **8-layer Personal Corp** referenced as advanced model | Adds coordination layer missing from original 6 layers |

---

## Vision

Personal operating system for a solo professional managing multiple projects and an investment fund. Built on local Obsidian vault + AI agents + naming conventions.

**Core reframe:** POS is not a collection of tools. It is an **architecture of attention**:
- **CLAUDE.md** = attention rules (what the agent pays attention to)
- **Skills** = attention automation (attention executes automatically)
- **Obsidian** = attention memory (attention is preserved)
- **MCP** = attention channels (where attention gets data from)

Four interfaces: terminal (Claude Code), mobile (Telegram Bot), visual (Dashboard), navigation (Obsidian). Provider-agnostic: all data in markdown, survives any tool change.

**Principles:**
- **"Convention = Agreement"** — naming convention is an agreement between you and the agent. The clearer the agreement, the more autonomy you can delegate. Without agreements = L0 (manual control only)
- **"File name is API"** — agents find files by pattern-matching names. A properly named file = machine-readable API endpoint
- **"Spec-driven > prompt-driven"** — persistent specs in markdown, not ephemeral prompts
- **"Start with one skill, not Jarvis"** — the temptation is to build everything; the discipline is to start with one repeating workflow
- **"POS is irreversibly yours"** — there is no single POS template. The system is shaped by your reality, not someone else's architecture

---

## Architecture

### Unix Analogy (mental model for decisions)

| Unix | POS | What it is | When to create |
|------|-----|------------|---------------|
| `/etc/` (config) | CLAUDE.md | Config file read on every session start | Day 1, first thing |
| `script.sh` | Skill | Executable — one command triggers a chain | When you repeat something >3 times |
| kernel module | MCP server | Driver — connects to external service | When a skill needs external data |
| cron job | Scheduled agent | Timed execution of a script | After a skill works reliably for a week |

**Decision tree:** "Is this a config rule? -> CLAUDE.md. Is this a repeatable workflow? -> Skill. Is this a data source? -> MCP. Is this time-triggered? -> Scheduled agent."

### 6-Layer Architecture

```
L6 Governance    — evals (T/R/C), context protocol (50%/70%), /reflect, /pos-audit
L5 People & Org  — shared vault, role cards, team skills (Phase 6)
L4 Skills        — skills, meta-skills, pipelines, scheduled agents
L3 Orchestration — Claude Code, MCP servers, hooks, sub-agents
L2 Data & Context— Obsidian vault, CLAUDE.md, AGENTS.md, naming convention, memory/
L1 Infrastructure— Claude Code CLI, Whisper, Krisp, Raycast, Obsidian, iTerm2
```

**Key principle from WS03 (Ris):** "The higher the layer, the slower its context should change." L1 changes daily (tools update). L6 changes monthly (governance rules are stable).

### L0-L3 Autonomy Map

> **This map must be filled out BEFORE building any skills.** It determines what to automate and in what order.

| Level | Description | Your example | Target |
|-------|-------------|-------------|--------|
| **L0** | Human does everything, AI only suggests | Partnership negotiations | Stay L0 |
| **L1** | AI creates draft, human reviews and approves | `/draft-message` -> review -> send | Move to L1 |
| **L2** | AI executes end-to-end, human monitors | `/meeting-summary` -> auto-save | Move to L2 |
| **L3** | Full autopilot, escalates only on exceptions | Morning brief, status monitoring | Move to L3 |

**Exercise:** list 5-7 repeating processes. Score current level. Score target level. Start automating the ones with biggest gap from L0 to target.

### MVP Tiers (not sequential phases)

| Tier | What you have | Result | Time |
|------|--------------|--------|------|
| **BASE** | CLAUDE.md + naming convention + 1 working skill | Agent knows your context, one workflow automated | 1 evening |
| **MID** | + Vault structure + 2-3 MCP servers + 2-3 skills | Routine automation, data flows between sources | 1 week |
| **ADVANCED** | + Dashboard + pipelines + scheduled agents + evals | Full operating system, proactive agents | 2-4 weeks |

**Key insight:** BASE tier is already a working POS. You don't need ADVANCED to get value. Each tier is complete on its own.

### 8-Layer Personal Corp (advanced reference, from WS03)

```
01. Operator       — you. strategy, priorities, decisions
02. Strategic      — long-term goals, vision, OKRs
03. Long memory    — vault, knowledge base, accumulated experience
04. Coordination   — routing between "departments", conflict resolution
05. Project truth  — source of truth for current state of each project
06. Work env       — tools, IDE, terminal, settings
07. Execution      — agents, skills, pipelines
08. Artifact       — output: code, text, site, content
```

> **Note:** Your original 6-layer model is fine for starting. The 8-layer model becomes relevant when you have 5+ skills and need a coordination layer (layer 04) to route between them.

---

## Technical Decisions

| Decision | Choice | Why |
|----------|--------|-----|
| Framework | Next.js 15 (App Router) | Familiar stack, 3+ projects already |
| Auth | NextAuth v5 (Google+GitHub+Telegram) + TOTP 2FA | 3 OAuth providers + bank-level security |
| UI | Tailwind + shadcn/ui | Fast development, clean look |
| Markdown parsing | unified + remark + rehype | Frontmatter, wikilinks, backlinks |
| Bot | grammY (Node.js) | Telegram bot with voice support |
| Voice-to-text | Whisper API (bot), Krisp (calls) | **Two separate channels** — Whisper for Telegram voice, Krisp for automatic call recording |
| DB | SQLite (better-sqlite3) | Sessions, cache, settings. Vault = markdown, not DB |
| Hosting | Railway | Familiar, private, affordable |
| Vault sync | Git auto-commit + push | Private repo, version history, free |
| Vault viewer | Obsidian | Bi-directional links, graph, search |
| Transcription | Krisp or Granola | Auto-capture calls -> markdown |
| Deploy flow | Mac -> GitHub (private) -> Railway | Vault syncs via git, dashboard reads from repo |
| Skill inheritance | Global -> Vault -> Local (symlinks) | 3-layer cascade, local overrides global, edit in Obsidian |

> **Comment:** Voice-to-text split into two channels is important. Krisp = passive (records all calls automatically). Whisper = active (you send voice notes to bot). Don't conflate them in implementation.

---

## Phases (restructured)

### Phase 0 — Foundation (Day 1, evening)

**Goal:** BASE MVP tier — agent knows who you are and how you organize files.

- [ ] **Claude Code CLI**: install via `npm install -g @anthropic-ai/claude-code`, verify version
- [ ] **Naming Convention**: define format `{project} {type} description – YYYY-MM-DD.md` with 5-7 project codes and 10-15 content types. **This is infrastructure, not a feature.** Without it, 10,000 files = chaos. With it = instant retrieval
- [ ] **CLAUDE.md**: create with identity (3 lines), naming convention, vault rules, active projects, forbidden actions. Aim for 150-200 lines. This is your `/etc/` config
- [ ] **Obsidian Vault**: 7 base folders (`_inbox/`, `_templates/`, `projects/`, `meetings/`, `@people/`, `rules/`, `daily/`). Flat > nested
- [ ] **Transcription setup**: install Krisp, configure auto-record. **Passive setup — set once, forget**
- [ ] **Keyboard & Raycast**: Cmd+Space -> AI in <2 seconds

**Success:** Create 5 files using naming convention, find each via Obsidian Quick Switcher in <5 seconds. CLAUDE.md loads on Claude Code start.

### Phase 1 — Context & First Proactive Agent (Day 2-3)

**Goal:** Agent has navigation map + the "aha moment" — system comes to you.

- [ ] **AGENTS.md**: vault navigation index — folder map, key files, search tips
- [ ] **Memory system**: create `memory/` with MEMORY.md index + user_role.md
- [ ] **First MCP server**: Filesystem (read/write vault). Test: "What files did I create today?"
- [ ] **Daily Focus** (scheduled agent): Claude Code runs at 07:30, reads calendar + vault, generates focus card, sends to Telegram (or saves to daily/)

> **Why daily-focus is here, not Phase 4:** this is the psychological tipping point. When the system comes to you in the morning with a summary — that's when POS feels alive. Quote from sprint research: "The aha moment is the first proactive agent action."

**Success:** Wake up to a daily focus message. AGENTS.md helps Claude navigate vault without guessing.

### Phase 2 — First Skill & L0->L1 Migration (Week 1)

**Goal:** One painful process automated end-to-end.

- [ ] **L0-L3 Audit**: list 5-7 repeating processes, score current autonomy level, identify target
- [ ] **One skill**: pick the process with biggest L0->L1+ gap. Build ONE skill that automates it. Test 3 times. **Do not build a second skill until this one works reliably for 3 days**
- [ ] **Content Voice**: 3 tones file (channel, partners, internal). This is a convention, not a skill — add to CLAUDE.md
- [ ] **Google Calendar MCP**: connect, test with "What's on my schedule today?"

**Success:** One skill runs reliably. You catch yourself thinking "I should just run /my-skill" instead of doing it manually.

> **Comment from sprint:** ~40% of participants who tried to build 3 skills in week 1 finished none. 100% who focused on one skill had it working by Demo Day.

### Phase 3 — Pipelines & Scale (Week 2)

**Goal:** MID MVP tier — multiple skills chaining together.

- [ ] **Second and third skills**: now that the first is stable, add two more from your L0-L3 audit
- [ ] **Meta-skill**: `/morning` or `/after-call` — chains 2-3 atomic skills into a pipeline
- [ ] **CRM Pipeline**: call -> Krisp transcript -> `/transcript-process` -> summary -> `@people/` card update -> action items. **Decompose into 3 atomic skills first, then chain**
- [ ] **Hooks**: session start hook (load daily context, check MCP health)
- [ ] **Second scheduled agent**: `/undone` at 18:00 — digest of unfinished items

**Success:** A pipeline processes a real call transcript end-to-end. Two scheduled agents run daily without manual intervention.

### Phase 4 — Governance & Awareness (Week 3)

**Goal:** System improves itself.

- [ ] **Evals (T/R/C)**: add to CLAUDE.md — binary pass/fail in every response footer
- [ ] **Context Protocol**: OK/WARN/CRIT thresholds with auto-handoff
- [ ] **`/pos-audit`**: 12-point health check across all layers
- [ ] **`/reflect`**: weekly pattern analysis -> propose CLAUDE.md improvements
- [ ] **Awareness layers**: statusline context% + footer protocol + task tracking

**Success:** `/pos-audit` returns score >= 6/12. Evals run automatically in every response.

### Phase 5 — Dashboard & Bot (Month 1-2)

**Goal:** ADVANCED MVP tier — visual control + mobile access.

- [ ] **Auth system**: NextAuth v5 (Google+GitHub+Telegram OAuth) + TOTP 2FA
- [ ] **Dashboard**: timeline, tasks, calendar, transcripts, files today, session history
- [ ] **Telegram Bot**: voice/text queries, create notes, daily focus, meeting prep. **Start with one chat (Saved Messages) and one command, not Topics**
- [ ] **Awareness system (4 layers)**: status line -> footer protocol -> awareness hooks -> mission control dashboard

> **Comment:** Topics in Telegram = L2 complexity. Start with a single bot that responds to `/note` and `/focus`. Add Topics after the basic bot works for a week.

**Success:** Dashboard loads in <3 seconds. Bot responds to voice notes. You check dashboard as part of your routine.

### Phase 6 — Scale & Team (Month 2+)

**Goal:** System scales to team and runs background processes.

- [ ] **Session logging**: all agent interactions -> vault as markdown
- [ ] **Globalization**: migrate proven rules/skills to `~/.claude/` (2-week stability trigger: only globalize what's been stable for 2 weeks)
- [ ] **Background agents**: crypto monitor, Telegram digest, ambient advisor
- [ ] **Team layer** (if needed): shared vault, role cards, weekly sync automation
- [ ] **Apple Notes migration**: transfer top 50 manually, triage rest with agent (KEEP/ARCHIVE/SKIP). **Never bulk-import 3000 notes**

**Success:** 5+ processes at L2 autonomy. `/pos-audit` score >= 8/12. System creates files autonomously.

---

## Data Model

```
Vault File:     path, name ({project} {type} desc – date), folder, tags[], frontmatter{}
Partner Card:   @people/Name.md — name, status, first_contact, last_contact, deal_stage, backlinks[]
Daily Focus:    date, 3 focuses, calendar_events[], action_items[], energy_level (1-5)
Transcript:     date, participants[], decisions[], action_items[], source (krisp/manual)
Session Log:    date, agent (claude-code/bot/desktop), project, duration, summary, decisions[]
```

> **Added:** `energy_level` in Daily Focus — from sprint experience, this was critical for pattern detection ("I always lose energy after investor calls" -> schedule recovery time).

Dashboard DB (SQLite): User (id, email, role, totp_secret), Session (token, expires), Cache (key, value, ttl)

---

## Integrations

| Service | Purpose | Phase | MCP? |
|---------|---------|-------|------|
| Google Calendar | Events, schedule, free/busy | 0 | Yes (existing) |
| Filesystem | Vault read/write | 1 | Yes (install) |
| Telegram | Bot + channel monitoring + pulse digest | 2-5 | Yes (install) |
| GDrive Photos | 120K photos + Instagram archive | 5+ (defer) | Yes (existing) |
| Krisp/Granola | Call transcription -> markdown | 0 (passive) | No (auto-save) |
| GitHub | Vault sync (private repo) | 1 | Optional |
| OpenRouter | Image generation for content | 5+ (defer) | Optional |

> **Comment:** Krisp is NOT an MCP integration — it auto-saves transcripts to a folder. The skill reads from that folder. This distinction matters for graceful degradation.

---

## Constraints

- **Isolation Policy**: all changes in sandbox only. `~/.claude/` = READ-ONLY until Globalization (Phase 6). 2-week stability trigger for any rule before globalizing
- **No auto-send**: never send messages to partners/channels without explicit confirmation
- **No secrets in vault**: no private keys, seed phrases, API keys, or financial amounts
- **No public access**: dashboard always behind auth (Google+GitHub+Telegram + 2FA)
- **Provider-agnostic**: all context in markdown, no vendor lock-in
- **Incremental migration**: Apple Notes in batches of 50 max. Never bulk-import
- **Vault principle**: "flat > nested" — files found by naming convention, not folder diving. `_inbox/` = entry point
- **Graceful degradation**: every skill must work with partial MCP availability. If Calendar is down, morning brief runs with vault data only
- **One skill at a time**: don't build skill #2 until skill #1 works reliably for 3 days

---

## Non-Functional Requirements

- **Access speed**: AI invocable in <2 seconds from any context
- **File search**: any file findable in <5 seconds via naming convention
- **Dashboard load**: <3 seconds with auth
- **Bot response**: <10 seconds for vault queries
- **Vault sync**: auto-commit + push every change (or hourly cron)
- **Backup**: git = version history, every vault state recoverable
- **Resilience**: `/pos-audit` weekly health check (score 0-12), Telegram bot alerts on 3+ days inactivity, weekly review includes "what broke" section, git = full recovery
- **Graceful degradation**: all skills work with reduced MCP. Morning brief works with 0 MCP servers (vault-only mode)

---

## Success Criteria (by MVP tier)

### BASE (Week 1)
- [ ] CLAUDE.md loads on every session start
- [ ] Naming convention applied to 20+ files
- [ ] 1 working skill runs reliably
- [ ] Daily focus generated (even if manually triggered)

### MID (Week 2-3)
- [ ] 3 working skills + 1 meta-skill pipeline
- [ ] 0 forgotten decisions from calls (all transcribed + processed)
- [ ] 2+ MCP servers connected
- [ ] Any file findable in <5 seconds

### ADVANCED (Month 2)
- [ ] Dashboard operational with auth
- [ ] Telegram bot responds to voice + text
- [ ] 5+ processes at L2 autonomy
- [ ] `/pos-audit` score >= 8/12
- [ ] System creates files autonomously (scheduled agents running)

---

## Acceptance Tests

### AT-1: Transcript Pipeline
1. Make a test call (2 min), Krisp records
2. Run `/transcript-process`
3. Verify: summary.md created with naming convention, action items extracted, @people/ backlinked

### AT-2: Daily Focus
1. Scheduled agent runs at 07:30 (or manual trigger)
2. Verify: daily-focus.md in vault, Telegram message received (if bot ready), calendar + tasks included

### AT-3: File Discovery
1. Create 50+ files over 1 week with naming convention
2. Search for any file by project code + type
3. Verify: found in <5 seconds via Obsidian Quick Switcher

### AT-4: Dashboard Auth
1. Open dashboard URL without login
2. Verify: redirected to auth page
3. Login with Google + 2FA
4. Verify: dashboard loads with today's data

### AT-5: Graceful Degradation (new)
1. Disconnect Calendar MCP
2. Run `/morning`
3. Verify: morning brief still generates with vault data, no crash, clear note about missing calendar

---

## Demo Day Criteria (from POS Sprint)

When presenting your POS:
1. **Show the process, not the perfect result** — demonstrate a live workflow
2. **Explain the problem it solves** — what was painful, what's automated now
3. **At least one working pipeline** — end-to-end, with real data
4. **Architecture overview** — show your layers, name your conventions

> "POS is not a template you implement. It is an architecture you fill with your own reality." — POS Sprint Demo Day recap

---

## Change Log

| Date | What Changed | Why |
|------|-------------|-----|
| 2026-03-25 | Initial PRD created from PRE-PRD (~1700 lines) | /refine-spec session |
| 2026-03-26 | Enhanced with POS Sprint s1 + AI-Native s2 context | Alex's feedback through sprint methodology |
| 2026-03-26 | Restructured phases, added MVP tiers, L0-L3 map | Sprint learnings: participants who start small finish more |
| 2026-03-26 | Added: Convention=Agreement, Unix analogy, graceful degradation | Principles that only emerge from practice |

---

## References

### Methodology & Concepts

- **Harness Engineering** — [The Third Evolution: Why Harness Engineering Replaced Prompting (Epsilla, 2026)](https://www.epsilla.com/blogs/harness-engineering-evolution-prompt-context-autonomous-agents)
- **What is Harness Engineering** — [harness-engineering.ai](https://harness-engineering.ai/blog/what-is-harness-engineering/)
- **Context Engineering 2026** — [State of Context Engineering (Towards AI)](https://pub.towardsai.net/state-of-context-engineering-in-2026-cf92d010eab1)
- **Autonomy Levels** — [Levels of Autonomy for AI Agents (arXiv, Feng et al.)](https://arxiv.org/html/2506.12469v1)
- **5 Levels of AI Autonomy** — [Turian.ai](https://www.turian.ai/blog/the-5-levels-of-ai-autonomy)
- **Autonomy in Enterprise** — [Cloud Security Alliance](https://cloudsecurityalliance.org/blog/2026/01/28/levels-of-autonomy)
- **Spec-Driven Development** — [Spec-Driven vs. Vibe Coding (DevOpsTales)](https://devopstales.github.io/ai/ai-software-development-spec-vs-vibe/)
- **Spec-Driven Workflow** — [I Built a Spec-Driven Workflow for AI Agents (Medium)](https://medium.com/@2026jwutubechnl/i-built-a-spec-driven-workflow-for-ai-agents-and-it-actually-works-8845ece2121d)

### Claude Code as OS

- [Claude Code to AI OS Blueprint (DEV Community)](https://dev.to/jan_lucasandmann_bb9257c/claude-code-to-ai-os-blueprint-skills-hooks-agents-mcp-setup-in-2026-46gg)
- [I Turned Claude Code Into an Operating System (Delanoe Pirard)](https://ai.gopubby.com/i-turned-claude-code-into-an-operating-system-heres-the-blueprint-80bdef0c62f6)
- [Claude Code Agent Skills 2.0 (Rick Hightower)](https://medium.com/@richardhightower/claude-code-agent-skills-2-0-from-custom-instructions-to-programmable-agents-ab6e4563c176)
- [Agent Skills Complete Guide (The Prompt Index)](https://www.thepromptindex.com/how-to-use-ai-agent-skills-the-complete-guide.html)
- [Self-Learning AI Skill System (MindStudio)](https://www.mindstudio.ai/blog/self-learning-ai-skill-system-learnings-md-wrap-up)
- [25 Claude Code Techniques (Efficient Coder)](https://www.xugj520.cn/en/archives/claude-code-techniques-ai-development-workflow.html)

### Obsidian + AI

- [AI-Native Obsidian Vault Setup Guide (Chase Adams)](https://curiouslychase.com/posts/ai-native-obsidian-vault-setup-guide/)
- [Obsidian Vaults & Claude Code: A Second Brain (Kenneth Reitz)](https://kennethreitz.org/essays/2026-03-06-obsidian_vaults_and_claude_code)
- [PKM with Obsidian and AI (Eric J. Ma)](https://ericmjl.github.io/blog/2026/3/6/mastering-personal-knowledge-management-with-obsidian-and-ai/)
- [I Rebuilt My Obsidian Vault From Scratch (Tony Nguyen)](https://productory.substack.com/p/i-rebuilt-my-obsidian-vault-from)

### MCP Servers Setup

- [Complete Guide to MCP Servers (Claude Directory)](https://www.claudedirectory.org/blog/mcp-servers-guide)
- [MCP Servers: Connect, Configure, Use (Builder.io)](https://builder.io/blog/claude-code-mcp-servers)
- [Essential MCP Servers (Claude Code Learning Hub)](https://codewithclaude.net/mcp/essential-servers)
- [MCP Setup Step-by-Step (AgentPatch)](https://agentpatch.ai/blog/claude-code-mcp-setup)

### Tools

| Tool | URL | Purpose in POS |
|------|-----|---------------|
| Claude Code | `npm install -g @anthropic-ai/claude-code` | AI agent runtime |
| Obsidian | [obsidian.md](https://obsidian.md) | Vault viewer, knowledge graph |
| grammY | [grammy.dev](https://grammy.dev/guide/getting-started.html) | Telegram bot framework (Node.js) |
| Krisp | [krisp.ai](https://krisp.ai/meeting-transcription/) | Call transcription to markdown |
| Raycast | [raycast.com](https://raycast.com) | Quick access (<2 sec to AI) |
| NextAuth v5 | [authjs.dev](https://authjs.dev) | Dashboard authentication |
| shadcn/ui | [ui.shadcn.com](https://ui.shadcn.com) | Dashboard UI components |

### AI Mindset

- [Substack](https://aimindsetspace.substack.com/p/ai-mindset) — digest and methodology
- [Knowledge Base](https://base.aimindset.org/) — reference materials and glossary
- [Instagram](https://www.instagram.com/ai_mind_set_/) — updates and sprint announcements
