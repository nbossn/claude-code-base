# Claude Code Base

A comprehensive, unified Claude Code configuration repository combining best practices from several Claude Code orchestration systems. It is recommended to pick & choose what is relevant to your scope and use-case.

## Description

Claude Code Base is an all-in-one configuration package for Claude Code that includes:

- **199+ Skills** - Workflow automation for coding standards, testing, security, deployment, and domain-specific tasks
- **40+ Commands** - Slash commands for quick access to common operations
- **Hooks** - Automated workflow triggers for continuous learning and optimization
- **Rules** - Coding standards for TypeScript, Python, Go, Swift, and more
- **Agents** - Specialized sub-agents for planning, coding, reviewing, security, and more
- **MCP Configurations** - Model Context Protocol server setups
- **Plugin System** - Full plugin infrastructure for extensibility

## Quick Start

### Prerequisites

- Claude Code installed (`npm install -g @anthropic-ai/claude-code`)
- Node.js 18+
- Git

### macOS (Apple Silicon / Intel)

macOS is fully supported. Install prerequisites with [Homebrew](https://brew.sh):

```bash
# Install Homebrew if not already installed
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install Node.js 20+ via nvm (recommended)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.zshrc   # or ~/.bash_profile
nvm install 20 && nvm use 20

# Or via Homebrew
brew install node

# Install Claude Code CLI
npm install -g @anthropic-ai/claude-code
```

> **Note for Apple Silicon (M1/M2/M3):** All Node.js tooling runs natively via arm64. No Rosetta 2 needed for this project.

### Linux / WSL2

Standard Linux prerequisites apply. See the Installation section below.

### Installation

> **If `~/.claude/` already exists** (i.e., Claude Code is already configured), use the
> [Selective Installation](#selective-installation) steps instead of cloning into `~/.claude/` directly.

```bash
# Clone the repository
git clone https://github.com/nbossn/claude-code-base.git ~/.claude/

# Install dependencies
cd ~/.claude
npm install

# Run the setup script (installs rules for one or more languages)
./install.sh typescript python
```

### Basic Usage

```bash
# Use a skill
/skill-name

# Use a command
/command-name

# Trigger an agent
@agent-type task description

# Run a hook manually
claude hook run hook-name
```

## Tools with Usage Examples

### Skills

Skills are comprehensive workflow definitions. Use `/skill-name` to invoke:

```bash
# Development workflows
/tdd              # Test-driven development
/code-review      # Code review process
/refactor-clean   # Clean up dead code

# Specialized domains
/security-review  # Security analysis
/api-design       # REST API design patterns
/postgres-patterns # PostgreSQL optimization

# Advanced agents
/sparc-methodology # SPARC implementation
/swarm-orchestration # Multi-agent coordination
/v3-performance-optimization # Performance tuning
```

### Commands

Slash commands for quick actions:

```bash
/plan             # Create implementation plan
/eval             # Run evaluation harness
/claw             # Start NanoClaw session
/projects         # List known projects
/learn            # Extract patterns from session
/promote          # Promote instincts globally
/model-route      # Route task to optimal model
/verify           # Run verification checks
```

### Agents

Specialized sub-agents for delegation:

```bash
@planner          # Create detailed implementation plans
@coder            # Write clean, efficient code
@reviewer         # Comprehensive code review
@security-reviewer # Security vulnerability detection
@tester           # Generate and run tests
@architect        # System design and architecture
@researcher       # Deep research and analysis
@performance-engineer # Performance optimization
```

### Hooks

Automated triggers:

- `pre-task` - Before task execution
- `post-task` - After task completion
- `pre-edit` - Before file edits
- `post-edit` - After file modifications
- `session-end` - Before session closes
- `auto-tmux-dev` - Development environment setup
- `learn-eval` - Pattern extraction

### Rules

Language-specific coding standards:

- `rules/typescript/` - TypeScript best practices
- `rules/python/` - Pythonic idioms
- `rules/golang/` - Go patterns
- `rules/swift/` - Swift conventions
- `rules/common/` - Language-agnostic rules

## Installation

### Full Installation

```bash
# 1. Clone repository
git clone https://github.com/nbossn/claude-code-base.git ~/.claude

# 2. Navigate to directory
cd ~/.claude

# 3. Install dependencies
npm install

# 4. Run installer (specify one or more languages)
./install.sh typescript python

# 5. Configure Claude Code
# Edit ~/.claude/settings.json as needed
```

### Selective Installation

Use this approach when `~/.claude/` already exists (Claude Code is already set up):

```bash
# Clone to a local directory (not ~/.claude/ directly)
git clone https://github.com/nbossn/claude-code-base.git ~/claude-code-base
cd ~/claude-code-base

# Install npm dependencies
npm install

# Install rules for your language(s)
./install.sh typescript python golang swift

# Copy skills, commands, and agents into your existing ~/.claude/
cp -r skills ~/.claude/skills
cp -r commands ~/.claude/commands
cp -r agents ~/.claude/agents
```

> **macOS tip:** The above selective approach is recommended when Claude Code is
> already installed, since `~/.claude/` will already contain your settings,
> sessions, and other Claude Code data.

### MCP Server Setup

```bash
# Copy MCP configurations
cp mcp-configs/mcp-servers.json ~/.claude/mcp-servers.json

# Edit with your API keys
nano ~/.claude/mcp-servers.json
```

## Token Optimization

Claude Code Base includes multiple strategies for optimizing token usage:

### 1. Strategic Compaction

Use `/compact` at strategic points:

```bash
/compact After completing research phase
```

Best practice: Compact after:
- Research → Planning transition
- Planning → Implementation transition
- Debugging → Next feature

### 2. Model Routing

Route tasks to appropriate model tiers:

```bash
/model-route complexity:low   # Uses Haiku (fast, cheap)
/model-route complexity:medium # Uses Sonnet
/model-route complexity:high   # Uses Opus (deep reasoning)
```

| Tier | Model | Latency | Cost | Use Case |
|------|-------|---------|------|----------|
| 1 | Agent Booster | <1ms | $0 | Simple transforms |
| 2 | Haiku | ~500ms | $0.0002 | Simple tasks |
| 3 | Sonnet | 2-3s | $0.003 | Complex coding |
| 4 | Opus | 3-5s | $0.015 | Deep reasoning |

### 3. Context Management

```bash
# Use memory for persistence
claude memory store --key "pattern-X" --value "description"

# Search memory before asking
claude memory search --query "auth patterns"
```

### 4. Instinct-Based Learning

Extract and reuse patterns:

```bash
/learn              # Extract patterns from session
/instinct-export    # Export to file
/instinct-import    # Import from file
```

### 5. Swarm Coordination

For large tasks, use agent swarms to parallelize:

```bash
# Initialize swarm
npx @claude-flow/cli@latest swarm init

# Spawn workers
npx @claude-flow/cli@latest agent spawn -t coder -c 4
```

## Configuration Files

| File | Purpose |
|------|---------|
| `CLAUDE.md` | Main configuration |
| `CLAUDE.local.md` | Local overrides |
| `settings.json` | Claude Code settings |
| `mcp-servers.json` | MCP server configs |
| `hooks.json` | Hook definitions |

## Directory Structure

```
claude-code-base/
├── .claude/           # Claude Code config
│   ├── agents/       # Agent definitions
│   ├── commands/     # Slash commands
│   ├── skills/       # Skill definitions
│   └── config/       # Configuration
├── .claude-plugin/   # Plugin system
│   ├── hooks/        # Plugin hooks
│   └── scripts/      # Plugin scripts
├── skills/           # 199+ skills
├── commands/         # 40+ commands
├── hooks/            # Automation hooks
├── rules/            # Coding standards
├── agents/           # Agent YAML configs
├── scripts/         # Setup scripts
├── mcp-configs/     # MCP server configs
└── install.sh       # Installation script
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Add your skill/command/rule
4. Submit a pull request

## License

MIT

## Credits

Built from:
- [everything-claude-code](https://github.com/affaan-m/everything-claude-code)
- [ruflo](https://github.com/ruvnet/ruflo)

## Support

- Issues: https://github.com/nbossn/claude-code-base/issues
- Documentation: See individual skill/command READMEs
