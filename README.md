# AdonisJS v7 Agent Skill

A comprehensive agent skill for AI coding assistants (Claude Code, OpenCode, Codex, etc.) that provides complete knowledge of AdonisJS v7 framework.

## Description

This skill enables AI agents to effectively work with AdonisJS v7 projects by providing:
- Complete documentation references (107+ topics)
- Code examples for all core features
- Project structure conventions
- Best practices and patterns
- Migration guidance from v5/v6

## When to Use This Skill

Use this skill when working with:
- Building new AdonisJS v7 applications
- Debugging existing AdonisJS applications
- Implementing features (routing, auth, models, etc.)
- Understanding AdonisJS v7 capabilities
- Upgrading from AdonisJS v5/v6
- Learning AdonisJS framework

## Features

- **107+ documentation topics** covered
- **Full documentation links** to https://docs.adonisjs.com/
- **Code examples** for all major features
- **Project structure** reference
- **Key packages** with docs links
- **Services reference** with import paths
- **Best practices** for AdonisJS development
- **Migration guide** from v5/v6

## Quick Reference

| Topic | Link |
|-------|------|
| Routing | https://docs.adonisjs.com/guides/basics/routing |
| Controllers | https://docs.adonisjs.com/guides/basics/controllers |
| Models (Lucid) | https://docs.adonisjs.com/guides/database/lucid |
| Authentication | https://docs.adonisjs.com/guides/auth/introduction |
| Validation | https://docs.adonisjs.com/guides/basics/validation |
| Middleware | https://docs.adonisjs.com/guides/basics/middleware |
| Testing | https://docs.adonisjs.com/guides/testing/introduction |
| Deployment | https://docs.adonisjs.com/start/deployment |

## Installation

### Option 1: From skills.sh (recommended)
```bash
npx skills add kamranallahyar/adonisjs-v7-agent-skill
```

### Option 2: Manual installation
1. Clone this repository or download SKILL.md
2. Place SKILL.md in your agent's skills directory:
   - Claude Code: `~/.claude/skills/adonisjs-v7-agent/`
   - OpenCode: `.claude/skills/adonisjs-v7-agent/`

### Option 3: Direct import
Copy the SKILL.md content directly into your AI assistant.

## Topics Covered

### Basics
- Routing, Controllers, Middleware, Validation
- Request, Response, Session, HTTP Context
- Body Parser, File Uploads, Exception Handling
- Static Files, URL Builder, Debugging

### Authentication
- Introduction, Session Guard, Access Tokens Guard
- Basic Auth Guard, Custom Auth Guard
- Authorization (Bouncer), Social Authentication

### Database
- Lucid ORM, Migrations, Relationships
- Redis Client

### Security
- Hashing, Encryption, Rate Limiting
- CORS, Securing SSR Applications

### Testing
- Introduction, API Tests, Browser Tests
- Console Tests, Test Doubles, Resetting State

### Frontend
- Vite Integration, Edge Templates
- Inertia, TanStack Query, API Client, Transformers

### Digging Deeper
- Logger, Cache, Queues, Mail, Drive
- Event Emitter, Atomic Locks, Health Checks
- Server-Sent Events (Transmit), i18n, OpenTelemetry

### Concepts
- Service Providers, Dependency Injection
- Container Services, Application Lifecycle
- Barrel Files, Scaffolding, Extending AdonisJS

### Ace CLI
- Introduction, Creating Commands
- Arguments, Flags, Prompts, TUI, REPL

### Reference
- Application, Commands, Events, Exceptions
- Helpers, String Helpers, Types Helpers
- Edge, adonisrc_file, Config files

## Compatible With

- Claude Code
- OpenCode
- Codex
- Any Claude-based AI coding assistant

## Documentation

All references point to the official AdonisJS documentation:
- **Base URL:** https://docs.adonisjs.com/
- **Official Docs:** https://docs.adonisjs.com/

## License

MIT License - See LICENSE file for details.

## Contributing

Contributions welcome! Please open an issue or submit a PR.

## Support

- Official Docs: https://docs.adonisjs.com/
- AdonisJS Discord: https://discord.gg/vDcEjq6
- GitHub Issues: https://github.com/adonisjs/core/issues