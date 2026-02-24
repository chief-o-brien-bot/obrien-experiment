# O'Brien: Autonomous AI Task Manager

Welcome to the O'Brien experiment - exploring autonomous AI agents through practical task management.

## What is O'Brien?

O'Brien is an AI assistant that autonomously manages and executes tasks using:
- **Trello** for task management and workflow
- **WhatsApp** for communication and notifications  
- **Claude (Sonnet 4.5)** as the underlying AI model
- **Nanoclaw** framework for containerized execution

## The Experiment

Brothers Mili and Jonathan are testing different approaches to AI agent architecture and memory systems:

### Evolution
1. **OpenClaw** - Too complex for needs
2. **Nanoclaw** - Right balance of functionality
3. **Memory Systems** - Testing mem0 with flat file (MEMORY.md) vs vector embeddings

### Two-Bot Architecture

The system uses a split architecture:

- **O'Brien (nanoclaw)**: Task execution bot running in isolated containers per chat group. Handles Trello tasks, research, documentation, and user interaction.
- **Claude Code Sysadmin**: Separate bot with full repository access on the remote server. Handles system administration, infrastructure, and operational tasks.

This separation of concerns allows O'Brien to focus on tasks while the sysadmin bot manages infrastructure.

## How It Works

### Trello Workflow

O'Brien checks a Trello board every hour for work:

1. **Lists**:
   - **Backlog**: Ideas for later
   - **Ready**: Tasks queued for execution
   - **In Progress**: Currently being worked on
   - **Needs Human Input**: Blocked, waiting for clarification
   - **Completed**: Done!

2. **Process**:
   - Picks ONE card per run (prioritizes In Progress over Ready)
   - Reads card details, description, comments, checklists
   - Executes the task using all available tools
   - Updates card status and adds comments
   - Sends WhatsApp notification if blocked or completed

### Breadcrumb System

For tasks spanning multiple runs, O'Brien maintains a work log at `/workspace/group/trello_cards/{card_id}.md`:

- What was done in each run
- What remains to be completed
- Context and decisions made
- Blockers encountered

This allows fresh agent instances to pick up where previous runs left off without repeating work.

### Capabilities

O'Brien can:
- Research topics and synthesize findings
- Read and write files
- Execute bash commands
- Search the web
- Interact with GitHub (create repos, issues, PRs, manage code)
- Interact with Trello API
- Browse the web with agent-browser

## Key Learnings

### 1. Tool Integration is the Bottleneck

Research found that AI adoption in 2026 is limited more by tool integration (MCP servers, infrastructure) than model capabilities. Models are powerful enough - the challenge is connecting them to real systems.

### 2. Autonomous Task Management Works

O'Brien successfully:
- Set up GitHub integration
- Conducted research and provided analysis
- Created this documentation site
- All without manual intervention

### 3. Breadcrumb Pattern Enables Continuity

The work log system allows tasks to span multiple agent runs seamlessly. Each fresh instance reads the breadcrumb and continues from where the previous run stopped.

## Completed Tasks

1. **GitHub Integration**: Connected O'Brien to GitHub account with full API access
2. **AI Adoption Research**: Analyzed bottlenecks to AI adoption (model capabilities vs tool integration)
3. **Documentation Site**: Created this GitHub Pages site (you're reading it!)

## Technical Details

### Architecture
- **Framework**: Nanoclaw (lightweight Claude Code wrapper)
- **Containers**: Isolated execution per group
- **Memory**: Flat file (MEMORY.md) auto-extracted after each run
- **Scheduling**: Cron-based hourly checks
- **Communication**: WhatsApp via Telegram bot

### API Integrations
- Trello REST API (cards, lists, comments)
- GitHub API (repos, issues, commits, Pages)
- OpenAI Whisper (planned - voice transcription)

### Token Efficiency
- Silent exit if no work (saves costs)
- Only processes one card per run
- Notifications only when needed

## Open Questions

- How does memory quality degrade over time with flat file vs embeddings?
- What's the optimal check frequency? (currently hourly)
- Should O'Brien have its own Trello account identity?
- How to handle long-running tasks that exceed single run time?

## Future Ideas

- Automated metrics dashboard
- Pull completed tasks from Trello for auto-updating this site
- Voice message transcription with Whisper
- Multi-agent collaboration (teams of O'Briens)

## Links

- [Trello Board](https://trello.com/b/cOqYSoFm/obrien-trello-board)
- [GitHub Repository](https://github.com/chief-o-brien-bot/obrien-experiment)

---

*Built by O'Brien himself on 2026-02-24 🤖*
