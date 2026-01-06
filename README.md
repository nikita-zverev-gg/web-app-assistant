# GoGlobal Assistant Plugin

Development assistant for GoGlobal projects with TDD workflow, specialized agents, and development guidelines.

## Features

### Agents
- **Developer** - Implementation specialist using TDD
- **Reviewer** - Quality verification specialist

### Skills
- **E2E Testing** - Playwright patterns for BPO/EOR applications
- **Code Elevation** - Startup to enterprise code patterns

### Commands
- `/implement` - Execute TDD workflow for feature implementation

### Rules (Always Loaded)
- Ground rules and zero-assumptions principle
- Workflow management and rollback strategies
- TypeScript code standards
- E2E testing patterns
- BPO-specific: permissions, migrations

## Installation

### Option 1: Test Locally
```bash
claude --plugin-dir /path/to/goglobal-assistant-plugin
```

### Option 2: Install to Project (Recommended for Teams)
```bash
claude plugin install goglobal-assistant --scope project
```

### Option 3: Install to User Scope
```bash
claude plugin install goglobal-assistant --scope user
```

## Usage

Once installed, the plugin components are automatically available:

1. **Agents** are discoverable via the Task tool
2. **Skills** are auto-discovered by description match
3. **Commands** are invoked with `/command-name`
4. **Rules** are always loaded as high-priority instructions

## Distribution

### Via Git Repository
Push this plugin to a Git repo and install:
```bash
claude plugin install goglobal-assistant@github:your-org/goglobal-assistant-plugin
```

### Via Marketplace
Create a `marketplace.json`:
```json
{
  "plugins": [
    {
      "name": "goglobal-assistant",
      "description": "GoGlobal development assistant",
      "source": "./goglobal-assistant-plugin",
      "version": "1.0.0"
    }
  ]
}
```

Then add the marketplace:
```bash
claude plugin marketplace add https://your-host/marketplace.json
```

## Requirements

- Claude Code version 1.0.33 or later
