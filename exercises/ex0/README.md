# Getting Started - Session Overview

Welcome to **XP162 - Beyond the Cockpit: Manage BTP Through Conversation with AI Agents**!

This page provides an overview of the session, explains the technology you'll use, and helps you verify you're ready to start the exercises.

## Session Overview

This hands-on session will fundamentally change how you think about BTP administration. Instead of clicking through web interfaces, you'll use **natural language conversations** to manage your BTP landscape.

###The Journey: From Clicks to Conversations

```
BTP Cockpit (Traditional)  →  AI Agent + MCP (Conversational)
        ↓                              ↓
   Manual Navigation              Natural Language
   Multiple Clicks                Single Prompts
   Sequential Tasks               Parallel Operations
   Rigid UI                       Flexible Queries
```

## What You'll Experience

### Exercise 1: The Baseline (15-20 minutes)
**Traditional BTP Cockpit Administration**

You'll log into BTP Cockpit as a test user and perform typical administrative tasks:
- Navigate through global accounts and subaccounts
- Manually discover your permissions
- Try to answer questions like "Which users have never logged in?"

**Key Insight**: You'll spend 10-15 minutes clicking through pages to gather basic information — highlighting the inefficiency of UI-based administration.

---

### Exercise 2: The Transformation (30-35 minutes)
**Your First BTP MCP Experience**

You'll set up Claude Code CLI and connect it to the BTP MCP Server:
- Configure and authenticate the MCP server
- Ask the **same questions from Exercise 1** in natural language
- Get comprehensive answers in seconds instead of minutes

**Key Insight**: Tasks that took 10+ minutes of clicking now take 10 seconds of typing.

---

### Exercise 3: Administrator Workflows in UI (10-15 minutes)
**Understanding Workflow Complexity**

With a Global Account Administrator user, you'll:
- Grant yourself access to locked subaccounts (multiple clicks per subaccount)
- Create a service subscription through a 30+ step workflow
- Navigate across 3 levels (Global Account → Subaccount → Users)

**Key Insight**: Even with administrator privileges, complex workflows require extensive clicking and careful attention to avoid errors.

---

### Exercise 4: Administrator Workflows with AI (30-35 minutes)
**The Ultimate Transformation**

You'll perform the **exact same workflows from Exercise 3**, but with BTP MCP:
- Grant access to multiple subaccounts in one prompt
- Create complete service subscriptions with a single multi-line prompt
- Experience 10-15x efficiency gains

**Key Insight**: 30+ manual steps become 1 prompt. 15 minutes becomes 30 seconds.

---

## Technology Introduction

### What is MCP?

**Model Context Protocol (MCP)** is an open protocol that standardizes how applications provide context to Large Language Models (LLMs).

Think of it as a universal adapter that lets AI agents interact with any system:

```
┌─────────────────┐
│   AI Agent      │  (Claude Code CLI)
│   (LLM Brain)   │
└────────┬────────┘
         │
         │ MCP Protocol
         │ (Standardized Communication)
         │
┌────────▼────────┐
│   MCP Server    │  (BTP MCP Server)
│   (58+ Tools)   │
└────────┬────────┘
         │
         │ BTP APIs
         │
┌────────▼────────┐
│  SAP BTP        │  (Your BTP Landscape)
│  Platform       │
└─────────────────┘
```

### The MCP Server for SAP BTP Administration

This specialized MCP server exposes **58+ administrative tools** across 4 domains:

| Domain | Tools | Examples |
|--------|-------|----------|
| **Accounts** | 15 | List Global Accounts, Create Subaccounts, Assign Entitlements |
| **Security** | 20 | List Users, Create Role Collections, Assign Roles |
| **Services** | 15 | List Subscriptions, Create Service Instances |
| **Connectivity** | 8 | List Destinations, Create Destinations |

Each tool is a function the AI agent can call to interact with BTP — reading data, creating resources, or modifying configurations.

### Claude Code CLI

**Claude Code** is an AI-powered command-line interface from Anthropic that can:
- Understand natural language instructions
- Execute complex multi-step tasks
- Connect to external systems via MCP servers
- Reason about problems and make decisions

In this session, Claude Code acts as your intelligent assistant for BTP administration.

---

## Lab Environment

### Your Test Users

You will receive **two** test user accounts for this session:

#### User 1: Custom IdP User (Exercises 1-2)
- 📧 **Email**: `teched.xp162.<NN>@education.cloud.sap`
- 🔑 **Password**: `xp162.<NN>...`
- 🏢 **Identity Provider**: Custom IdP (`aju4hpp6l.accounts.ondemand.com`)
- 👤 **Role**: Global Account Viewer
- 🎯 **Purpose**: Experience read-only queries and basic navigation

#### User 2: SAP ID Service User (Exercises 3-4)
- 📧 **Email**: `jens.glander+teched.edu.<NN>@sap.com`
- 🔑 **Password**: `xp162.<NN>...`
- 🏢 **Identity Provider**: SAP ID Service (default IdP)
- 👤 **Role**: Global Account Administrator
- 🎯 **Purpose**: Perform write operations and administrative workflows

> 💡 **Why Two Users?** This simulates a realistic enterprise scenario where you might have different accounts with different privilege levels across various BTP landscapes.

### Your BTP Account Access

Both users are assigned to global account: **`SAP_TechEd_2026_XP162_<NN>`**

| User | Global Account Role | Subaccount Access | Capabilities |
|------|---------------------|-------------------|--------------|
| **User 1** | Global Account Viewer | 10 accessible (out of 100) | Read-only queries |
| **User 2** | Global Account Administrator | 5 accessible (out of 10 initially) | Full administrative operations |

---

## Prerequisites Check

Before starting Exercise 1, verify you have everything ready:

### ✅ Session Materials
- [ ] Participant number `<NN>` received from instructor
- [ ] Test user 1 credentials (Custom IdP)
- [ ] Test user 2 credentials (SAP ID Service)
- [ ] Access to TechEd lab machine

### ✅ Software Installed
- [ ] Google Chrome browser
- [ ] Visual Studio Code
- [ ] Claude Code CLI
- [ ] PowerShell terminal (Windows)

### ✅ Quick Software Verification

Run these commands in PowerShell to verify installations:

```powershell
# Check Claude Code CLI
claude --version

# Check VS Code
code --version

# Check Chrome (check Start menu)
# Look for Google Chrome application
```

Expected results:
- `claude --version` should show version information
- `code --version` should show VS Code version
- Chrome should be available in Start menu

---

## Understanding the Efficiency Gains

Here's what you'll experience quantitatively:

### Time Savings

| Task | Traditional UI | AI + MCP | Time Saved |
|------|----------------|----------|------------|
| Find user permissions | 5-10 minutes | 10 seconds | **95%+** |
| Grant subaccount access (4 subaccounts) | 8 minutes | 30 seconds | **93%** |
| Create service subscription | 10-15 minutes | 30-60 seconds | **90%+** |
| List inactive users across subaccounts | 15-20 minutes | 15 seconds | **98%** |

### Complexity Reduction

| Workflow | UI Steps | MCP Prompts | Reduction |
|----------|----------|-------------|-----------|
| Grant access to subaccounts | 8-10 steps × 4 subaccounts | 1 prompt | **97%** |
| Create subscription workflow | 30+ steps | 1 multi-line prompt | **97%** |
| User permission audit | Navigate × 10 subaccounts | 1 prompt | **100%** |

---

## Session Tips for Success

### 💡 Best Practices

1. **Follow the sequence**: Each exercise builds on the previous one
2. **Take your time in Exercise 1**: Understanding the baseline is crucial
3. **Pay attention to timings**: Note how long tasks take in Cockpit vs. MCP
4. **Experiment**: Try your own prompts after completing scripted ones
5. **Ask questions**: Session facilitators are here to help

### ⚠️ Common Pitfalls to Avoid

- ❌ **Skipping Exercise 1**: The baseline experience is crucial for comparison
- ❌ **Typos in credentials**: Double-check email and password — wrong credentials can lock accounts
- ❌ **Not using Administrator PowerShell**: Required for proper permissions
- ❌ **Rushing through tool permissions**: Understand what you're approving in Claude Code
- ❌ **Mixing up the two users**: Use the correct user for each exercise!

### 🎯 What to Focus On

- **Time savings**: Note how long tasks take in Cockpit vs. Claude Code
- **Information aggregation**: See how AI combines data from multiple sources
- **Natural language flexibility**: Observe how different phrasings produce similar results
- **Error handling**: Watch how the AI responds to ambiguous requests
- **Cognitive load reduction**: Feel the difference between navigating vs. asking

---

## Frequently Asked Questions

### About the Technology

**Q: Is this production-ready?**  
A: Yes! The MCP Server for SAP BTP Administration is available now and can be used with production BTP accounts (with proper authorization and testing).

**Q: Does this work with my existing BTP accounts?**  
A: Yes. The MCP server works with any BTP global account you have access to, including custom Identity Providers.

**Q: What permissions does the MCP server need?**  
A: It uses YOUR credentials and YOUR permissions. The MCP server can only do what you're already authorized to do in BTP.

**Q: Is my data secure?**  
A: Yes. Data flows: Your BTP → MCP Server → AI Agent (in your session). SAP controls the MCP server, and you control what tools the AI can use.

### About the Session

**Q: Do I need AI or programming experience?**  
A: No! This session is designed for BTP administrators. If you can use BTP Cockpit, you can use this.

**Q: Can I use this with my own BTP account?**  
A: Not during the session (we provide test accounts), but absolutely afterward! Documentation links are provided.

**Q: Will I get the exercise materials?**  
A: Yes. All materials including step-by-step guides, prompts, and screenshots are available in this repository.

---

## Ready to Start?

You now understand:
- ✅ What you'll experience in each exercise
- ✅ The technology behind conversational BTP administration
- ✅ Your lab environment and test users
- ✅ The efficiency gains you'll achieve
- ✅ Tips for success

**Let's begin the transformation!**

Continue to [Exercise 1 - Exploring BTP Accounts with BTP Cockpit](../ex1/README.md)

---

## Additional Resources

- **SAP Help Portal**: [MCP Server for SAP BTP Administration](https://help.sap.com/docs/btp/sap-business-technology-platform/mcp-server-for-sap-btp-administration)
- **Claude Code**: [Claude.ai/code](https://claude.ai/code)
- **Model Context Protocol**: [modelcontextprotocol.io](https://modelcontextprotocol.io)
- **Session Repository**: [github.com/SAP-samples/teched2026-XP162](https://github.com/SAP-samples/teched2026-XP162)
