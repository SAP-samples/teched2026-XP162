# XP162 - Beyond the Cockpit: Manage BTP Through Conversation with AI Agents

[![REUSE status](https://api.reuse.software/badge/github.com/SAP-samples/teched2026-XP162)](https://api.reuse.software/info/github.com/SAP-samples/teched2026-XP162)

## Description

This repository contains the material for the SAP TechEd 2026 session **XP162 - Beyond the Cockpit: Manage BTP Through Conversation with AI Agents**.

Experience SAP Business AI Platform in action: Transform BTP administration through natural conversations in agentic tools connected to the new MCP Server for SAP BTP Administration. Manage complex accounts, security, and service-related tasks using simple language instead of navigating the rigid BTP Cockpit.

## Overview

This hands-on session will fundamentally change how you think about BTP administration. Instead of clicking through web interfaces, you'll use **natural language conversations** to manage your BTP landscape.

**Session XP162** explores how BTP administration transforms when you move from a web UI to natural language — using the **MCP Server for SAP BTP Administration** connected to an **agentic tool** (Claude Code CLI).

### The Journey: From Clicks to Conversations

The exercises follow a deliberate progression designed to help you directly experience the transformation:

```
BTP Cockpit (Traditional)  →  AI Agent + MCP (Conversational)
        ↓                              ↓
   Manual Navigation              Natural Language
   Multiple Clicks                Single Prompts
   Sequential Tasks               Parallel Operations
   Rigid UI                       Flexible Queries
```

### What You'll Learn

By the end of this session, you will:

✅ **Understand the limitations** of traditional UI-based BTP administration  
✅ **Experience AI-powered administration** through the MCP Server for SAP BTP Administration  
✅ **Master conversational interfaces** for complex administrative tasks  
✅ **Gain practical skills** in using Claude Code CLI with BTP MCP  
✅ **Discover new possibilities** for automating and streamlining your BTP workflows

### Why This Matters: The Business Case

**Traditional BTP Administration Challenges:**
- 🕐 Admins spend 40-60% of time just navigating UIs
- 📊 Data scattered across multiple pages and levels
- ❌ Copy-paste mistakes, missed steps in procedures
- 🔄 Same clicks every time for routine tasks

**The MCP Server + AI Agent Solution:**
- ⚡ **10x Faster Queries** - Single prompts replace multi-step navigation
- 🎯 **Contextual Intelligence** - AI understands intent and finds right information
- 📊 **Aggregated Insights** - Cross-subaccount views in seconds
- 📚 **Self-Documenting** - Prompts ARE the documentation

## Requirements

To complete the exercises in this repository, you need:

### Provided by Session Organizers
- Test user credentials (2 sets - custom IdP and SAP ID Service)
- Participant number `<NN>` (e.g., 00, 01, 02...)
- Access to TechEd lab machine (Windows with PowerShell)

### Pre-installed Software
- Google Chrome browser
- Visual Studio Code
- Claude Code CLI
- PowerShell (with Administrator access)

### Knowledge Prerequisites
- Basic understanding of SAP BTP concepts (global accounts, subaccounts, users)
- Familiarity with BTP Cockpit (helpful but not required)
- Comfort with command-line interfaces (basic level)
- **No AI or programming experience required!**

## Exercises

The exercises are designed to provide a progressive learning experience, from traditional UI-based administration to AI-powered conversational interfaces:

- **[Getting Started](exercises/ex0/)** - Session overview, prerequisites, and technology introduction
- **[Exercise 1 - Baseline: Exploring BTP with Cockpit](exercises/ex1/)** - Experience traditional UI-based administration
  - Navigate BTP Cockpit with custom IdP authentication
  - Discover permissions and roles manually
  - Document time and effort for basic tasks
- **[Exercise 2 - Transformation: First BTP MCP Setup](exercises/ex2/)** - Set up Claude Code CLI with BTP MCP
  - Configure and authenticate BTP MCP Server
  - Execute read-only queries with natural language
  - Compare efficiency: prompts vs. clicks
- **[Exercise 3 - Administrator Capabilities with Cockpit](exercises/ex3/)** - Experience complex administrative workflows in UI
  - Use Global Account Administrator privileges
  - Perform multi-step subscription creation (30+ steps)
  - Understand workflow complexity and time investment
- **[Exercise 4 - Administrative Workflows with BTP MCP](exercises/ex4/)** - Transform workflows with conversational AI
  - Configure second BTP MCP with SSO authentication
  - Execute write operations through natural language
  - Perform 30+ step workflows in single prompts
  - Experience 10-15x efficiency gains

### Estimated Time

- **Total session duration**: 90 minutes
- **Exercise 0**: 5 minutes (overview and setup)
- **Exercise 1**: 15-20 minutes
- **Exercise 2**: 30-35 minutes
- **Exercise 3**: 10-15 minutes
- **Exercise 4**: 30-35 minutes
- **Wrap-up & Q&A**: 10 minutes

## Technology Overview

### What is MCP?

**Model Context Protocol (MCP)** is an open protocol that standardizes how applications provide context to Large Language Models (LLMs). Think of it as a universal adapter that lets AI agents interact with any system.

### The MCP Server for SAP BTP Administration

This specialized MCP server exposes **58+ administrative tools** across 4 domains:

1. **Accounts** (15 tools): Global accounts, directories, subaccounts, entitlements
2. **Security** (20 tools): Users, roles, role collections, trust configurations
3. **Services** (15 tools): Service instances, subscriptions, service plans
4. **Connectivity** (8 tools): Destinations, connectivity configurations

Each tool is a function the AI agent can call to interact with BTP — reading data, creating resources, or modifying configurations.

## Key Metrics & Results

Participants will experience quantifiable efficiency gains:

| Metric | Traditional UI | AI + MCP | Improvement |
|--------|----------------|----------|-------------|
| **Query time** | 5-10 minutes | 10-30 seconds | **10-20x faster** |
| **Workflow steps** | 30+ manual actions | 1 prompt | **97% reduction** |
| **Error rate** | High (many click points) | Low (AI validates) | **Significant decrease** |
| **Documentation** | External guides needed | Prompts self-document | **Built-in** |

## How to obtain support

Support for the content in this repository is available during the actual time of the online session for which this content has been designed. Otherwise, you may request support via the [Issues](../../issues) tab.

## Contributing

Please read the [CONTRIBUTING.md](./CONTRIBUTING.md) to understand the contribution guidelines.

## Code of Conduct

Please read the [SAP Open Source Code of Conduct](https://github.com/SAP-samples/.github/blob/main/CODE_OF_CONDUCT.md).

## License

Copyright (c) 2026 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSE) file.
