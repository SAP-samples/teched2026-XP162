# Exercise 2 - Using BTP MCP Server with Claude Code CLI

⏱️ **Estimated time**: 30-35 minutes

## Overview

In Exercise 1, you experienced the limitations of using BTP Cockpit - navigating back and forth between pages to gather information took 10-15 minutes and was highly inefficient.

**Now experience the transformation.**

In this exercise, you'll use the **MCP Server for SAP BTP Administration** with **Claude Code CLI** to answer the same administrative questions — but in seconds instead of minutes, using natural language instead of clicking.

## Learning Objectives

By the end of this exercise, you will be able to:
- Configure and authenticate the BTP MCP Server in Claude Code CLI
- Understand the MCP architecture and authentication flow
- Use natural language prompts to query BTP account information
- Manage tool permissions in Claude Code
- Experience 10x efficiency gains compared to Exercise 1

---

## What is MCP?

**Model Context Protocol (MCP)** is an open protocol that standardizes how applications provide context to Large Language Models (LLMs).

The **MCP Server for SAP BTP Administration** exposes **58+ tools** that allow Claude Code to:
- List and manage BTP accounts, subaccounts, and directories
- Query and manage users, roles, and role collections
- Retrieve information about services, subscriptions, and destinations
- Perform administrative operations on your behalf

This makes agentic tools (here Claude Code CLI) an intelligent assistant that can interact with your BTP landscape using natural language.

---

## 1 Set up BTP MCP Server with Claude Code CLI

### 1.1 Open PowerShell Terminal

1. Click **`Start`** button on the Windows taskbar and search for **`Terminal`**

2. Right-click on **`Terminal App`** and choose **`Run as administrator`**

3. If `User Access Control` dialog opens, confirm with **Yes**

   ![Open Terminal as Administrator](./images/01_open_terminal_as_admin.png)

   ✅ **Expected Result**: An Administrator PowerShell Terminal window opens.

> [!NOTE]
> For each command in the terminal, press the return key ⏎ to execute it.

4. Create a project folder:
   ```powershell
   mkdir MyFirstBtpMcpProject
   ```

5. Navigate into the folder:
   ```powershell
   cd MyFirstBtpMcpProject
   ```
   ![Terminal as Administrator](./images/01b_terminal_as_admin.png)

---

### 1.2 Launch Claude Code CLI

1. Open Claude Code CLI:
   ```powershell
   claude
   ```
2. Press **`Enter`** ⏎ to confirm default text style (if Claude asks)
3. Read the two security notes and press **`Enter`** ⏎ to continue
4. Press **`Enter`** ⏎ again to confirm *Yes, I trust this folder*

   ✅ **Expected Result**: The Claude Code CLI interface is ready to take your first prompt.

   ![Claude Code CLI Ready](./images/02_claude_code_cli.png)

---

### 1.3 Configure BTP MCP Server

Before using the BTP MCP server, you need to:
- (1) Add the MCP configuration (1.3.2)
- (2) Set up authentication credentials (1.3.3)

We'll use VS Code to visualize the configuration.

#### 1.3.1 Open VS Code

1. Type **`exit`** and press **`Enter`** ⏎ to leave Claude:
   ```claude_cli
   exit
   ```

2. Clean up Terminal output:
   ```powershell
   clear
   ```

3. Open VS Code in the current folder:
   ```powershell
   code .
   ```

   ✅ **Expected Result**: VS Code opens showing your empty project folder.

   ![VS Code Opened](./images/04_vs_code_opened.png)

   💡 **Tip**: Place VS Code next to the Terminal window for easy switching.

#### 1.3.2 Add MCP Configuration

1. Run this command in PowerShell to add the BTP MCP configuration:

   ```powershell
   claude mcp add --transport http --scope project mcp-btp-admin-customidp "https://proxy.c-769d49e.kyma.ondemand.com/mcp" --header 'Authorization: Basic ${BTP_CREDENTIALS}' --header 'X-Platform-Origin: ${BTP_ORIGIN}'
   ```

   ✅ **Expected Result**: A `.mcp.json` file appears in your project folder (visible in VS Code).

   ![MCP Configuration Created](./images/05_vs_code_mcp_json.png)

   **What this does:**
   - Creates an MCP server configuration named `mcp-btp-admin-customidp`
   - Points to the BTP MCP server URL
   - Configures authentication to use environment variables `${BTP_CREDENTIALS}` and `${BTP_ORIGIN}`

#### 1.3.3 Set Authentication Credentials

Now you'll store your BTP credentials as environment variables.

> [!CAUTION]
> **Be very precise with email and password!** A password typo could lock your account after several failed attempts.

1. Store your BTP credentials:

   **Template** (don't run this - see example below):
   ```powershell
   $Env:BTP_CREDENTIALS = [Convert]::ToBase64String([Text.Encoding]::UTF8.GetBytes('<YOUR-TEST-USER-EMAIL>:<YOUR-TEST-USER-PASSWORD>'))
   ```

   **Example with your credentials** (adapt in e-mail '00' and in password '00xx' to your values):
   ```powershell
   $Env:BTP_CREDENTIALS = [Convert]::ToBase64String([Text.Encoding]::UTF8.GetBytes('teched.xp162.00@education.cloud.sap:xp162.00xxAcce$$'))
   ```

   ![Set BTP Credentials](./images/06_env_variable.png)

2. Verify that your stored BTP_CREDENTIALS environment variable

   ```powershell
   [Text.Encoding]::UTF8.GetString([Convert]::FromBase64String($Env:BTP_CREDENTIALS))
   ```
   ![Set BTP Credentials](./images/06b_env_variable.png)
   - Confirm output: `email` of your user before the colon 
   - Confirm output: `password` of your user after the colon 

3. Store the custom IdP origin:
   ```powershell
   $Env:BTP_ORIGIN = 'aju4hpp6l'
   ```

   ![Set BTP Origin](./images/07_env_variable.png)

4. Verify that your stored BTP_ORIGIN
   ```powershell
   $Env:BTP_ORIGIN
   ```
   ![Set BTP Origin](./images/07b_env_variable.png)
   - Confirm output: `aju4hpp6l` 

> [!NOTE]
> The two stored environment variable values live only in this Terminal session. If you close the powershell Terminal and re-open it you have to store them again to work with the `mcp-btp-admin-customidp` MCP server.

✅ **Checkpoint**: Environment variables are set. You're ready to authenticate!



---

## 1.4 Verify BTP MCP Connection

1. Launch Claude Code CLI again:
   ```powershell
   claude
   ```

2. Confirm **`Use this MCP Server`** with **`Enter`** ⏎

3. Open the MCP management menu:
   ```claude_cli
   /mcp
   ```

   > 💡 **Tip**: In Claude Code, slash commands (like `/mcp`) are shortcuts to specific actions.

   ✅ **Expected Result**: The `mcp-btp-admin-customidp` MCP server is listed as **connected** with 58 tools.

   ![MCP Server Connected](./images/09_mcp_server_menu.png)

   > 🔧 **Troubleshooting**: If the MCP shows "Not connected", verify your `BTP_CREDENTIALS` and `BTP_ORIGIN` environment variables. Test your credentials by logging into [BTP Cockpit](https://cockpit.btp.cloud.sap/?idp=aju4hpp6l.accounts.ondemand.com) first.

4. Press **`Enter`** ⏎ with the MCP server selected to see details

   ![MCP Server Details](./images/10_mcp_server_menu.png)

   **Verify:**
   - ✅ Status: Connected
   - ✅ Auth: authenticated
   - ✅ Tools: 58 available

### 1.5 Explore Available Tools

5. Select **`View tools`** and press **`Enter`** ⏎

   ![MCP Tools List](./images/11_mcp_server_menu.png)

   - navigate with `up` and `down` arrow keys through the list of available tools to find out which kind of administrative information or actions the MCP can trigger.

   **Tool Categories:**
   - **accounts**: List Global Accounts, Create Subaccounts, etc.
   - **security**: List Users, Create Role Collections, etc.
   - **services**: List Subscriptions, Create Service Instances, etc.
   - **connectivity**: List Destinations, Create Destinations, etc.

6. Press **`Esc`** (several times) to exit the MCP menu

   ✅ **Expected Result**: Claude Code CLI shows "MCP dialog dismissed" and is ready for prompts.

   ![Ready for Prompts](./images/12_mcp_server_menu.png)

---

## 2 Query Your BTP Account with Natural Language

Now the transformation begins! You'll ask the same questions from Exercise 1, but using natural language.

### 2.1 Query 1: Get Your Global Account

1. Copy and paste this prompt into Claude Code:
   ```
   Which Global Account I'm assigned to? Give me the Cockpit URL to access it. Output in table format.
   ```

   Claude will ask permission to use tools. This is **manual mode** - you approve which tools Claude can use.

2. Select **`Yes, and don't ask again...`** for the `List Global Accounts` tool

   ![Tool Permission Request](./images/13_btp_mcp_in_action.png)

   **Why approve?**
   - This is a read-only tool (safe to use repeatedly)
   - "Don't ask again" saves time for future calls
   - Permissions are stored in your project at `./.claude/settings.local.json`
   ![Tool Permission Request](./images/13b_btp_mcp_in_action.png)
   - The given permissions can be removed at any time so that Claude would ask again for permission for the removed tool (API). 

3. Also approve **`Build Navigation Link`** tool with **`Yes, and don't ask again...`**

   ✅ **Expected Result**: Claude shows your Global Account name and provides a Cockpit URL.

   ![Global Account Result](./images/15_btp_mcp_in_action.png)

> [!NOTE]
> **About Agentic Tool Outputs:** Claude's responses are generated dynamically and may vary slightly between runs, even for identical queries. For example:
> - The global account details might include different parameter values (more or fewer fields)
> - Cockpit URLs may appear as full paths (e.g., https://cockpit.btp.cloud.sap/cockpit/#/globalaccount/...) or as formatted "Open in Cockpit" links
> - Information might be formatted as tables, lists, or paragraphs
>
> **This is normal behavior** for agentic tools. The core information remains accurate and complete - only the presentation style varies. See the screenshot below for an example of alternative formatting for the same query.

   ![Global Account Result](./images/15b_btp_mcp_in_action.png)

4. **`Ctrl + Click`** on the Cockpit URL link

5. Sign in with your test user if needed

   ✅ **Expected Result**: BTP Cockpit opens to your global account home page.

   ![BTP Cockpit Opened](./images/17_btp_cockpit.png)

   > 💡 **Setup Tip**: Place the Browser window next to your Claude window so you can verify results side-by-side.

---

### 2.2 Query 2: Find Your Permissions (The Same Task from Exercise 1!)

Remember in Exercise 1 how you had to navigate through multiple subaccounts to find your permissions? Let's see how long it takes now.

5. Copy and paste this prompt (replace `<NN>` with your number):
   ```
   Which role collections (i.e. permissions) are assigned to my user user teched.xp162.<NN>@education.cloud.sap on global account level?
   ```

6. Approve any read-only tools Claude needs with **`Yes, and don't ask again...`**

   ✅ **Expected Result**: Claude provides the information that your test user has Global Account Viewer permission.
 
   ![User Permissions Result](./images/18a_btp_mcp_in_action.png)

7. Copy and paste this prompt (replace `<NN>` with your number):
   ```
   List the accessible subaccounts of my user teched.xp162.<NN>@education.cloud.sap
   ```

8. Approve any read-only tools Claude needs with **`Yes, and don't ask again...`**

   ✅ **Expected Result**: Claude provides the information that your test user has access to 10 subaccounts

   ![User Permissions Result](./images/18b_btp_mcp_in_action.png)

9. Copy and paste this prompt (replace `<NN>` with your number):

   ```
   Which role collections (i.e. permissions) are assigned to my user user teched.xp162.<NN>@education.cloud.sap for these accessible subaccounts?
   Create list with this info and cockpit links
   ```

10. Approve any read-only tools Claude needs with **`Yes, and don't ask again...`**

   ✅ **Expected Result**: Claude provides the information that your test user has access to 2 subaccounts with `Subaccount Administrator` and 8 with `Subaccount Viewer` access.

   ![User Permissions Result](./images/1_btp_mcp_in_action.png)

**Summary:** 

With 3 queries which took all in all ~1 min you got the same information as in Exercise 1.

**Compare with Exercise 1:**
   - **Exercise 1**: ~5-10 minutes of manual navigation
   - **Exercise 2**: ~1 minute with one prompt
   - **Efficiency gain**: 5-10x faster! ⚡

---

## 3 Try More Administrative Queries

Now experiment with the other questions from Exercise 1!

### 3.1 User Management

1. Copy and paste this prompt (replace `<NN>` with your number):
   ```
   Which other users (from custom IdP and sap default IdP) exist in the accessible subaccounts of my user teched.xp162.<NN>@education.cloud.sap?
   Which role collections (i.e. permissions) have these users there?
   ```

2. Approve read-only tools as needed.

   ✅ **Expected Result**: Comprehensive overview of all users and their permissions across your 10 subaccounts.

   ![User Management](./images/18d_btp_mcp_in_action.png)


### 3.2 Inactive Users

1. Copy and paste this prompt (replace `<NN>` with your number):
   ```
   Which users (custom or sap IdP) exist in the subaccounts where my user teched.xp162.<NN>@education.cloud.sap is Subaccount Administrator and have never logged in?
   Create cockpit links to those subaccounts users pages where inactive users exist
   ```

   ✅ **Expected Result**: List of users who never logged in, organized by subaccount, with direct links to manage them.

   ![Inactive Users Result](./images/19_btp_mcp_in_action.png)

   **In Exercise 1**, this would require:
   - Navigating to each of the subaccounts
   - Checking each user's last login date
   - Manually noting down the results
   - **Time**: ~5 minutes (if you take all accessible subaccounts into account)

   **In Exercise 2**: One prompt, ~30 seconds ⚡

### 3.3 Runtime Environments

1. Copy and paste:
   ```
   Which the accessible subaccounts of my user teched.xp162.<NN>@education.cloud.sap have a Cloud Foundry runtime environment enabled?
   ```
2. Approve any read-only tools Claude needs with **`Yes, and don't ask again...`**

   ![Inactive Users Result](./images/20_btp_mcp_in_action.png)

   ✅ **Expected Result**: List of subaccounts with Cloud Foundry, including org names and API endpoints.

---

## ✓ Validation Checklist

You have successfully completed this exercise if you can:

- [ ] Configure and authenticate BTP MCP Server in Claude Code CLI
- [ ] View the 58 available MCP tools in the `/mcp` menu
- [ ] Use natural language prompts to query BTP information
- [ ] Understand tool permission management
- [ ] Retrieve user permissions in 10 seconds (vs. 10 minutes in Exercise 1)
- [ ] Answer administrative questions across multiple subaccounts instantly

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| **MCP shows "Not connected"** | Check `BTP_CREDENTIALS` and `BTP_ORIGIN` environment variables. Test credentials at BTP Cockpit first. |
| **"Permission denied" errors** | Ensure PowerShell is running as Administrator |
| **Environment variables not found** | Re-run the `$Env:BTP_CREDENTIALS` and `$Env:BTP_ORIGIN` commands. Note: These are session-specific. |
| **Claude asks permission repeatedly** | Check `./.claude/settings.local.json` - permissions should be saved there |
| **Wrong Global Account** | Verify you're using the correct test user from Exercise 1 |
| **VS Code doesn't open** | Use full path: `"C:\Program Files\Microsoft VS Code\Code.exe" .` |

---

## Summary

**What You Accomplished:**

1. ✅ Configured BTP MCP Server with Basic Authentication
2. ✅ Authenticated using environment variables
3. ✅ Explored 58 administrative tools across 4 domains
4. ✅ Retrieved information using natural language prompts
5. ✅ Experienced **10-60x efficiency gains** compared to Exercise 1

**The Transformation in Numbers:**

| Task | Exercise 1 (Cockpit) | Exercise 2 (MCP) | Improvement |
|------|---------------------|------------------|-------------|
| **Find user permissions** | ~5-10 minutes | ~1 minute | **~5-10x faster** |
| **Identify inactive users** | ~5 minutes | ~30 seconds | **~10x faster** |
| **List runtime environments** | ~5 minutes | ~30 seconds | **~10x faster** |

**Key Insight:**
Single prompts replaced multi-step navigation. Aggregated data came from all subaccounts at once. Tasks that took minutes now take seconds.

---

## What's Next?

So far you've used **read-only queries** with a **Viewer** user.

In **Exercise 3**, you'll switch to a **Global Account Administrator** user and experience complex **write operations** through BTP Cockpit (creating subscriptions, assigning roles). You'll see how even with administrator privileges, workflows remain complex and time-consuming in the UI.

Then in **Exercise 4**, you'll perform these same workflows with BTP MCP - transforming 30+ manual steps into single prompts.

**The transformation continues...**

Continue to - [Exercise 3 - Exploring Administrator Capabilities with BTP Cockpit](../ex3/README.md)
