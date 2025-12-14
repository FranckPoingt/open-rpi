# OpenCode Agent System

A refined 7-agent RPI (Research → Plan → Implement) system for OpenCode with Beads integration and Kit MCP.

## Pre-requisites

- OpenCode CLI installed
- Beads installed
- Kit MCP installed

## Goal

Deliver high-quality code with minimal scope and context creep, leveraging Kit MCP for context and Beads for memory.

## Disclaimer

There is no one-size-fits-all agent system. This is a starting point that you can customize further based on your projects and workflows.
There are many possible improvements and variations. Feel free to experiment and adapt the system to your needs and suggest improvements.

I am keen to hear your feedback and ideas! Please open issues so we can improve this together.

## Features

- **Anti-Gold-Plating**: Architect enforced to stick to requirements only
- **Pragmatic Reviews**: Critic rejects only serious issues (max 2 iterations)
- **User Approval Gate**: Review plans before Bead creation
- **Kit MCP**: All agents leverage codebase context before external resources
- **Clear Role Separation**: Manager orchestrates, Architect creates Beads, Builders implement

## Agents

### Primary Agent

- **Manager** - Orchestrates the RPI loop, presents plans to user for approval

### Research & Planning

- **Researcher** - Maps internal (Kit) and external context to research.md
- **Architect** - Drafts minimal plans, searches Kit for patterns, creates Beads
- **Critic** - Pragmatic plan reviewer (focuses on serious issues only)

### Implementation

- **Frontend Builder** - UI/UX specialist (Gemini 3 Pro)
- **Backend Builder** - API/DB/Logic specialist (Claude Sonnet 4.5)
- **Verifier** - QA validation against plan and codebase patterns

## Workflow

```
Phase 1: Planning
Manager → Researcher (Kit-first) → .opencode/packet/research.md
       → Architect (no gold-plating, Kit patterns) → .opencode/packet/plan.md
       → Critic (pragmatic, max 2 rejections) → APPROVED/REJECTED
       → Manager → USER REVIEW (new gate)
       → Architect → bd create

Phase 2: Execution
Manager → Frontend/Backend Builder (Kit patterns) → DONE
       → Verifier (Kit compliance + tests) → APPROVED
       → bd close
```

## Installation

1. Copy the `agent/` folder to `~/.config/opencode/agent/`
2. Copy `opencode.jsonc` to `~/.config/opencode/opencode.jsonc`
3. Ensure Kit MCP server is configured (see opencode.jsonc)

## Key Improvements Over Default

1. **Architect constrained** - "CRITICAL RULES" prevent scope creep
2. **Reduced chatter** - Critic max 2 rejections before user escalation
3. **User in the loop** - Approve plans before implementation starts
4. **Kit MCP maximized** - All agents search codebase first
5. **Clear permissions** - Manager can't create Beads (only Architect can)

## Requirements

- OpenCode (https://opencode.ai)
- Kit MCP server (cased-kit)
- Beads (https://github.com/steveyegge/beads)
- API keys for the models you choose to use

## Model Selection

- **Manager**: Claude Haiku 4.5 (lightweight orchestration)
- **Researcher**: Grok Code Fast 1 (fast code analysis)
- **Architect**: Claude Opus 4.5 (complex planning)
- **Critic**: GPT-5.2 (evaluation/review)
- **Frontend Builder**: Gemini 3 Pro Preview (UI specialization)
- **Backend Builder**: Claude Sonnet 4.5 (API/logic)
- **Verifier**: Grok Code Fast 1 (fast validation)

## Usage

Each project should have an `AGENTS.md` file in the root with:

- Tech stack
- Coding conventions
- Testing strategy
- Project-specific guidelines

Agents will read this file to understand project context.

## Credits

Built on:

- [OpenCode](https://opencode.ai) - open source coding agent
- [Beads](https://github.com/steveyegge/beads) - Steve Yegge's memory system for coding agents
- [Kit](https://github.com/cased/kit) - Cased's codebase context server
