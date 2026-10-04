# Claude Platform Complete Guide

> Notes based on the [Claude Platform 101](https://anthropic.skilljar.com/claude-platform-101) course from Anthropic Academy. Model IDs and beta header names in the examples are the ones used in the course; check the [Claude docs](https://platform.claude.com/docs) for current values.

## Table of Contents

### Platform Basics
- [What is the Claude Platform?](#what-is-the-claude-platform)
- [Your First API Call](#your-first-api-call)
- [Choosing the Right Model](#choosing-the-right-model)

### Building Agents
- [The Agent Loop](#the-agent-loop)
- [Tool Use](#tool-use)
- [Extended Thinking](#extended-thinking)
- [Built-in Tools](#built-in-tools)

### Extending Claude
- [Skills](#skills)
- [MCP](#mcp)
- [Context Management](#context-management)

### Managed Agents and Tooling
- [What are Managed Agents?](#what-are-managed-agents)
- [Building Your First Managed Agent](#building-your-first-managed-agent)
- [Building with Claude Code](#building-with-claude-code)
- [Choosing the Right Feature](#choosing-the-right-feature)

### Interview Preparation
- [Common Interview Questions](#common-interview-questions)

---

## What is the Claude Platform?

### 🎯 The Claude Platform

**Definition:**
> The Claude Platform is Anthropic's infrastructure for building with Claude programmatically - you send structured requests from code and get structured responses back.

**Simple meaning:**
Instead of chatting in a browser, your app talks to Claude directly and you control every detail: the model, token budget, tools, and system instructions.

**Why it matters:**
- ✅ Wire Claude into a product that already exists
- ✅ Full control over model, response length, tools, and instructions
- ✅ Works from any language through the REST API or SDKs
- ✅ Scales from one call to thousands with managed infrastructure

**What it's made of:**
- A **REST API** you can call from any language
- **SDKs** for several programming languages
- **Command line interfaces**
- A **Console** for API keys, usage monitoring, managed agents, and prompt testing

**Real-life analogy:**
Claude.ai is like eating at a restaurant. The Claude Platform is like getting access to the restaurant's kitchen - you decide the ingredients, the recipe, and how it's served in your own dining room.

---

### 🏗️ The Three Layers

| Layer | What It Is | Examples |
|-------|------------|----------|
| **Primitives** | API building blocks you call from code | Messages API, tool use, files, web search, code execution, MCP servers, skills |
| **Infrastructure** | Plumbing to scale past a prototype | Managed agents, retries, queues, observability, prompt caching, memory |
| **Controls** | Dials for running in production | Dashboards, evals, workspaces, usage and spend limits, request logs |

**Remember:**
> "Build with primitives, scale on infrastructure, run with control."

---

### 🔧 Example: Drafting Help Desk Replies

A help desk app needs a "Draft reply with Claude" button that follows your team's tone.

**Steps:**
1. Define a client
2. Retrieve the ticket
3. Call `messages.create`
4. Return the response to the button

```python
import anthropic

client = anthropic.Anthropic()

response = client.messages.create(
    model="claude-haiku-4-5",      # Haiku: a good fit for a simple drafting task
    max_tokens=1024,               # cap on response length
    system=TONE_AND_GUIDELINES,    # the role and rules Claude follows
    messages=[
        {"role": "user", "content": ticket_content}   # the ticket text
    ],
)

draft = response.content
```

| Parameter | Job |
|-----------|-----|
| **model** | Which model handles the request |
| **max_tokens** | Caps how long the response can be |
| **system** | System prompt - the role Claude plays, tone, and guidelines |
| **messages** | Array of `user` / `assistant` turns |

**Interview Tip:**
> "The Claude Platform is API-level access to Claude's models, tools, and infrastructure - it takes you from asking Claude a question to making Claude part of your product."

---

## Your First API Call

### 🎯 The Messages API

**Definition:**
> Every API call goes through `messages.create`, which takes a model, a max token limit, and a list of messages.

**Simple meaning:**
One function call sends Claude a conversation and gets a reply back.

**Real-life analogy:**
`messages.create` is like sending a letter with a cover note (system prompt) and a word limit (max tokens) - and getting a reply in the mail.

---

### 🔧 Get Set Up

**Steps:**
1. Create an **API key** at platform.claude.com (buy credits first)
2. Store it in `.env.local`, never in source code
3. Install the SDK

```bash
npm install @anthropic-ai/sdk
```

**❌ Bad Example:**
```javascript
// Hardcoded key - ends up leaked on GitHub
const client = new Anthropic({ apiKey: "sk-ant-..." });
```

**✅ Good Example:**
```javascript
// SDK reads ANTHROPIC_API_KEY from the environment (.env.local)
const client = new Anthropic();
```

---

### 🚀 Example: Reviewing Buggy Code

```javascript
import Anthropic from "@anthropic-ai/sdk";

const client = new Anthropic();

const buggyCode = `
function add(a, b) {
  return a - b;
}
`;

const response = await client.messages.create({
  model: "claude-opus-4-8",
  max_tokens: 1024,
  // System prompt shapes the persona
  system: "You are a terse senior code reviewer. Give feedback in one paragraph.",
  messages: [
    { role: "user", content: `Review this code:\n${buggyCode}` },
  ],
});

// content is an array of blocks, not a string - always check the type
for (const block of response.content) {
  if (block.type === "text") {
    console.log(block.text);
  }
}
// Output: Claude points out that add() subtracts and suggests a + b
```

**Key points:**
- ✅ `system` shapes the persona (terse reviewer, not chatty)
- ✅ `response.content` is an **array of blocks** - text, tool calls, thinking - so loop and check `type`

**From script to product:**
The same call powers a "Generate summary" endpoint: load a meeting transcript from the database, send it with a system prompt like "extract insights and risks", save the result, return it to the UI.

**Interview Tip:**
> "A basic call is `messages.create` with a model, max tokens, and messages; add a system prompt for behavior, and remember the response content is an array of typed blocks."

---

## Choosing the Right Model

### 🎯 Model Tiers

**Definition:**
> Claude comes in model tiers that trade capability for speed and cost; you pick one with the `model` parameter.

**Simple meaning:**
Bigger models are smarter but slower and more expensive. Pick the smallest one that does the job well.

| Model | Capability | Speed | Cost | Best For |
|-------|-----------|-------|------|----------|
| **Fable** | Highest (above Opus) | Slowest | Significantly higher than Opus | Toughest challenges where the extra capability pays off |
| **Opus** | Very high | Slow | High | Deep reasoning, complex analysis, multi-step coding, nuanced writing |
| **Sonnet** | Balanced | Fast | Medium | Most production work |
| **Haiku** | Good | Fastest | Lowest | Classification, extraction, routing, high volume |

**Real-life analogy:**
Choosing a model is like choosing a delivery service - you don't send a letter by private jet. Pick the cheapest option that arrives on time and intact.

---

### 🔍 Start with a Simple Evaluation

**Steps:**
1. Collect 20-30 representative examples from your real workload
2. Define what good output looks like
3. Run them through **Haiku** first - if quality holds, you're done
4. If not, step up to **Sonnet**
5. Only use **Opus** when the task needs it

```python
models = ["claude-haiku-4-5", "claude-sonnet-4-6", "claude-opus-4-7"]

# Same prompt, same max tokens - only the model changes
for model in models:
    response = client.messages.create(
        model=model,
        max_tokens=300,
        messages=[{"role": "user", "content": prompt}],
    )
    # usage = input and output tokens, which is what you're billed on
    print(model, response.usage)
```

For a two-sentence definition, Haiku often answers in under a second with a perfectly good result, while Opus's extra polish is wasted.

**Remember:**
> "The right model is the cheapest one whose output you'd actually ship."

---

### 🚀 Routing Work to Different Models

In one document processing endpoint:
- Every incoming file is **classified with Haiku**
- Client updates are **drafted with Sonnet**
- Only RFP responses **use Opus**

##### ⚖️ Trade-offs

| Benefit | Cost |
|---------|------|
| **Bigger model: better quality on hard tasks** | Higher latency and price |
| **Smaller model: fast and cheap** | May fall short on complex reasoning |
| **Per-task routing: best of both** | More logic to maintain |

**Interview Tip:**
> "Run a small eval from Haiku upward, stop at the cheapest model whose output you'd ship, and route different tasks to different models within the same app."

---

## The Agent Loop

### 🎯 What an Agent Is

**Definition:**
> An agent is an autonomous version of Claude that runs both sides of the messaging loop: it receives a task, picks tools, and keeps executing until it decides the task is done.

**Simple meaning:**
A single call gives one answer. An agent acts, looks at the result, decides what's next, and keeps going.

**Why it matters:**
- ✅ Automates multi-step workflows
- ✅ Claude can use your data and systems through tools
- ✅ The same simple loop scales from demos to production
- ✅ You own the loop and tools; Claude owns the reasoning

**Real-life analogy:**
An agent is like a detective - gather a clue, decide where to look next, follow it, and repeat until the case is solved.

---

### 🔧 How the Loop Works

**Steps:**
1. Send a message to Claude with tools available
2. Claude replies with a final answer **or** a tool request
3. Your code runs the tool
4. Send the result back to Claude
5. Repeat until `stop_reason` is `end_turn`

```python
import anthropic

client = anthropic.Anthropic()

# Tools tell Claude what's available: name, description, input schema
tools = [
    {
        "name": "get_weather",
        "description": "Get the current weather for a city.",
        "input_schema": {
            "type": "object",
            "properties": {
                "city": {"type": "string", "description": "The city to get weather for"}
            },
            "required": ["city"],
        },
    }
]

# Hardcoded lookup - in a real app this would hit a database or API
def run_tool(name, tool_input):
    if name == "get_weather":
        return f"Weather in {tool_input['city']}: 95F, sunny"
    raise ValueError(f"Unknown tool: {name}")

messages = [{"role": "user", "content": "What should I wear in Austin today?"}]

# The agent loop: switch on the stop reason each iteration
while True:
    response = client.messages.create(
        model="claude-sonnet-4-6",
        max_tokens=1024,
        tools=tools,
        messages=messages,
    )

    if response.stop_reason == "end_turn":
        # Claude is done - print the final answer
        for block in response.content:
            if block.type == "text":
                print(block.text)
        break

    if response.stop_reason == "tool_use":
        # Run every tool Claude asked for
        tool_results = []
        for block in response.content:
            if block.type == "tool_use":
                tool_results.append({
                    "type": "tool_result",
                    "tool_use_id": block.id,
                    "content": run_tool(block.name, block.input),
                })
        # Feed Claude's turn and the results back, then loop
        messages.append({"role": "assistant", "content": response.content})
        messages.append({"role": "user", "content": tool_results})
```

**Running it:**
- **Turn 1:** `stop_reason` is `tool_use` - Claude asks for `get_weather("Austin")`
- **Turn 2:** `stop_reason` is `end_turn` - Claude suggests light, breathable clothes

Two API calls, one tool run, one answer.

**In production:**
The same loop powers a compliance agent that reads a structural report, looks up building codes through a tool, and writes risk findings to the database. The differences are real tools, results streamed to the UI with server-sent events, and findings saved to a table.

**Interview Tip:**
> "An agent is Claude in a loop: send messages with tools, run any tool Claude requests, return the result, and stop when the stop reason is `end_turn`."

---

## Tool Use

### 🎯 Tools

**Definition:**
> A tool is a function you define and expose to Claude; Claude decides when to call it, and your code executes it.

**Simple meaning:**
Claude can't check your database or project tracker on its own. Tools give it a way to ask your code to do it.

**Why it matters:**
- ✅ Gives Claude access to your data and actions
- ✅ Claude picks the right tool, in the right order
- ✅ Tools can wrap functions you already have
- ✅ Adding a tool is just adding to an array

**Real-life analogy:**
Tools are like a menu of services at a hotel front desk - the guest (Claude) asks for room service, but the kitchen (your code) actually makes the food.

**Key point:**
> Claude doesn't execute the tool - your code does. Claude requests → your code runs it → the result goes back to Claude.

---

### 🔧 Defining a Tool

A tool is a JSON schema with a **name**, a **description**, and an **input schema**, passed in the `tools` array.

**❌ Bad Example:**
```json
{
  "name": "lookup",
  "description": "Looks things up.",
  "input_schema": {
    "type": "object",
    "properties": { "q": { "type": "string" } }
  }
}
```

**Problems:**
- Vague description - Claude can't tell when to use it
- Unclear input name and no description of the input

**✅ Good Example:**
```json
{
  "name": "lookup_building_code",
  "description": "Look up a specific building code section by its identifier. Returns the full text of that code section.",
  "input_schema": {
    "type": "object",
    "properties": {
      "section": {
        "type": "string",
        "description": "The building code section to look up"
      }
    },
    "required": ["section"]
  }
}
```

⚠️ **Vague descriptions are the number one reason agents misfire.** The description is what Claude reads to decide whether to call the tool.

When Claude wants a tool, the response has `stop_reason: "tool_use"` and a `tool_use` block. You send back a user message containing a `tool_result` block with the matching `tool_use_id`.

---

### 🧩 Multiple Tools

Give Claude several tools and it picks which to use and in what order, based on their descriptions.

```javascript
const tools = [
  {
    name: "get_weather",
    description: "Get today's current weather for a city.",
    input_schema: {
      type: "object",
      properties: { city: { type: "string", description: "The city to check" } },
      required: ["city"],
    },
  },
  {
    name: "get_forecast",
    description: "Get the weather forecast for the next few days for a city.",
    input_schema: {
      type: "object",
      properties: { city: { type: "string", description: "The city to check" } },
      required: ["city"],
    },
  },
];

// Dispatch on the tool name - add a case per tool
function runTool(name, input) {
  switch (name) {
    case "get_weather":
      return getWeather(input.city);
    case "get_forecast":
      return getForecast(input.city);
  }
}
```

For "packing for a three-day trip to Denver", Claude calls both tools, sometimes in the same turn, then answers.

---

### 🚀 The Tool Runner

Handwriting the loop and JSON schemas is a lot of code. The **tool runner** (TypeScript, Python, and Ruby SDKs) builds schemas from your actual functions and runs the whole loop.

```typescript
// Plain functions - no JSON schemas
function getWeather(city: string) {
  // ...existing lookup
}

function getForecast(city: string) {
  // ...existing lookup
}

const runner = client.beta.messages.toolRunner({
  model: "claude-sonnet-4-6",
  max_tokens: 1024,
  messages: [
    {
      role: "user",
      content: "I'm packing for a three-day trip to Denver. What's the weather today and over the next few days?",
    },
  ],
  tools: [getWeather, getForecast],
});

// Final assistant message after all the tool calls settle
const finalMessage = await runner.untilDone();
```

| Approach | Manual Loop | Tool Runner |
|----------|-------------|-------------|
| **While loop / stop reason switch** | You write it | ✅ Handled |
| **JSON schemas** | You write them | ✅ Generated from functions |
| **Control** | ✅ Full | Less |
| **Code size** | Large | Small |

**Interview Tip:**
> "A tool is a function Claude can request but your code executes; write specific descriptions, handle `stop_reason: tool_use` by returning a `tool_result`, or let the SDK's tool runner handle the loop."

---

## Extended Thinking

### 🎯 Extended Thinking

**Definition:**
> Extended thinking lets Claude reason step by step (a visible chain of thought) before producing its final answer.

**Simple meaning:**
Claude works the problem out before answering, instead of blurting out the first answer - and you can see the reasoning.

**Why it matters:**
- ✅ Fewer confident wrong answers on multi-step problems
- ✅ Better at weighing trade-offs
- ✅ Can connect issues across a long document
- ✅ Reasoning is visible, so you can inspect it

**Real-life analogy:**
It's like showing your work on a math exam - slower, but you catch your mistakes before writing the final answer.

---

### 🔧 Adaptive Thinking and Effort

With adaptive thinking (Opus 4.7 in the course), you don't set a token budget. Turn it on and Claude decides when and how much to think. Control depth with the **effort** parameter, which goes **inside `output_config`**, not next to `thinking`.

| Effort | Use |
|--------|-----|
| `low` | Light reasoning |
| `medium` | Moderate |
| `high` | Default |
| `xhigh` | Extra high |
| `max` | Hardest problems |

```python
response = client.messages.create(
    model="claude-opus-4-7",
    max_tokens=16000,
    thinking={"type": "adaptive"},       # Claude decides when and how much to think
    output_config={"effort": "high"},    # low | medium | high | xhigh | max
    tools=[weather_tool],
    messages=[{
        "role": "user",
        "content": "Plan a road trip out of San Francisco with two stops, "
                   "weighing weather and drive time.",
    }],
)
# Response contains thinking blocks, then tool calls, then the final text
```

**When to choose thinking:**
- ✅ Math and multi-step logic
- ✅ Code debugging
- ✅ Regulatory analysis
- ✅ Trade-offs and comparisons
- ❌ Avoid for simple classification, extraction, or boilerplate - it only adds latency and cost

**In production:**
In a compliance review app, adaptive thinking lets the agent reason *across* sections - e.g. catching a wind load spec in section three that conflicts with a material spec elsewhere.

**Interview Tip:**
> "Extended thinking lets Claude reason before answering; with adaptive thinking you just enable it and set `effort` inside `output_config`, and you use it for hard, trade-off-heavy problems, not simple ones."

---

## Built-in Tools

### 🎯 Server Tools

**Definition:**
> Server tools are pre-built tools you declare in the `tools` array and Anthropic runs on its own infrastructure.

**Simple meaning:**
You don't write the code or host a sandbox. Declare the tool, and the result comes back in the same response - no agent loop needed.

| Server Tool | What It Does |
|-------------|--------------|
| **Web search** | Searches the internet, returns results with citations |
| **Code execution** | Writes and runs Python in a sandbox |
| **Web fetch** | Retrieves full content from URLs |

```python
# Web search - Anthropic runs the search server-side
search_response = client.messages.create(
    model="claude-opus-4-8",
    max_tokens=1024,
    tools=[{"type": "web_search_20260209", "name": "web_search"}],
    messages=[{"role": "user", "content": "What is Anthropic's latest model release? Answer in one sentence."}],
)

# Code execution - Claude writes and runs Python in a sandbox
code_response = client.messages.create(
    model="claude-opus-4-8",
    max_tokens=1024,
    tools=[{"type": "code_execution_20260120", "name": "code_execution"}],
    messages=[{"role": "user", "content": "Calculate the mean and standard deviation of [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]"}],
)

for block in code_response.content:
    if block.type == "server_tool_use":                       # the tool call
        print(f"Tool call: {block.name} — {block.input}")
    elif block.type == "bash_code_execution_tool_result":     # sandbox output
        print(f"stdout: {block.content.stdout}")
    elif block.type == "text":                                # final answer
        print(block.text)
```

**Key points:**
- ✅ No `stop_reason` switch, no pushing tool results back
- ✅ New block types: `server_tool_use` and tool result blocks, next to text blocks

---

### 🧩 Client Tools

**Client tools** run where your code runs, but the SDK ships their schema and a runner.

| Client Tool | What It Does |
|-------------|--------------|
| **Memory** | Claude reads and writes memory across sessions |
| **Bash** | A persistent bash shell for running commands |

| Feature | Custom Tools | Server Tools | Client Tools |
|---------|--------------|--------------|--------------|
| **Who defines the schema** | You | Anthropic | Anthropic (SDK) |
| **Who runs it** | Your code | Anthropic | Your code |
| **Agent loop needed** | ✅ | ❌ | ✅ (SDK runner helps) |
| **Example** | `lookup_building_code` | Web search | Memory, bash |

**Real-life analogy:**
Server tools are like ordering delivery - the restaurant cooks and you just receive the meal. Custom tools are cooking yourself from your own recipe.

⚠️ Web search can power a fact-check endpoint, but something being on the internet doesn't make it true - always double-check.

**Interview Tip:**
> "Server tools like web search, web fetch, and code execution are declared in the tools array and run by Anthropic, so the result comes back in the same response without an agent loop."

---

## Skills

### 🎯 Skills

**Definition:**
> Skills are folders of instructions, scripts, and resources - centered on a `SKILL.md` file - that Claude loads dynamically to perform specialized tasks your way.

**Simple meaning:**
A skill teaches Claude *how you* do something: your status report format, your review checklist, your release notes.

**Why it matters:**
- ✅ Standardizes output across a whole feature or team
- ✅ Loads progressively - only name and description at first, full skill when needed
- ✅ Upload once, attach to any request
- ✅ Can bundle scripts that do real work

**Real-life analogy:**
A skill is like a company's standard operating procedure binder - anyone who follows it produces the same report, in the same format, every time.

---

### ⚖️ Skills vs Tools

| Feature | Tools | Skills |
|---------|-------|--------|
| **Purpose** | Connect to data and actions | Teach a procedure |
| **Answers** | **What** Claude can do | **How** you want it done |
| **Example** | "Look up this code section" | "Generate the daily status report from this template" |

---

### 🔧 Upload and Attach a Skill

**Step 1: Upload once**
```python
skill = client.beta.skills.create(
    display_title="Status Report Generator",
    files=files_from_dir("status-report-skill"),  # folder containing SKILL.md
)

print(skill.id)  # reference this ID in future requests
```

**Step 2: Attach to a request**
```python
response = client.beta.messages.create(          # beta endpoint
    model="claude-sonnet-4-5",
    max_tokens=4096,
    betas=["skills-2025-10-02", "code-execution-2025-08-25"],
    container={
        "skills": [                               # a list - you can layer skills
            {"type": "custom", "skill_id": skill.id, "version": "latest"}
        ]
    },
    tools=[{"type": "code_execution_20250825", "name": "code_execution"}],
    messages=[{
        "role": "user",
        "content": f"Generate the daily status report from this activity log:\n\n{activity_log}",
    }],
)
```

**Key points:**
- ✅ Uses `client.beta.messages.create` with the skills beta header (beta at the time of the course)
- ✅ `container.skills` is a list - layer multiple skills on one call
- ✅ Pair with **code execution** when the procedure needs to run scripts

The user prompt is one line; sections, tone, and blocker handling all come from `SKILL.md`.

**Interview Tip:**
> "Tools are about what Claude can do and skills are about how you want it done; upload a skill once and attach it through `container.skills`, and it loads into context only when relevant."

---

## MCP

### 🎯 Model Context Protocol

**Definition:**
> MCP (Model Context Protocol) is a standard protocol through which service providers publish servers that expose their tools - with descriptions, schemas, and authentication - to Claude.

**Simple meaning:**
Instead of you writing and maintaining an Asana or Slack wrapper, Asana and Slack publish one, and Claude plugs into it.

**Why it matters:**
- ✅ The service provider maintains the integration, not you
- ✅ No tool schemas to write - Claude discovers them
- ✅ When the provider's API changes, you change nothing
- ✅ Works with any compliant server

**Real-life analogy:**
Custom integrations are like building your own adapter for every appliance. MCP is like a standard wall socket - each manufacturer builds the plug, and it just fits.

---

### ⚖️ Tools vs Skills vs MCP

| Feature | Tools | Skills | MCP |
|---------|-------|--------|-----|
| **Connects to** | Your internal systems | (Procedures, not systems) | Third-party services |
| **Who maintains it** | You | You | Service provider |
| **Example** | Your database | Report template | Linear, Slack, Asana |

**Remember:**
> "Tools are for your stuff, skills are for your processes, and MCP is for everyone else's stuff."

---

### 🔧 Connecting to an MCP Server

Two pieces work together:
- `mcp_servers` declares the connection (type, URL, name, optional auth token)
- An `mcp_toolset` entry in `tools` sets which of that server's tools Claude can use (all by default)

```python
import os
import anthropic

client = anthropic.Anthropic()

response = client.beta.messages.create(
    model="claude-opus-4-8",
    max_tokens=1000,
    messages=[{"role": "user", "content": "What tools do you have available?"}],
    mcp_servers=[{
        "type": "url",
        "url": "https://mcp.linear.app/mcp",
        "name": "linear",
        "authorization_token": os.environ["LINEAR_MCP_TOKEN"],   # from .env
    }],
    tools=[{"type": "mcp_toolset", "mcp_server_name": "linear"}],
    betas=["mcp-client-2025-11-20"],                              # MCP connector is beta
)
```

Claude **introspects** the server, gets its tool list and schemas, and picks one for the prompt.

---

### 🔐 Filtering Tools

**❌ Bad Example:**
```python
# Every Slack tool enabled - including posting and deleting
tools=[{"type": "mcp_toolset", "mcp_server_name": "slack"}]
```

**✅ Good Example:**
```python
# Disable everything, then allow only read tools
tools=[{
    "type": "mcp_toolset",
    "mcp_server_name": "slack",
    "default_config": {"enabled": False},
    "configs": {
        "search_messages": {"enabled": True},
        "list_channels": {"enabled": True},
    },
}]
```

**Benefits:**
- ✅ Read-only access - Claude can't post or delete by accident
- ✅ Fewer tool definitions taking up context

See **modelcontextprotocol.io** for available servers.

**Interview Tip:**
> "MCP moves integration maintenance to the service provider: declare the server in `mcp_servers`, grant access with an `mcp_toolset`, and scope it down with `default_config` and `configs`."

---

## Context Management

### 🎯 Context

**Definition:**
> Context is everything Claude sees on a given turn: the system prompt, message history, tool definitions and results, attached files and skills, and thinking blocks.

**Simple meaning:**
It's the input to every API call. You pay for it, it has a limit, and once the window is full the request fails.

**Why it matters:**
- ✅ Directly affects cost
- ✅ A full window fails the request
- ✅ Long-running agents hit limits faster than you'd expect, even with a million tokens
- ✅ The goal is to fit the *right* things in, not everything

**Real-life analogy:**
Context is like a backpack for a hike - you can't bring the whole house, so you pack what you need now and pick up supplies along the way.

---

### 🧩 The Four Patterns

| Pattern | Type | Solves |
|---------|------|--------|
| **Just-in-time context** | Design pattern | Window size |
| **Server-side compaction** | API feature | Window size in long conversations |
| **Prompt caching** | API feature | Cost |
| **Memory tool** | API feature | Statelessness across sessions |

**1. Just-in-time context**
Load only what's needed now; let tools pull in the rest. A compliance agent calls `lookup_building_code` instead of putting the whole code book in the system prompt.

**2. Server-side compaction**
The API summarizes old turns into one block when input crosses a trigger threshold.
```python
response = client.messages.create(
    model="claude-sonnet-4-5",
    max_tokens=1024,
    context_management={"edits": [{"type": "compact"}]},   # opt in
    messages=messages,
)
```

**3. Prompt caching**
Mark stable parts (system prompt, tool definitions, long documents) and reuse them across calls at a fraction of the cost. A 4,000-token system prompt called 100 times an hour adds up fast without caching.

**4. Memory tool**
- Claude reads and writes a memory directory through tool calls
- You implement the storage backend (files, database, encrypted store)
- Anthropic adds a system instruction telling Claude to check memory before starting

In production you usually layer all four. Pick the ones that match what's breaking: **cost**, **window size**, or **statelessness**.

**Interview Tip:**
> "Manage context with four patterns: load just in time, compact long conversations server-side, cache stable prompt parts to cut cost, and use the memory tool for state across sessions."

---

## What are Managed Agents?

### 🎯 Claude Managed Agents

**Definition:**
> Claude Managed Agents is a suite of APIs for building and deploying agents at scale, running the agent loop on Anthropic's infrastructure inside isolated containers with file system access, bash, and web search.

**Simple meaning:**
You define the agent and its sandbox, start a session from your app, and Anthropic runs the loop. You just watch the events.

**Why it matters:**
- ✅ No loop, sandbox, or resumability to build yourself
- ✅ Sessions run in parallel, each in its own container
- ✅ Tool calls stream back to your app in real time
- ✅ Built-in memory, MCP, rubrics, permissions, and multi-agent coordination

**Real-life analogy:**
Building your own agent loop is like running your own server room. Managed agents are like the cloud - you describe what you need, and someone else keeps the machines running.

---

### 🔍 Three Example Shapes

| Example | What Happens | Features Used |
|---------|--------------|---------------|
| **Kanban board** | Dragging a ticket to "In progress" starts a session that optimizes site performance; a grader checks a rubric (Lighthouse > 90) and Claude iterates to 96 | Sessions, environments, rubrics and graders, event stream, parallel sessions |
| **Weekly pricing research** | Tracks SaaS pricing changes, runs cost analysis in Python, writes an Excel report, posts to Slack and Asana, remembers last week's findings | Web search, code execution, skills, MCP, memory store |
| **Incident response** | An alert enters a session; a coordinator delegates to three specialists, checks past incidents in memory, and waits for approval before posting to Slack | Custom tools, multi-agent coordination, memory, permissions policy |

---

### 🏗️ Building Blocks

| Block | What It Is |
|-------|------------|
| **Agents** | Definitions with tools, personas, and capabilities |
| **Sessions** | Individual runs started from your app |
| **Environments** | Sandboxes with packages and network controls |
| **Tools** | Including custom tools on your back end |
| **MCP** | Connections to services like Slack and Asana |
| **Memory** | A store the agent reads before starting and writes when done |
| **Outcomes** | Rubrics and graders that define and check "done" |
| **Multi-agent coordination** | Coordinators delegating to specialists |

**Interview Tip:**
> "Managed agents host the agent loop on Anthropic's infrastructure in isolated containers, with sessions, environments, memory, MCP, rubrics, and multi-agent coordination - you define what done looks like and Claude works until it gets there."

---

## Building Your First Managed Agent

### 🎯 The Four Primitives

| Primitive | What It Is | Reusable? |
|-----------|------------|-----------|
| **Agent** | Persona: model, system prompt, toolset | ✅ Across many runs |
| **Environment** | Where it runs: cloud or local, networking | ✅ |
| **Session** | One run of an agent in an environment - the unit of work | ❌ One run |
| **Events** | Messages in and out: actions, tool calls, results, replies | - |

Your app talks to a session, the session drives work inside the environment, and everything flows back out through the event stream. You're not running a while loop - you send events and read events.

Managed agents are enabled by default for every API account.

**Real-life analogy:**
The agent is a job description, the environment is the office, the session is one shift, and events are the radio chatter you listen to while they work.

---

### 🔧 Step by Step: A Line Counter Agent

**Step 1: Create the agent** (uses the bundled agent toolset: file, bash, and web tools)
```python
import anthropic

client = anthropic.Anthropic()

agent = client.beta.agents.create(
    name="Line Counter",
    model="claude-opus-4-8",
    system="You are a helpful agent that completes small file tasks.",
    tools=[{"type": "agent_toolset_20260401", "default_config": {"enabled": True}}],
)
```

**Step 2: Create the environment**
```python
environment = client.beta.environments.create(
    name="line-counter-env",
    config={"type": "cloud", "networking": {"type": "unrestricted"}},
)
```

**Step 3: Create the session**
```python
session = client.beta.sessions.create(
    agent=agent.id,
    environment_id=environment.id,
    title="Count lines demo",
)
```

**Step 4-5: Open the stream first, send the kickoff, then consume events**
```python
# Open the stream BEFORE sending - it only delivers events after it opens
with client.beta.sessions.events.stream(session_id=session.id) as stream:
    client.beta.sessions.events.send(
        session_id=session.id,
        events=[{                                   # note: events, plural
            "type": "user.message",
            "content": [{"type": "text",
                         "text": "Create a file in the temp directory, count its lines, and report back."}],
        }],
    )

    for event in stream:
        if event.type == "agent.message":           # Claude's text
            for block in event.content:
                if block.type == "text":
                    print(block.text, end="", flush=True)
        elif event.type == "agent.tool_use":        # tool Claude picked
            print(f"\n[tool] {event.name}")
        elif event.type == "session.status_idle":   # agent is done
            print("\n--- Agent done ---")
            break
```

⚠️ **Gotcha:** Always open the event stream *before* sending the kickoff message, or you'll miss events.

---

### ⚖️ Manual Loop vs Managed Agent

| Feature | Manual Agent Loop | Managed Agent |
|---------|-------------------|---------------|
| **Who runs the loop** | Your server | Anthropic |
| **Sandbox** | You build it | ✅ Provided |
| **Resumability** | You build it | ✅ Provided |
| **Control** | ✅ Full | Less |
| **Best for** | Short, focused features | Long-running, file-heavy tasks |

**When to choose managed agents:**
- ✅ The loop runs for minutes or hours
- ✅ Many tools, files to write, state to keep
- ✅ Work must survive a network hiccup
- ❌ Avoid if you need full control over every step - write the loop yourself

**Example:** A file share cleanup agent walks a messy folder, moves files into project folders, archives duplicates and empty files, and flags anything it can't place - across thousands of files.

**Interview Tip:**
> "Create an agent, an environment, and a session, open the event stream, send events in, and read `agent.message`, `agent.tool_use`, and `session.status_idle` out - Anthropic runs the loop."

---

## Building with Claude Code

### 🎯 Let Claude Code Write the Integration

**Simple meaning:**
Instead of typing API code from memory, stub out the file, hand it to Claude Code, and review the diff.

**The Claude API skill:**
- Built into Claude Code; invoke with `/claude-api`
- Loads automatically when Claude Code detects the Claude SDK
- If missing, add it from the marketplace:

```bash
/plugin marketplace add AnthropicsSkills
```

(Note the **s** at the end of `Anthropics`.)

---

### 🔧 Writing the Prompt

A good prompt does three things:

| Element | Example |
|---------|---------|
| **Names the file** | "In `weather.ts`..." |
| **Names the pattern** | "...implement `getWeather` and `run` using the tool runner..." |
| **Names the end state** | "...then run it and show me the output." |

```text
In weather.ts, implement getWeather to return temperature and conditions for
a city, and implement run using the Claude TypeScript SDK's tool runner with
getWeather as a tool. Then execute the script and show me the output.
```

Claude Code fills in the stubs (in the course, using a Zod tool), adds a call at the bottom, runs the script, and fixes any errors in place.

**Real-life analogy:**
It's like giving a contractor a floor plan with labeled rooms - they build it, and you just inspect the result.

**The pattern to remember:**
1. Define a tool
2. Hand it to a runner
3. Return the result

**Interview Tip:**
> "Most Claude API code has the same shape - define a tool, hand it to a runner, return the result - so stub the file, give Claude Code a prompt naming the file, pattern, and end state, and review the diff."

---

## Choosing the Right Feature

### ⚖️ Feature Decision Guide

| Scenario | Use | Avoid |
|----------|-----|-------|
| One-shot text task (draft, summarize, review) | **`messages.create`** | An agent loop |
| Claude needs your data or actions | **Custom tools** | Pasting data into the prompt |
| Many tools, little boilerplate | **Tool runner** | Hand-written JSON schemas |
| Search, fetch, or run Python | **Server tools** | Building your own crawler or sandbox |
| Hard reasoning or trade-offs | **Extended thinking** | Thinking on simple classification |
| Repeatable output format or procedure | **Skills** | Copy-pasting templates into prompts |
| Third-party service (Slack, Linear, Asana) | **MCP** | Maintaining your own API wrapper |
| Long conversation or big repeated prompt | **Compaction + caching** | Letting the window overflow |
| State across sessions | **Memory tool** | Re-sending history every time |
| Long-running, file-heavy agent | **Managed agents** | Running the loop on your server |

---

## Common Interview Questions

### Basic Questions

**1. What is the Claude Platform?**
> "Anthropic's infrastructure for building with Claude in code: a REST API, SDKs, CLIs, and a Console, organized as primitives, infrastructure, and controls."

**2. What are the required parameters of `messages.create`?**
> "A model, a `max_tokens` limit, and a list of messages; a system prompt is optional but shapes behavior."

**3. Why is `response.content` an array?**
> "Claude can return several block types - text, tool calls, thinking - so you loop over the blocks and check each `type`."

**4. How do you choose a model?**
> "Run a small eval of 20-30 real examples from Haiku upward and pick the cheapest model whose output you'd ship."

**5. Where should API keys live?**
> "In an environment file like `.env.local`, never hardcoded in source, so they stay out of version control."

### Intermediate Questions

**1. Who executes a tool - Claude or your code?**
> "Your code; Claude only requests the tool call, and you return the output as a `tool_result` block."

**2. How does the agent loop know when to stop?**
> "It loops while `stop_reason` is `tool_use` and stops when it's `end_turn`."

**3. What's the difference between server tools and custom tools?**
> "Server tools like web search run on Anthropic's infrastructure and return results in the same response; custom tools run in your code inside an agent loop."

**4. Tools vs skills vs MCP?**
> "Tools are for your systems, skills are for your procedures, and MCP is for third-party services maintained by their providers."

**5. When should you use extended thinking?**
> "For math, debugging, multi-step logic, and trade-offs; skip it for simple classification or extraction because it adds latency and cost."

### Advanced Questions

**1. How do you keep a long-running agent within its context window?**
> "Load context just in time through tools, enable server-side compaction, cache stable prompt parts, and use the memory tool for state across sessions."

**2. How do you limit what an MCP server lets Claude do?**
> "Set `default_config` to disabled in the `mcp_toolset` and enable only specific tools in `configs`, e.g. read-only Slack search."

**3. When would you choose managed agents over your own loop?**
> "When the task runs for minutes or hours, touches many files and tools, and needs a sandbox and resumability; keep your own loop when you need full control."

**4. What are the managed agent primitives and how do they relate?**
> "An agent defines the persona, an environment defines where it runs, a session is one run, and events flow in and out through a stream you open before sending the kickoff."

**5. How would you route work across models in one product?**
> "Classify every input with Haiku, handle routine drafting with Sonnet, and send only complex, high-stakes tasks like RFP responses to Opus."

---

## 🎓 Summary

**Core ideas:**
1. **Build with primitives, scale on infrastructure, run with control**
2. **`messages.create`** = model + max tokens + messages (+ system prompt)
3. **Pick the cheapest model** whose output you'd ship
4. **Agents** are Claude in a loop; **tools** are run by your code
5. **Server tools, skills, and MCP** add search, procedures, and third-party services
6. **Context** needs managing: just-in-time, compaction, caching, memory
7. **Managed agents** run the loop for you on Anthropic's infrastructure

**Remember:**
> "You own the loop and the tools, Claude owns the reasoning - or delegate the whole loop with managed agents."

---

**Source:** [Claude Platform 101 - Anthropic Academy](https://anthropic.skilljar.com/claude-platform-101)
**Last Updated:** October 2026
