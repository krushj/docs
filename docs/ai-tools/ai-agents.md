# AI Agents Complete Guide

> Notes based on IBM's [What are AI agents?](https://www.ibm.com/think/topics/ai-agents) by Anna Gutowska. Code examples use the Anthropic Python SDK to match the [Claude Platform guide](claude/claude-platform-101.md); the concepts apply to any LLM.

## Table of Contents

### Foundations
- [What are AI Agents?](#what-are-ai-agents)
- [Agentic vs Nonagentic Chatbots](#agentic-vs-nonagentic-chatbots)

### How Agents Work
- [The Complete Agent Flow](#the-complete-agent-flow)
- [Goal Initialization and Planning](#goal-initialization-and-planning)
- [Reasoning with Available Tools](#reasoning-with-available-tools)
- [Learning and Reflection](#learning-and-reflection)

### Reasoning Paradigms
- [ReAct: Reasoning and Action](#react-reasoning-and-action)
- [ReWOO: Reasoning Without Observation](#rewoo-reasoning-without-observation)
- [ReAct vs ReWOO](#react-vs-rewoo)

### Types of AI Agents
- [The Five Agent Types](#the-five-agent-types)
- [Comparing Agent Types](#comparing-agent-types)

### In Practice
- [Use Cases](#use-cases)
- [Benefits](#benefits)
- [Risks and Limitations](#risks-and-limitations)
- [Best Practices](#best-practices)

### Interview Preparation
- [Common Interview Questions](#common-interview-questions)

---

## What are AI Agents?

### 🎯 AI Agents

**Definition:**
> An AI agent is a system that autonomously performs tasks by designing workflows with available tools.

**Simple meaning:**
An agent takes a goal, works out the steps, uses tools to fill in what it doesn't know, and keeps going until the goal is met.

**Why it matters:**
- ✅ Goes beyond language: decision-making, problem-solving, and taking actions in external systems
- ✅ Gets up-to-date information through tool calling instead of relying only on training data
- ✅ Breaks complex goals into subtasks on its own
- ✅ Adapts to users over time through memory

**Where they're used:**
- Software design and code generation
- IT automation
- Conversational assistance
- Enterprise workflows

**Real-life analogy:**
A plain LLM is like an expert who answers from memory. An AI agent is like an expert with a phone, a library card, and a team of specialists on call - when they don't know something, they go and find out.

---

### 🔧 LLMs at the Core

AI agents are often called **LLM agents** because a large language model is at their core.

| Feature | Traditional LLM | AI Agent |
|---------|-----------------|----------|
| **Knowledge** | Limited to training data | Fetches current data through tools |
| **Tasks** | Single response | Plans and runs subtasks |
| **Memory** | ❌ None between conversations | ✅ Stores past interactions |
| **Human input** | Needed every turn | Can work without intervention |

**Real-world example:**
Dynamiq built a multi-agent legal research assistant for an insurance client. A low-cost classifier model handles every query first and escalates only complex cases to a more capable research agent. This routing cut contract review time from **90 minutes to 45** while keeping every decision auditable.

**Interview Tip:**
> "An AI agent is an LLM-powered system that autonomously completes goals by planning subtasks, calling tools for information it lacks, and using memory to improve over time."

---

## Agentic vs Nonagentic Chatbots

### ⚖️ Chatbot vs Agent

**Key idea:**
> A chatbot is a *modality* (a way to interact); agency is a *technological framework* (a way to act).

| Feature | Nonagentic Chatbot | Agentic Chatbot |
|---------|--------------------|-----------------|
| **Tools** | ❌ | ✅ |
| **Memory** | ❌ | ✅ |
| **Reasoning and planning** | ❌ Short-term goals only | ✅ Plans ahead, considers options |
| **User input** | Needed continuously | Creates subtasks on its own |
| **User-specific questions** | Poor - doesn't know your data | Good - fills gaps with tools |
| **Learns from mistakes** | ❌ | ✅ Self-corrects and updates plans |

**Real-life analogy:**
A nonagentic chatbot is like a vending machine - press a button, get a fixed item. An agentic chatbot is like a personal assistant who remembers your preferences and runs errands to get what you need.

**Interview Tip:**
> "Nonagentic chatbots have no tools, memory, or planning and need constant input; agentic chatbots plan, call tools, remember, and self-correct to complete complex goals."

---

## The Complete Agent Flow

### 🏗️ End-to-End Flow

Every agent run passes through three stages: **goal initialization and planning**, **reasoning with tools**, and **learning and reflection**.

```text
┌──────────────────────────────────────────────────────────────────────┐
│ 1. GOAL INITIALIZATION                                               │
│    Developers (design/train) + Deployers (access) + User (goal,tools)│
└───────────────────────────────┬──────────────────────────────────────┘
                                ▼
┌──────────────────────────────────────────────────────────────────────┐
│ 2. PLANNING  - task decomposition into subtasks                      │
│    (skipped for simple tasks: the agent just reflects and improves)  │
└───────────────────────────────┬──────────────────────────────────────┘
                                ▼
┌──────────────────────────────────────────────────────────────────────┐
│ 3. REASONING WITH TOOLS  (repeat per subtask)                        │
│    Perceive → find knowledge gap → call tool (data, web, API, agent) │
│    → update knowledge base → reassess plan → self-correct            │
└───────────────────────────────┬──────────────────────────────────────┘
                                ▼
┌──────────────────────────────────────────────────────────────────────┐
│ 4. RESPONSE  - combine findings, present to user                     │
└───────────────────────────────┬──────────────────────────────────────┘
                                ▼
┌──────────────────────────────────────────────────────────────────────┐
│ 5. LEARNING AND REFLECTION                                           │
│    Feedback (user / HITL / other agents) → store in memory           │
│    → iterative refinement for future goals                           │
└──────────────────────────────────────────────────────────────────────┘
```

---

### 🔍 Walkthrough: The Surfing Trip

**Goal:** "Which week next year will likely have the best weather for my surfing trip in Greece?"

| Step | What the Agent Does |
|------|---------------------|
| **1. Goal** | User sets the goal; the agent has a weather database and a surfing-expert agent available |
| **2. Plan** | Splits into subtasks: get historical weather → learn ideal surf conditions → match them |
| **3. Tool: weather DB** | The LLM doesn't specialize in weather, so it queries daily weather reports for Greece over past years |
| **4. Gap found** | Still doesn't know what "good surfing weather" means → creates a new subtask |
| **5. Tool: surf agent** | Asks a surfing agent and learns: high tides, sun, little to no rain |
| **6. Combine** | Finds weeks with that pattern in the weather data |
| **7. Respond** | Presents the most likely week |
| **8. Learn** | Stores what it learned plus the user's feedback for future requests |

Sharing information between tools is what makes agents more general purpose than traditional AI models.

**Interview Tip:**
> "An agent run goes goal → plan → reason with tools (repeatedly filling knowledge gaps and self-correcting) → respond → learn from feedback and store it in memory."

---

## Goal Initialization and Planning

### 🎯 Goals and Task Decomposition

**Definition:**
> Agents act autonomously but within goals and rules set by humans; given a goal and tools, they perform task decomposition - creating a plan of tasks and subtasks.

**Simple meaning:**
Humans decide *what* the agent should achieve and *what it may use*. The agent decides *how*, by breaking the goal into steps.

**Three influences on agent behavior:**

| Who | Role |
|-----|------|
| **Developers** | Design and train the agentic AI system |
| **Deployers** | Deploy the agent and give users access |
| **User** | Sets the specific goal and which tools are available |

**When to plan:**
- ✅ Complex, multi-step goals → decompose into subtasks
- ❌ Simple tasks → skip planning; the agent iteratively reflects on and improves its answer

**Real-life analogy:**
Task decomposition is like planning a wedding - "have a wedding" becomes book a venue, hire a caterer, send invitations, each with its own smaller steps.

**Interview Tip:**
> "Humans set the goals, rules, and tools; the agent then decomposes the goal into subtasks, though simple tasks can skip planning and rely on iterative reflection."

---

## Reasoning with Available Tools

### 🔧 Tool Calling and Agentic Reasoning

**Definition:**
> When an agent lacks knowledge for a subtask, it calls tools - external datasets, web searches, APIs, or other agents - updates its knowledge base, and keeps reassessing its plan (agentic reasoning).

**Simple meaning:**
The agent notices what it doesn't know, looks it up, and changes its plan based on what it finds.

**Why it matters:**
- ✅ Bridges the gap between training data and the real world
- ✅ Enables self-correction mid-task
- ✅ Lets one agent draw on many specialized sources
- ✅ Makes decisions more informed and adaptive

| Tool Type | Example |
|-----------|---------|
| **External datasets** | Historical weather database |
| **Web search** | Current prices, news |
| **APIs** | CRM, ticketing, payment systems |
| **Other agents** | A specialist agent (e.g. surfing expert) |

**Real-life analogy:**
It's like a detective solving a case - each clue changes where they look next, and a dead end means rethinking the plan.

**Interview Tip:**
> "Agents call tools - datasets, web search, APIs, or other agents - to fill knowledge gaps, then update their knowledge and reassess the plan, which is called agentic reasoning."

---

## Learning and Reflection

### 🎯 Feedback and Iterative Refinement

**Definition:**
> Agents improve accuracy using feedback from humans (human-in-the-loop, HITL) and other agents, storing what they learn so future responses improve - a process called iterative refinement.

**Simple meaning:**
After answering, the agent remembers what worked, what the user said, and how it solved past problems.

**Feedback sources:**

| Source | When It Helps |
|--------|---------------|
| **User / HITL** | Throughout actions and reasoning, to align with the intended goal |
| **Other agents** | Reduces how much time humans spend giving direction |
| **Knowledge base** | Stores solutions to past obstacles so mistakes aren't repeated |

**Real-life analogy:**
It's like a chef keeping a notebook - every customer comment and every fixed recipe goes in, so next time the dish comes out better.

**Interview Tip:**
> "Agents learn through feedback from users, human-in-the-loop review, and other agents, and store solutions in memory so iterative refinement improves future results."

---

## ReAct: Reasoning and Action

### 🎯 ReAct

**Definition:**
> ReAct is a reasoning paradigm where the agent thinks and plans after every action and tool response to decide the next step, in a Think → Act → Observe loop.

**Simple meaning:**
Think, do one thing, look at the result, think again. Repeat until done.

**Why it matters:**
- ✅ Adapts on the fly to each tool result
- ✅ Visible "thoughts" show how the answer was formed
- ✅ Good when the next step depends on what was just found
- ✅ A form of Chain-of-Thought prompting

**Real-life analogy:**
ReAct is like driving without GPS in a new city - check the street sign, turn, check again.

---

### 🔧 How It Works

```text
          ┌─────────┐
  Goal →  │  THINK  │ ← "What do I know? What's next?"
          └────┬────┘
               ▼
          ┌─────────┐
          │   ACT   │ ← call a tool
          └────┬────┘
               ▼
          ┌─────────┐
          │ OBSERVE │ ← read the tool result, add to context
          └────┬────┘
               │ not done → back to THINK
               ▼ done
            Answer
```

```python
import anthropic

client = anthropic.Anthropic()

# Tools the agent can choose from
tools = [
    {
        "name": "get_weather_history",
        "description": "Get average weekly weather (sun hours, rain, tide) for a location over past years.",
        "input_schema": {
            "type": "object",
            "properties": {"location": {"type": "string"}},
            "required": ["location"],
        },
    },
    {
        "name": "ask_surf_expert",
        "description": "Ask a surfing specialist agent a question about surf conditions.",
        "input_schema": {
            "type": "object",
            "properties": {"question": {"type": "string"}},
            "required": ["question"],
        },
    },
]

def run_tool(name, tool_input):
    # Mock tools - in a real app these hit a database and another agent
    if name == "get_weather_history":
        return "Week 24: 11h sun, 2mm rain, high tide | Week 30: 12h sun, 0mm rain, low tide"
    if name == "ask_surf_expert":
        return "Best surfing: high tides, sunny weather, little to no rain."
    raise ValueError(f"Unknown tool: {name}")

messages = [{
    "role": "user",
    "content": "Which week next year is best for a surfing trip in Greece? "
               "Think step by step and explain each thought before acting.",
}]

# ReAct loop: Think (model turn) → Act (tool call) → Observe (tool result)
while True:
    response = client.messages.create(
        model="claude-sonnet-4-6",
        max_tokens=1024,
        tools=tools,
        messages=messages,
    )
    messages.append({"role": "assistant", "content": response.content})

    if response.stop_reason != "tool_use":
        print(response.content[-1].text)   # final answer
        break

    observations = [
        {"type": "tool_result", "tool_use_id": block.id,
         "content": run_tool(block.name, block.input)}
        for block in response.content if block.type == "tool_use"
    ]
    messages.append({"role": "user", "content": observations})
# Output: Week 24 - it has high tide, lots of sun, and little rain
```

**Interview Tip:**
> "ReAct interleaves reasoning and acting in a Think-Act-Observe loop, deciding each next tool call from the last result, like Chain-of-Thought with tools."

---

## ReWOO: Reasoning Without Observation

### 🎯 ReWOO

**Definition:**
> ReWOO is a reasoning paradigm where the agent plans all tool calls upfront, without depending on intermediate tool outputs, then executes them and combines the results.

**Simple meaning:**
Make the whole plan first, run the tools, then write the answer.

**Why it matters:**
- ✅ Avoids redundant tool calls
- ✅ Uses fewer tokens and less compute
- ✅ Less damage if an intermediate tool fails
- ✅ The user can review and approve the plan before it runs

**Real-life analogy:**
ReWOO is like writing a full shopping list before going to the store - one trip, no wandering back and forth.

---

### 🔧 The Three Modules

| Module | What It Does |
|--------|--------------|
| **1. Planner** | Anticipates all steps and tool calls from the user's prompt |
| **2. Worker** | Runs the planned tool calls and collects outputs |
| **3. Solver** | Combines the plan with the tool outputs to write the answer |

```python
import json
import anthropic

client = anthropic.Anthropic()
MODEL = "claude-sonnet-4-6"

def ask(prompt):
    reply = client.messages.create(
        model=MODEL, max_tokens=1024,
        messages=[{"role": "user", "content": prompt}],
    )
    return reply.content[0].text

goal = "Which week next year is best for a surfing trip in Greece?"

# 1. PLANNER - all tool calls decided upfront, as JSON
plan = json.loads(ask(
    f"Goal: {goal}\n"
    "Available tools: get_weather_history(location), ask_surf_expert(question).\n"
    'Reply with only a JSON list of steps like '
    '[{"tool": "...", "input": "..."}].'
))
print("Plan for user approval:", plan)   # user can confirm before execution

# 2. WORKER - run every planned step (run_tool from the ReAct example)
evidence = [
    {"step": step, "result": run_tool(step["tool"], {"location": step["input"], "question": step["input"]})}
    for step in plan
]

# 3. SOLVER - combine plan + evidence into the final answer
print(ask(f"Goal: {goal}\nEvidence: {json.dumps(evidence)}\nAnswer the goal using only this evidence."))
```

**Interview Tip:**
> "ReWOO separates planning from observation: a planner decides every tool call upfront, a worker runs them, and a solver combines the results, which saves tokens and lets a human approve the plan first."

---

## ReAct vs ReWOO

### ⚖️ Comparison

| Feature | ReAct | ReWOO |
|---------|-------|-------|
| **Planning** | Step by step, after each observation | All upfront |
| **Depends on tool outputs to plan** | ✅ | ❌ |
| **Token usage** | Higher - context grows each loop | Lower |
| **Adapts to surprises** | ✅ Strong | ❌ Weak - plan is fixed |
| **Tool failure impact** | Can recover next step | Smaller blast radius, but no replanning |
| **Human review of plan** | Hard - plan emerges over time | ✅ Easy - review before execution |
| **Best for** | Exploratory, unpredictable tasks | Predictable, well-defined tasks |

##### ⚖️ Trade-offs

| Benefit | Cost |
|---------|------|
| **ReAct: flexible, self-correcting** | More tokens, risk of loops |
| **ReWOO: efficient, reviewable** | Can't react to unexpected results |

**When to choose ReAct:**
- ✅ Next step depends on what you just learned
- ✅ The environment is uncertain
- ❌ Avoid if cost and token usage must be tightly controlled

**When to choose ReWOO:**
- ✅ Steps are predictable from the start
- ✅ A human must approve actions first
- ❌ Avoid if tool results will often change the plan

**Interview Tip:**
> "ReAct plans after every observation, so it's adaptive but token-heavy; ReWOO plans everything upfront, so it's efficient and reviewable but can't adapt mid-run."

---

## The Five Agent Types

Agent types are ordered from simplest to most advanced.

### 🧩 1. Simple Reflex Agents

**Definition:**
> Agents that act only on current perception using fixed condition-action rules, with no memory and no interaction with other agents.

**Simple meaning:**
"If this happens, do that." Nothing more.

- ✅ Work well in fully observable environments
- ❌ Fail in situations they weren't programmed for

**Example:** A thermostat that turns on the heating at 8 PM every night.

**Real-life analogy:** A motion-sensor light - it turns on when something moves, and that's all it knows.

---

### 🧩 2. Model-Based Reflex Agents

**Definition:**
> Agents that combine current perception with memory to maintain an internal model of the world, updated as new information arrives.

**Simple meaning:**
Still rule-based, but it remembers what it has seen.

- ✅ Work in partially observable, changing environments
- ❌ Still limited by their rules

**Example:** A robot vacuum that steers around furniture and remembers which areas it has cleaned so it doesn't loop.

---

### 🧩 3. Goal-Based Agents

**Definition:**
> Agents with an internal world model and one or more goals; they search for and plan action sequences that reach the goal before acting.

**Simple meaning:**
It knows where it wants to end up and plans a way there.

- ✅ More effective than reflex agents thanks to search and planning

**Example:** A navigation system that recommends the fastest route, switching if a quicker one appears.

---

### 🧩 4. Utility-Based Agents

**Definition:**
> Agents that choose the action sequence that reaches the goal *and* maximizes utility, scored by a utility function over criteria like progress, time, and cost.

**Simple meaning:**
Many paths reach the goal; it picks the best one.

- ✅ Useful when several scenarios achieve the goal and the optimal one must be chosen

**Example:** A navigation system that optimizes fuel efficiency, time in traffic, and toll cost together.

---

### 🧩 5. Learning Agents

**Definition:**
> Agents that have the capabilities of the other types and also learn autonomously, adding new experiences to their knowledge base.

**Simple meaning:**
It gets better the more it works.

| Component | Role |
|-----------|------|
| **Learning** | Improves knowledge from the environment through percepts and sensors |
| **Critic** | Judges whether responses meet the performance standard |
| **Performance** | Selects actions based on what was learned |
| **Problem generator** | Proposes new actions to try |

**Example:** E-commerce recommendations that track your activity and get more accurate over time.

---

### 🔧 Code: Reflex vs Utility-Based

```python
# Simple reflex agent: one fixed rule, no memory
def thermostat(hour):
    return "heat_on" if hour == 20 else "idle"

# Utility-based agent: score every option, pick the best
routes = [
    {"name": "Highway", "minutes": 30, "fuel_l": 4.0, "tolls": 5},
    {"name": "City",    "minutes": 45, "fuel_l": 3.0, "tolls": 0},
    {"name": "Scenic",  "minutes": 60, "fuel_l": 3.5, "tolls": 0},
]

def utility(route):
    # Higher is better: penalize time, fuel, and tolls with weights
    return -(route["minutes"] * 1.0 + route["fuel_l"] * 5 + route["tolls"] * 2)

best = max(routes, key=utility)
print(thermostat(20), best["name"])
# Output: heat_on City
```

---

## Comparing Agent Types

### 📊 Comparison

| Feature | Simple Reflex | Model-Based | Goal-Based | Utility-Based | Learning |
|---------|---------------|-------------|------------|---------------|----------|
| **Memory** | ❌ | ✅ | ✅ | ✅ | ✅ |
| **World model** | ❌ | ✅ | ✅ | ✅ | ✅ |
| **Goals** | ❌ | ❌ | ✅ | ✅ | ✅ |
| **Optimizes "best" path** | ❌ | ❌ | ❌ | ✅ | ✅ (if utility-based) |
| **Learns over time** | ❌ | ❌ | ❌ | ❌ | ✅ |
| **Environment** | Fully observable | Partially observable | Planned | Many valid options | Unfamiliar |
| **Example** | Thermostat | Robot vacuum | Fastest route | Cheapest/fastest route | Recommendations |

**Remember:**
> "Reflex reacts, model-based remembers, goal-based plans, utility-based optimizes, and learning agents improve."

**Interview Tip:**
> "The five types build on each other: simple reflex follows rules, model-based adds memory, goal-based adds planning, utility-based picks the best plan, and learning agents improve from experience."

---

## Use Cases

### 🌐 Where Agents Are Used

| Domain | How Agents Help |
|--------|-----------------|
| **Customer experience** | Virtual assistants, mental health support, interview simulation; many no-code templates exist |
| **Healthcare** | Multi-agent systems for emergency-department treatment planning and drug process management |
| **Emergency response** | Find people needing rescue from social media posts and map their locations for rescue teams |
| **Finance and supply chain** | Analyze real-time financial data, anticipate market trends, optimize supply chains |
| **Legal** | Route queries through a cheap classifier, escalate complex ones to a research agent |

**Interview Tip:**
> "Agents are used in customer experience, healthcare, emergency response, finance, and supply chain - anywhere multi-step decisions need current data and tools."

---

## Benefits

### ✅ Why Use Agents

| Benefit | Explanation |
|---------|-------------|
| **Task automation** | Automates complex work that would need people - cheaper, faster, at scale |
| **Greater performance** | Multi-agent frameworks tend to beat single agents; more plans mean more learning and reflection |
| **Quality of responses** | More comprehensive, accurate, and personalized, through tools, other agents, and memory |

**Real-life analogy:**
A multi-agent system is like a hospital team - a specialist for each area, sharing notes, gives better care than one generalist.

**Interview Tip:**
> "Agents automate complex tasks at scale, multi-agent setups outperform single agents through shared learning, and tools plus memory produce more accurate, personalized responses."

---

## Risks and Limitations

### ⚠️ What Can Go Wrong

| Risk | What Happens | Mitigation |
|------|--------------|------------|
| **Multi-agent dependencies** | Agents on the same foundation model share weaknesses; one flaw can fail the whole system or open it to attacks | Strong data governance, thorough training and testing, activity logs |
| **Infinite feedback loops** | Agents that can't plan or reflect keep calling the same tools | Real-time human monitoring, interruptibility, step limits |
| **Computational complexity** | Building agents is slow and expensive; complex tasks can take days | Start with existing models and frameworks; route simple work to cheaper models |
| **Data privacy** | Unsupervised agents in dev, pricing, or customer systems can expose sensitive data | Security protocols, guardrails, human oversight |

**❌ Bad Example:**
```python
# No step limit - an agent that never reaches end_turn runs forever
while True:
    response = call_agent(messages)
    if response.done:
        break
```

**✅ Good Example:**
```python
MAX_STEPS = 10   # guard against infinite feedback loops

for step in range(MAX_STEPS):
    response = call_agent(messages)
    if response.done:
        break
else:
    # Hit the limit: stop and hand over to a human instead of looping
    escalate_to_human(messages)
```

**Interview Tip:**
> "Key risks are shared failures across multi-agent systems, infinite tool-calling loops, high compute cost, and data privacy, mitigated with governance, step limits, monitoring, and guardrails."

---

## Best Practices

### 🚀 Building Agents Responsibly

**1. Activity logs**
Give users a log of agent actions, including tools and external agents used. This makes decisions transparent, helps catch errors, and builds trust.

**2. Interruption**
Let humans gracefully stop a sequence of actions or the whole run - especially for infinite loops, changed tool access, or design flaws. Choose carefully: stopping a faulty agent mid-emergency can sometimes do more harm than letting it continue.

**3. Unique agent identifiers**
Require agents to carry identifiers when accessing external systems, so developers, deployers, and users can be traced if something goes wrong.

**4. Human supervision**
Give human feedback in the early stages in a new environment, and **require human approval before high-impact actions** like sending mass emails or financial trading.

```python
HIGH_IMPACT = {"send_mass_email", "execute_trade"}

def run_tool_safely(name, tool_input, agent_id, log):
    # Activity log + unique identifier on every action
    log.append({"agent": agent_id, "tool": name, "input": tool_input})

    # Human approval before high-impact actions
    if name in HIGH_IMPACT:
        answer = input(f"[{agent_id}] wants to run {name}({tool_input}). Approve? (y/n) ")
        if answer.lower() != "y":
            return "Action rejected by human reviewer."

    return run_tool(name, tool_input)
```

| Practice | Addresses |
|----------|-----------|
| **Activity logs** | Multi-agent dependencies, trust, debugging |
| **Interruption** | Infinite loops, malfunctions |
| **Unique identifiers** | Accountability, malicious use |
| **Human supervision** | High-risk actions, early learning |

**Interview Tip:**
> "Build agents with activity logs for transparency, interruptibility to stop runaway loops, unique identifiers for accountability, and human approval before high-impact actions."

---

## Common Interview Questions

### Basic Questions

**1. What is an AI agent?**
> "A system that autonomously performs tasks by designing workflows with available tools, usually with an LLM at its core."

**2. How is an agent different from a regular LLM?**
> "A regular LLM answers from training data; an agent calls tools for current information, plans subtasks, and uses memory to improve."

**3. What are the three stages of how agents work?**
> "Goal initialization and planning, reasoning with available tools, and learning and reflection."

**4. What is task decomposition?**
> "Breaking a complex goal into a plan of smaller tasks and subtasks the agent can complete one by one."

**5. What is human-in-the-loop?**
> "A feedback mechanism where people review or guide the agent's actions and reasoning to keep results aligned with the goal."

### Intermediate Questions

**1. What's the difference between ReAct and ReWOO?**
> "ReAct reasons after every tool result in a Think-Act-Observe loop; ReWOO plans all tool calls upfront, then runs them and combines the results."

**2. Name the five types of AI agents.**
> "Simple reflex, model-based reflex, goal-based, utility-based, and learning agents."

**3. Goal-based vs utility-based agents?**
> "Goal-based agents find any path to the goal; utility-based agents find the path that maximizes a utility function, like least time and cost."

**4. What are the components of a learning agent?**
> "Learning, critic, performance, and problem generator."

**5. Agentic vs nonagentic chatbots?**
> "Nonagentic chatbots have no tools, memory, or planning; agentic chatbots plan, use tools, remember, and self-correct."

### Advanced Questions

**1. How do you prevent infinite feedback loops?**
> "Cap the number of steps, let humans interrupt, monitor in real time, and improve planning and reflection so the agent doesn't repeat tool calls."

**2. Why might multi-agent systems fail together?**
> "Agents built on the same foundation model share the same weaknesses, so one flaw or attack can break every agent at once."

**3. When would you choose ReWOO over ReAct?**
> "When steps are predictable, token cost matters, or a human must approve the plan before anything runs."

**4. How would you make an enterprise agent safe?**
> "Activity logs, interruptibility, unique agent identifiers, least-privilege tool access, and human approval before high-impact actions."

**5. How would you reduce cost in a multi-agent system?**
> "Route requests through a cheap classifier model first and escalate only complex cases to a more capable agent, as in the legal research example."

---

## 🎓 Summary

**Core ideas:**
1. **AI agents** autonomously complete goals by designing workflows with tools
2. **Flow:** goal → plan → reason with tools → respond → learn
3. **ReAct** thinks after every action; **ReWOO** plans everything upfront
4. **Five types:** simple reflex, model-based, goal-based, utility-based, learning
5. **Benefits:** automation, multi-agent performance, better responses
6. **Risks:** shared failures, infinite loops, cost, privacy
7. **Best practices:** logs, interruption, identifiers, human approval

**Remember:**
> "An agent is an LLM with goals, tools, and memory - give it guardrails as carefully as you give it capabilities."

---

**Source:** [What are AI agents? - IBM Think](https://www.ibm.com/think/topics/ai-agents)
**Last Updated:** October 2026
