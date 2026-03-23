# 🤖 AI-Agents

> A structured guide to build and orchestrate a complete AI-powered software development team using specialized agents, MCP tools, and shared memory across projects.

Stop prompting AI one task at a time. This repo gives you a **reusable team of specialized agents** — each with a defined role, tools, memory, and conventions — that work together to design, build, test, and document software projects.

---

## Who is this for?

- Developers who want to automate repetitive dev tasks with AI
- Teams exploring multi-agent workflows for real projects
- Anyone building with Claude, GPT, or Gemini APIs
- Developers tired of re-explaining context to AI on every session

---

## The idea

Most people use AI as a single assistant. This repo treats AI as a **team**:

```
You describe what to build
        ↓
PO defines the User Stories
        ↓
Scrum Master coordinates the team and manages tasks
        ↓
DBA designs the database schema
        ↓
Backend implements the API
        ↓
Frontend builds the UI
        ↓
Tester runs E2E tests
        ↓
DocGen documents everything
```

Each agent has **one responsibility**, knows **only its own routes**, and updates **its own memory** at the end of every task.

---

## Key concepts

### Agents are reusable across projects

The agent is the **specialization**. The project context is **swappable**:

```
Backend Agent + context of Project A  →  works on Project A
Backend Agent + context of Project B  →  works on Project B
```

You never create new agents per project — you create new **contexts**.

### Memory persists between sessions

Each agent maintains its own memory file per project:

```
memory-backend.md   → endpoints created, patterns used, decisions made
memory-dba.md       → tables, relations, design decisions
memory-tester.md    → what was tested, bugs found, coverage
```

No more re-explaining what was already built.

### Tools via MCP

Agents interact with the real world through MCP (Model Context Protocol) servers — read/write files, run queries, create branches, commit code, search the web.

---

## The team

| Agent | Role | Repo |
|---|---|---|
| **PO** | Defines User Stories and acceptance criteria | — |
| **Scrum Master** | Coordinates the team, manages tasks and blockers | All (read) |
| **DBA** | Designs schemas and migrations | `db-repo/` |
| **Backend** | Implements APIs and business logic | `back-repo/` |
| **Frontend** | Builds UI and consumes the API | `front-repo/` |
| **Tester** | Runs E2E and regression tests | `test-repo/` |
| **DocGen** | Documents what the team delivers | `*/docs/` |

---

## Repository structure

```
agents/
│
├── roles/                        # Who each agent is and how they work
│   ├── po.md
│   ├── scrum.md
│   ├── dba.md
│   ├── backend.md
│   ├── frontend.md
│   ├── tester.md
│   └── docs.md
│
├── prompts/                      # Reusable instruction templates
│   └── README.md
│
├── projects-memories/            # Context and memory per project
│   ├── context_example.md        # Template — copy this to start a new project
│   └── {project-name}/           # One folder per project
│       ├── context.md            # Stack, rules, structure (you fill this)
│       ├── tasks.json            # Tasks per User Story (Scrum Master manages this)
│       ├── progress.json         # Real project status (Scrum Master manages this)
│       ├── memory-dba.md
│       ├── memory-backend.md
│       ├── memory-frontend.md
│       ├── memory-tester.md
│       └── memory-docs.md
│
└── mcp/                          # MCP server configuration
    ├── config.json               # All available MCP servers
    ├── README.md
    └── custom/                   # Your own MCP servers
        └── README.md             # Includes a full example
```

---

## Conventions enforced across all agents

### Branch naming
```
feat-HU{number}
Examples: feat-HU001, feat-HU015
```

### Commit messages
```
{PROJECT_INITIALS}{commit_number} | {Short description}
Examples:
  ESC01 | Alumnos table migration created
  SF03  | Income endpoint implemented
  ECOMM08 | Cart view completed
```

Project initials are defined in each project's `context.md`.

---

## Testing responsibilities

| Test type | Responsible | Location |
|---|---|---|
| Unit tests | Backend | `back-repo/tests/unit/` |
| Unit tests | Frontend | `front-repo/tests/unit/` |
| Integration | Frontend | `front-repo/tests/integration/` |
| E2E | Tester | `test-repo/e2e/` |
| Regression | Tester | `test-repo/regression/` |

> The Tester **does not run E2E** until Backend and Frontend have passed their own tests.

---

## Getting started

### 1. Clone this repo
```bash
git clone https://github.com/your-username/AI-Agents.git
cd AI-Agents
```

### 2. Create your project context
```bash
cp projects-memories/context_example.md projects-memories/{your-project}/context.md
# Fill it in with your stack, rules, and project description
```

### 3. Configure MCP servers
```bash
# Edit mcp/config.json and replace the placeholders:
# TU_USUARIO, TU_GITHUB_TOKEN, TU_BRAVE_API_KEY, etc.
```

### 4. Start using the agents
Feed each agent its role file + your project's context.md.
The Scrum Master will generate `tasks.json` and `progress.json` on the first session.

---

## What you need

- API Key from at least one provider:
  - [Anthropic (Claude)](https://console.anthropic.com/)
  - [OpenAI (GPT)](https://platform.openai.com/)
  - [Google (Gemini)](https://aistudio.google.com/)
- Node.js 18+
- Your project repositories already created locally

> **Note:** A Claude Pro / ChatGPT Plus subscription is different from an API Key. To use these agents programmatically you need the **API Key**, not the web subscription.

---

## Roadmap

| Component | Status |
|---|---|
| `roles/` | ✅ Done |
| `prompts/` | 🟡 Built from real usage |
| `projects-memories/` | ✅ Template ready |
| `mcp/` | ✅ Done |
| `orchestrator/` | 🔜 Coming soon |
| `agents/*.ts` | 🔜 Coming soon |

---

## License

MIT — see [LICENSE](./LICENSE) for details.
