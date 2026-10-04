# Claude Code Complete Guide

> Notes based on the [Claude Code 101](https://anthropic.skilljar.com/claude-code-101) course from Anthropic Academy.

## Table of Contents

### Getting Started
- [What is Claude Code?](#what-is-claude-code)
- [How Claude Code Works](#how-claude-code-works)
- [Your First Prompt](#your-first-prompt)

### Working Effectively
- [Explore, Plan, Code, Commit](#explore-plan-code-commit)
- [Context Management](#context-management)
- [Code Review and Git Workflow](#code-review-and-git-workflow)

### Customizing Claude Code
- [The CLAUDE.md File](#the-claudemd-file)
- [Subagents](#subagents)
- [Hooks](#hooks)
- [Choosing the Right Customization](#choosing-the-right-customization)

### Interview Preparation
- [Common Interview Questions](#common-interview-questions)

---

## What is Claude Code?

### 🎯 Claude Code as an Agentic Coding Tool

**Definition:**
> Claude Code is an agentic coding tool that understands your codebase, edits your files, runs commands, and works with your existing developer tools.

**Simple meaning:**
Instead of copying code back and forth with a chat window, Claude Code goes into your project and does the work itself.

**Why it matters:**
- ✅ Reads and understands the whole codebase - explains features, traces bugs
- ✅ Edits files across the project, e.g. refactors a function and updates every caller
- ✅ Runs terminal commands (builds, tests, installs) and uses the output to decide what to do next
- ✅ Searches the web for docs and the latest API references

**Where it runs:**
- Terminal
- VS Code and JetBrains IDEs
- Claude Desktop app
- Web

**Real-life analogy:**
Claude.ai is like calling a senior engineer on the phone and reading them your code. Claude Code is like that engineer sitting at your keyboard - they open files, run the tests, and make the change.

---

### 🔍 Claude vs Claude Code

| Feature | Claude.ai (chat) | Claude Code |
|---------|------------------|-------------|
| **Access to your files** | ❌ Only what you paste or upload | ✅ Whole codebase |
| **Runs commands** | ❌ | ✅ Builds, tests, installs |
| **Edits files** | ❌ You copy the output | ✅ Edits directly |
| **Works as an agent** | Limited | ✅ Loops until the task is done |
| **Best for** | Questions, writing, analysis | Building and changing software |

---

### 🧩 What is an Agent?

**Definition:**
> An AI agent is software that interacts with its environment and takes actions to complete a defined goal. At its core, it's a large language model running in a loop with access to tools.

**Simple meaning:**
An agent doesn't just answer. It acts, checks the result, and keeps going until the job is done.

**Real-life analogy:**
A chatbot is like a cookbook - it tells you the steps. An agent is like a cook - it follows the steps, tastes the food, and adjusts the seasoning.

---

### ⚠️ Three Things to Keep in Mind

| Concept | What It Means |
|---------|---------------|
| **Context window** | Claude's working memory. It's large but finite, so Claude searches for what it needs instead of loading the whole codebase. |
| **Permissions** | By default, Claude asks before running commands or changing files. You stay in control. |
| **Mistakes happen** | Claude can misread intent, introduce a bug, or over-engineer. Stay in the loop to catch these early. |

**Interview Tip:**
> "Claude Code is an agentic coding tool: unlike a chat window, it reads your codebase, edits files, and runs commands in a loop until the task is done, with permissions that keep you in control."

---

## How Claude Code Works

### 🎯 The Agentic Loop

**Definition:**
> The agentic loop is the cycle Claude Code repeats for every task: gather context, take action, verify the results, and loop again until the goal is met.

**Simple meaning:**
Claude looks around, does something, checks whether it worked, and tries again if it didn't.

**Steps:**
1. You enter a prompt
2. **Gather context** - Claude reads files and searches the codebase
3. **Take action** - edits a file, runs a command
4. **Verify results** - checks whether the action achieved the goal
5. If done, it stops and waits for your next prompt. If not, it loops back to step 2

At any point you can **interrupt**, **steer**, or **add context**.

```text
         ┌──────────────────────────────────────┐
Prompt → │ Gather context → Take action → Verify│ → Done
         │        ↑                        │    │
         │        └──── not done yet ──────┘    │
         └──────────────────────────────────────┘
              ↑ you can interrupt / steer / add context at any time
```

**Real-life analogy:**
The agentic loop is like a mechanic fixing a car - inspect, try a fix, test drive, and repeat until the noise is gone.

---

### 🔧 Tools

**Definition:**
> Tools are capabilities - like reading files, running shell commands, or searching the web - that Claude Code chooses to call when they move a task forward.

**Simple meaning:**
Most AI assistants only take text in and give text out. Tools let Claude actually *do* things, and Claude decides when to use each one.

**Real-life analogy:**
Tools are like the instruments in a toolbox - a plumber picks the wrench or the pipe cutter based on the job in front of them.

---

### 🔐 Permission Modes

Press `Shift + Tab` to cycle between modes.

| Mode | File Edits | Shell Commands | Use When |
|------|-----------|----------------|----------|
| **Default (approval)** | Asks first | Asks first | You want to review every step |
| **Auto-accept** | ✅ Automatic | Asks first | You trust the edits, want speed |
| **Plan mode** | ❌ Read-only | ❌ Read-only tools only | Planning a change or doing a safe review |

**Benefits:**
- ✅ You choose how hands-on you want to be
- ✅ Plan mode lets Claude research with no risk of changes
- ✅ All modes can be configured in your settings file

**Warnings:**
- ⚠️ Skipping permissions gives Claude free rein - a bad command is harder to catch before it runs

**Interview Tip:**
> "Claude Code runs an agentic loop of gather context, act, and verify, using tools it picks itself, and permission modes control how much it can do without asking."

---

## Your First Prompt

### 🎯 Writing a Good Prompt

**Simple meaning:**
Talk to Claude Code like any AI assistant, but be as descriptive as possible. The clearer the goal, the less Claude has to guess.

**❌ Bad Example:**
```text
Add dark mode.
```

**Problems:**
- No location for the toggle
- No guidance on colors
- Claude has to guess the scope

**✅ Good Example:**
```text
My app needs a dark mode implemented across the entire app. Can you create
a toggle switch on the header that allows a user to toggle between light
mode and dark mode? I need you to find a good contrast color that works
based on my existing light theme.
```

**Benefits:**
- ✅ Scope is clear (entire app)
- ✅ Location is clear (header)
- ✅ Constraint is clear (match existing theme)

---

### 🏗️ Plan Mode

**Definition:**
> Plan mode uses read-only tools to analyze your codebase and research an implementation, asks clarifying questions, and returns a detailed plan before any code is written.

**Simple meaning:**
Claude thinks it through and shows you the plan first. Nothing changes until you approve.

**When to use:**
- Multi-step features
- Complex or risky changes
- Safe code reviews

**Steps (dark mode example):**
1. Open your project root and run `claude`
2. Press `Shift + Tab` until you see "Plan Mode"
3. Enter your prompt
4. Review the plan; ask Claude to revise specific areas if needed
5. Approve and let Claude ask for approval at each step

**Real-life analogy:**
Plan mode is like an architect's blueprint - you agree on the drawings before anyone starts knocking down walls.

**Interview Tip:**
> "Be descriptive in the prompt, and use plan mode for multi-step work so Claude researches and proposes a plan before touching any code."

---

## Explore, Plan, Code, Commit

### 🎯 The Core Workflow

**Definition:**
> Explore, Plan, Code, Commit is the recommended Claude Code workflow: gather context, agree on a plan, implement against it, then review and ship.

**Simple meaning:**
Don't jump straight to "write the code". Let Claude understand the problem and plan first, so you spend less time course-correcting later.

**Why it matters:**
- ✅ Course-correcting is cheapest before code is written
- ✅ The plan becomes the measure of success
- ✅ You keep the context of *how* you reached the result
- ✅ Fewer surprises at review time

**Real-life analogy:**
It's like cooking from a recipe: read it (explore), lay out ingredients (plan), cook (code), and taste before serving (commit).

---

### 🔍 Step 1-2: Explore and Plan

Use **plan mode** - Claude can only read files, so it gathers information without making changes.

```text
I need to add WebP conversion to our image upload pipeline. Figure out where
in the pipeline it should happen, whether we need new dependencies, and how
to approach it.
```

Claude reads relevant files, runs web searches, and returns a plan. Review it and ask for revisions on specific areas.

**Tip:** You can also run the **Explore subagent** outside plan mode when you just want a summary of the codebase with no changes planned.

---

### 🔧 Step 3: Code

Approve the plan and let Claude work through it, in auto-accept or approval mode.

**Tips for a smoother coding phase:**
- ✅ **Define success criteria** - Claude needs to know what "correct" looks like
- ✅ **Add tools** - e.g. the Claude in Chrome extension lets Claude open a browser tab and test the UI
- ✅ **Include a test suite** - Claude validates against it continuously (make sure the tests are reliable first)
- ✅ **Save recurring fixes** - if Claude keeps hitting the same issue, ask it to save the solution to `CLAUDE.md`

---

### 🚀 Step 4: Commit

1. Test the changes yourself
2. Run a **code-reviewer subagent** - it has fresh eyes and none of the main session's bias
3. Ask Claude to write a commit message in your style
4. Push, and repeat for the next feature

| Step | Purpose |
|------|---------|
| **Explore** | Give Claude the relevant context |
| **Plan** | Create the plan Claude measures success against |
| **Code** | Iterate with Claude to the final outcome |
| **Commit** | Review and push so you can move on |

**Interview Tip:**
> "The key workflow is Explore, Plan, Code, Commit: use plan mode to research and agree on an approach, implement with clear success criteria and tests, then review with a subagent before committing."

---

## Context Management

### 🎯 The Context Window

**Definition:**
> The context window is the amount of information Claude can hold at once - every prompt, file read, tool call, and tool result adds to it.

**Simple meaning:**
It's Claude's working memory. Space is finite, so use it wisely.

**Why it matters:**
- ✅ A clean context keeps Claude focused on the current task
- ✅ Irrelevant history can bias new work
- ✅ When context fills up, details can be lost

**Real-life analogy:**
The context window is like a desk - you can spread out many papers, but once it's full, older papers get stacked in a summary pile and fine details get harder to find.

---

### 🔧 Compaction

When you approach the limit, Claude Code **compacts** automatically: it summarizes important details and removes unneeded tool results.

⚠️ Compaction can lose details.

---

### 🧩 Context Commands

| Command | What It Does | Use When |
|---------|--------------|----------|
| `/compact` | Summarizes everything so far, keeps a memory of it | Same feature, running out of space |
| `/clear` | Wipes the conversation completely | Starting a new feature |
| `/context` | Shows context size, top consumers, and a visual breakdown | Checking what's using space |

**When to choose `/compact`:**
- ✅ Mid-feature and need to continue
- ❌ Avoid when switching to unrelated work - old context can bias the new task

**When to choose `/clear`:**
- ✅ Starting a new feature
- ✅ Previous work isn't relevant
- 💡 Put anything Claude must remember across sessions in `CLAUDE.md`

---

### 💡 Tips for Saving Context Space

**1. Be specific**
A vague prompt looks smaller but costs more - Claude has to explore and reason more to fill the gaps.

**2. Manage your MCP servers**
MCP servers load all their tool definitions into context by default, even unused ones. Turn off servers unrelated to the current project. **Skills** are an alternative that only load when needed.

**3. Use subagents**
A subagent has its own context window. For questions where you only need the answer ("where are the authentication endpoints?"), it does the searching and returns just a summary.

**Interview Tip:**
> "Context is Claude's finite working memory: use `/compact` to continue a long feature, `/clear` to start a new one, and keep it lean with specific prompts, fewer MCP servers, and subagents."

---

## Code Review and Git Workflow

### 🎯 Review with a Subagent

**Simple meaning:**
Before you push a PR, ask a subagent to review your changes. It runs in its own context window, so it doesn't carry the bias of the session that wrote the code.

**Best practices:**
- ✅ Restrict the reviewer to **read-only tools** - it should flag issues, not edit files
- ✅ Check the subagent config into the repo so the whole team uses the same reviewer

**Real-life analogy:**
It's like asking a colleague to proofread your essay - you're too close to your own writing to see the mistakes.

---

### 🔧 Git Shortcuts

| Feature | What It Does |
|---------|--------------|
| `/commit-push-pr` skill | Commits, pushes, and opens a PR in one step. With a Slack MCP server and channels listed in `CLAUDE.md`, it also posts the PR link. |
| `claude --from-pr <PR_NUMBER>` | Resumes the session linked to a PR (created via `gh pr create`), e.g. to address review comments or fix a failing build. |

```bash
# Come back to a PR later and continue where you left off
claude --from-pr 1234
```

**Interview Tip:**
> "Use a read-only reviewer subagent for an unbiased review, `/commit-push-pr` for the commit-to-PR flow, and `--from-pr` to resume work on a PR later."

---

## The CLAUDE.md File

### 🎯 Persistent Project Memory

**Definition:**
> `CLAUDE.md` is a Markdown file in your project that Claude Code reads automatically at the start of every session; its contents are added to your prompt.

**Simple meaning:**
An onboarding guide for your codebase, so Claude doesn't start from zero every time.

**Why it matters:**
- ✅ Claude doesn't have to re-explore the stack, commands, and conventions
- ✅ Fewer wrong assumptions
- ✅ Shared with the team through version control
- ✅ Captures corrections so you don't repeat them

**Real-life analogy:**
`CLAUDE.md` is like the welcome binder a new hire gets on day one - the stack, the commands, and the house rules in one place.

---

**❌ Bad Example:**
```text
(No CLAUDE.md - every session)
"We use pnpm, not npm... tests run with pnpm test... use server actions,
 not API routes... remember 2-space indentation..."
```

**✅ Good Example:**
```markdown
# Project

This is a Next.js 15 app using the App Router, Tailwind, and Drizzle ORM.

# Commands

- Dev server: `pnpm dev`
- Run tests: `pnpm test`
- Lint: `pnpm lint`

# Code Style

- Use 2-space indentation
- Prefer named exports
- All API routes go in app/api/
- Use server actions instead of API routes where possible
```

Now when you ask for a React component, Claude already knows to use Tailwind and follow your conventions.

---

### 🏗️ Memory Hierarchy

| Level | Location | Shared? | Use For |
|-------|----------|---------|---------|
| **Project** | Project root | ✅ Committed to git | Stack, commands, team conventions |
| **User** | Your Claude config folder | ❌ Just you | Personal preferences across all projects |

---

### 💡 Tips

**1. Save corrections to memory**
If you keep correcting Claude, ask it to save the rule:
```text
Always use server actions instead of API routes. Save this rule to CLAUDE.md.
```

**2. Reference project docs with `@`**
```markdown
## README.md

Please read if you need more info: @README.md
```

**3. Start without one**
Work without a `CLAUDE.md` first to see where you keep course-correcting. Then run `/init` to generate one. This keeps it short and focused.

##### ⚖️ Trade-offs

| Benefit | Cost |
|---------|------|
| **Context loaded every session** | Uses context space every session |
| **Team-wide consistency** | Must be kept up to date |
| **Fewer repeated corrections** | Instructions are followed most of the time, not guaranteed (use hooks for that) |

**Interview Tip:**
> "`CLAUDE.md` gives Claude Code persistent project memory: it's read at the start of every session, committed for the team, and should hold only the stack, commands, and rules you'd otherwise repeat."

---

## Subagents

### 🎯 Subagents

**Definition:**
> A subagent is a separate Claude instance that the main agent delegates a task to; it runs with its own isolated context window and returns only a summary.

**Simple meaning:**
Claude sends a helper to do the digging, and the helper reports back with just the answer.

**Why it matters:**
- ✅ Exploration and research don't clutter the main context
- ✅ Can run in parallel with the main agent
- ✅ Fresh context means no bias (great for code review)
- ✅ Can be restricted to specific tools

**When to use:**
- "Explore this codebase and tell me where X happens"
- Research tasks with lots of web searches
- Independent code review

**Real-life analogy:**
A subagent is like sending an intern to the archive - they read hundreds of files and come back with a one-page summary, so your desk stays clear.

---

### 🔧 Creating a Subagent

Run `/agents`, choose **Create new agent**, then pick the scope, purpose, tools, and color. Claude generates the name, description, and prompt. The description also tells Claude *when* to call the subagent.

Subagents are Markdown files with YAML frontmatter:

```markdown
---
name: code-reviewer
description: Reviews recent changes for bugs and style issues. Use before committing or opening a PR.
tools: Read, Grep, Glob
---

You are a senior code reviewer. Review the recent changes for:
- Correctness bugs and missed edge cases
- Violations of the conventions in CLAUDE.md
- Missing or weak tests

Report findings with file and line references. Do not edit files.
```

**Further customization:**
- **Persistent memory** - the subagent keeps memory across conversations
- **Preloaded skills** - list skills under the `skills` key. Unlike the main conversation, the *entire* skill loads into the subagent's context

##### ⚖️ Trade-offs

| Benefit | Cost |
|---------|------|
| **Clean main context** | Main agent only sees the summary, not the details |
| **Unbiased fresh perspective** | No knowledge of the session's decisions unless you pass them in |
| **Parallel work** | Extra token usage across multiple context windows |

**Interview Tip:**
> "Subagents run tasks in their own context window and return only a summary, which keeps the main context clean and gives an unbiased view, especially for exploration and code review."

---

## Hooks

### 🎯 Hooks

**Definition:**
> Hooks are commands that run automatically at specific points in Claude Code's lifecycle; unlike prompts and `CLAUDE.md`, they are deterministic and always run.

**Simple meaning:**
If something must happen every time, without exception, don't ask Claude - put it in a hook.

**Why it matters:**
- ✅ Guaranteed behavior (`CLAUDE.md` rules are followed *most* of the time)
- ✅ Can block dangerous actions before they happen
- ✅ Shared with the team via the repo
- ✅ Automates formatting, logging, and notifications

**Common use cases:**
- Auto-format after file edits
- Log every executed command for compliance
- Block edits to production files
- Notify yourself when Claude finishes

**Real-life analogy:**
A `CLAUDE.md` rule is like a "please wipe your feet" sign. A hook is an automatic door that won't open until you step on the mat.

---

### 🔧 Hook Events

| Event | Runs |
|-------|------|
| **PreToolUse** | Before a tool call (can block it) |
| **PostToolUse** | After a tool call completes |
| **UserPromptSubmit** | When you submit a prompt, before Claude processes it |
| **Stop** | When Claude finishes responding |
| **Notification** | When Claude sends a notification |

Configure hooks with the `/hooks` command or by editing `settings.json`. Each hook has an **event**, an optional **matcher** (which tools it applies to), and a **command**.

---

### 🚀 Example: Auto-format After Edits

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "\"$CLAUDE_PROJECT_DIR\"/.claude/hooks/format.sh"
          }
        ]
      }
    ]
  }
}
```

```bash
#!/bin/bash
# .claude/hooks/format.sh - format the file Claude just edited
# The hook receives the tool call as JSON on stdin
file=$(jq -r '.tool_input.file_path')

case "$file" in
  *.ts|*.tsx|*.js) npx prettier --write "$file" ;;
  *.go)            gofmt -w "$file" ;;
esac
```

---

### 🔐 Blocking with PreToolUse

A PreToolUse hook receives the tool name and input as JSON on stdin. Its **exit code** decides what happens:

| Exit Code | Result |
|-----------|--------|
| **0** | Proceed normally |
| **2** | Block the action; stderr is sent to Claude so it knows why and can adjust |
| **Other** | Non-blocking error shown to you; nothing is stopped |

```bash
#!/bin/bash
# .claude/hooks/block-rm.sh - block destructive bash commands
command=$(jq -r '.tool_input.command // ""')

if echo "$command" | grep -q 'rm -rf'; then
  echo "Blocked: 'rm -rf' is not allowed in this project." >&2
  exit 2   # block and tell Claude why
fi

exit 0     # allow everything else
```

Use this to enforce hard rules: block writes to production config, block `rm -rf`, block commits to `main`.

---

### 🧩 Sharing Hooks with Your Team

- Hooks in `.claude/settings.json` are project-level and can be committed
- Use `$CLAUDE_PROJECT_DIR` to reference scripts, so they work from any working directory

**Interview Tip:**
> "Hooks are deterministic: PostToolUse is great for formatting and logging, and PreToolUse can block a tool call by exiting with code 2, so anything that must always happen belongs in a hook, not a prompt."

---

## Choosing the Right Customization

### ⚖️ CLAUDE.md vs Subagents vs Hooks vs Skills

| Feature | CLAUDE.md | Subagents | Hooks | Skills |
|---------|-----------|-----------|-------|--------|
| **Purpose** | Project memory | Delegate tasks | Enforce behavior | Reusable procedures |
| **Guaranteed?** | ❌ Followed most of the time | ❌ | ✅ Always runs | ❌ |
| **Context cost** | Loaded every session | Own context window | None | Loaded when relevant |
| **Shared via git** | ✅ | ✅ | ✅ | ✅ |
| **Example** | "Use pnpm, 2-space indent" | Code reviewer | Prettier after edits | Release notes format |

| Scenario | Use | Avoid |
|----------|-----|-------|
| Claude keeps forgetting a convention | **CLAUDE.md** | Repeating it in every prompt |
| Need research without cluttering context | **Subagent** | Exploring in the main session |
| Rule must never be broken | **Hook** | Relying on a CLAUDE.md instruction |
| Repeated multi-step procedure | **Skill** | Pasting the same instructions |

**Remember:**
> "If something needs to happen every time without fail, don't put it in a prompt. Put it in a hook."

---

## Common Interview Questions

### Basic Questions

**1. What is Claude Code?**
> "An agentic coding tool that reads your codebase, edits files, and runs commands in your terminal, IDE, desktop app, or browser."

**2. How is Claude Code different from Claude.ai?**
> "Claude Code has direct access to your files and terminal and works as an agent, so it does the work itself instead of you copying code back and forth."

**3. What is the agentic loop?**
> "Gather context, take action, verify results, and repeat until the goal is met, while you can interrupt or steer at any time."

**4. What are the permission modes?**
> "Default asks before edits and commands, auto-accept edits files freely but still asks before commands, and plan mode is read-only; `Shift + Tab` cycles between them."

**5. What is `CLAUDE.md`?**
> "A Markdown file Claude Code reads at the start of every session to learn the project's stack, commands, and conventions."

### Intermediate Questions

**1. What's the difference between `/compact` and `/clear`?**
> "`/compact` summarizes the conversation so you can keep working on the same feature; `/clear` wipes it so a new feature starts without bias."

**2. Why use plan mode?**
> "It researches the codebase with read-only tools and proposes a plan, so you course-correct before any code is written."

**3. How do subagents help with context?**
> "They do the heavy exploration in their own context window and return only a summary, keeping the main context clean."

**4. Why should a code reviewer be a subagent?**
> "It has fresh context without the main session's bias, and it should be limited to read-only tools so it flags issues instead of editing."

**5. How does a vague prompt waste context?**
> "Without clear instructions, Claude has to explore and reason more, which uses far more context than a detailed prompt."

### Advanced Questions

**1. When would you use a hook instead of a `CLAUDE.md` rule?**
> "When the behavior must be guaranteed - `CLAUDE.md` is followed most of the time, but a hook always runs, like formatting after every edit or blocking `rm -rf`."

**2. How does a PreToolUse hook block an action?**
> "It reads the tool call as JSON on stdin and exits with code 2; Claude Code blocks the call and sends stderr back to Claude as feedback."

**3. How do MCP servers affect context, and what's the alternative?**
> "MCP servers load all their tool definitions upfront even if unused, so disable unrelated servers; skills load only their name and description until needed."

**4. How would you set up Claude Code for a team?**
> "Commit a project `CLAUDE.md`, shared subagents like a read-only reviewer, and hooks in `.claude/settings.json` using `$CLAUDE_PROJECT_DIR` so everyone gets the same behavior."

**5. How do you make Claude Code confident its work is correct?**
> "Define explicit success criteria in the plan, give it a reliable test suite and tools like a browser to verify UI, and review with a subagent before committing."

---

## 🎓 Summary

**Core ideas:**
1. **Claude Code** is an agent - it reads, edits, runs, and verifies in a loop
2. **Permission modes** control how much it does without asking
3. **Explore → Plan → Code → Commit** is the workflow to follow
4. **Context** is finite - `/compact`, `/clear`, `/context`, and subagents keep it clean
5. **CLAUDE.md** is persistent project memory
6. **Subagents** delegate work in separate context windows
7. **Hooks** guarantee behavior every time

**Remember:**
> "Plan before you code, keep context clean, and put anything that must always happen in a hook."

---

**Source:** [Claude Code 101 - Anthropic Academy](https://anthropic.skilljar.com/claude-code-101)
**Last Updated:** October 2026
