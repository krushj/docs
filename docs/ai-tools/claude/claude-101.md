# Claude 101 Complete Guide

> Notes based on the [Claude 101](https://anthropic.skilljar.com/claude-101) course from Anthropic Academy. Plan availability and feature names change often; check the [Anthropic Help Center](https://support.claude.com) for the latest.

## Table of Contents

### Meet Claude
- [What is Claude?](#what-is-claude)
- [Your First Conversation with Claude](#your-first-conversation-with-claude)
- [Getting Better Results](#getting-better-results)
- [Working with Claude on Your Desktop](#working-with-claude-on-your-desktop)

### Organizing Your Work and Knowledge
- [Introduction to Projects](#introduction-to-projects)
- [Creating with Artifacts](#creating-with-artifacts)
- [Working with Skills](#working-with-skills)

### Expanding Claude's Reach
- [Connecting Your Tools](#connecting-your-tools)
- [Enterprise Search](#enterprise-search)
- [Research for Deep Dives](#research-for-deep-dives)

### Putting It All Together
- [Claude in Action: Use Cases by Role](#claude-in-action-use-cases-by-role)
- [Other Ways to Work with Claude](#other-ways-to-work-with-claude)
- [Choosing the Right Feature](#choosing-the-right-feature)

### Interview Preparation
- [Common Interview Questions](#common-interview-questions)

---

## What is Claude?

### 🎯 Claude as a Thinking Partner

**Definition:**
> Claude is an AI assistant for life and work, trained with Constitutional AI to align with human values, avoid harmful outputs, and behave as a safe and beneficial system.

**Simple meaning:**
Claude is more than a chatbot. It's a thinking partner that helps you work through complex problems, not just answer simple questions.

**Why it matters:**
- ✅ Handles summarization, search, writing, Q&A, coding, and more with high reliability
- ✅ Steerable - takes direction on personality, tone, and behavior
- ✅ Can both automate *and* augment your work
- ✅ Available on every plan (Free, Pro, Max, Team, Enterprise) with conversations, projects, memory, and preferences synced across devices

**Real-life analogy:**
Claude is like a sharp colleague who has read a huge library - you bring the context and expertise, and they help you think, draft, and analyze.

---

### 🧩 What Claude Excels At

| Area | What Claude Does |
|------|------------------|
| **Writing and content** | Social posts, emails, complex reports - iterating on structure, clarity, and your voice |
| **Research and analysis** | Explores angles, compiles findings, analyzes data from uploaded documents |
| **Coding** | Writes, debugs, and explains code across many languages |
| **Problem-solving** | Math, strategy, analysis; can answer instantly or use **Thinking** to reason step by step first |
| **Learning** | Adapts to your pace; **Learning mode** guides your reasoning instead of handing you answers |

**Context window:**
Claude can take in 200K+ tokens (about 500 pages of text), and up to 1M tokens on Pro, Max, Team, and Enterprise with supported models. That lets it consider large materials in one conversation.

---

### 🌐 Ways to Access Claude

Claude is the intelligence; it's available through several interfaces.

| Interface | What It Is |
|-----------|------------|
| **Claude.ai** (web, desktop, mobile) | The main way to chat, brainstorm, write, research, analyze, and create files - the focus of this course |
| **Claude Code** | Agentic coding tool that edits files, runs commands, and makes commits |
| **Claude Tag** | Claude inside Slack - chat in any channel or tag Claude in threads |
| **Claude Design** | Turns ideas, sketches, or screenshots into interactive prototypes |
| **Claude for Microsoft 365** | Sidebar in Excel, PowerPoint, Word, and Outlook |

**Interview Tip:**
> "Claude is Anthropic's AI assistant, trained with Constitutional AI to be safe and steerable, and it works as a thinking partner for writing, research, coding, and reasoning across web, desktop, mobile, and tools like Slack and Microsoft 365."

---

## Your First Conversation with Claude

### 🎯 Writing Effective Prompts

**Definition:**
> A prompt is the message that starts every interaction; together with any other context, it shapes Claude's response.

**Simple meaning:**
Talk to Claude like a coworker - naturally, concisely, and conversationally. You bring the context, Claude brings the intelligence.

**The three elements of a good prompt:**

| Element | Question to Answer |
|---------|--------------------|
| **Setting the stage** | What is your role, objective, and relevant context? |
| **Defining the task** | What action should Claude take - write, analyze, build? |
| **Specifying rules** | What style, tone, format, or examples should it follow? |

**Real-life analogy:**
A prompt is like briefing a freelancer - who you are, what you need, and how you want it delivered.

---

**❌ Bad Example:**
```text
Tell me about the streaming market.
```

**Problems:**
- No role or goal
- No clear task or scope
- No format or sourcing rules

**✅ Good Example:**
```text
I'm the marketing lead at an indie streaming startup, and we're preparing an
investor pitch deck for Series A investors. Can you research the current state
of the independent film streaming market and identify key trends, competitor
positioning, and growth opportunities? Use current web research with citations
and structure it as a professional report of up to 5 pages, with an executive
summary, market analysis, competitive landscape, and growth opportunities.
```

**Why it works:**
- ✅ **Stage:** investor pitch deck for an indie streaming startup
- ✅ **Task:** research the market (trends, competitors, opportunities)
- ✅ **Rules:** web research with citations, a structured report of up to 5 pages

This framework comes from the **4D Framework for AI Fluency** (see [Getting Better Results](#getting-better-results)).

---

### 🔧 Adding Context

**File uploads:**
Claude reads text *and* visuals (images, charts, graphics) in PDF, DOCX, CSV, TXT, PNG, JPEG, and more.

- Upload a document → summarize key points
- Share an image → describe or analyze it
- Attach a spreadsheet → find trends
- Upload code → explain it or find bugs

**💡 Pro tip:** Set preferences for every conversation under **Settings > Account > Instructions for Claude**.

---

### 🔍 Iterating on Responses

Conversations are meant to be iterative. Chain bite-sized prompts and guide Claude based on its replies.

| Option | Example |
|--------|---------|
| **Ask follow-ups** | "Can you expand on the second point?" |
| **Give feedback** | "Good, but the tone is too formal. Make it more conversational." |
| **Redirect** | "Actually, I was asking about X, not Y." |
| **Restart** | Open a new chat to fully refresh the context |

**💡 Pro tip:** Click the pencil icon on any of your messages to edit and resubmit it.

---

### 🧩 Personalizing Claude

| Feature | What It Does |
|---------|--------------|
| **Memory** | Saves key context (role, preferences, decisions, working style) across chats; review, edit, or delete it in Settings; syncs across devices |
| **Skills** | Reusable instructions for specific tasks and workflows, applied automatically when relevant (see [Working with Skills](#working-with-skills)) |

**Interview Tip:**
> "A good prompt sets the stage, defines the task, and specifies rules, and the real value comes from iterating - follow-ups, feedback, and redirection - rather than one-off prompts."

---

## Getting Better Results

### 🎯 Common Challenges and Fixes

| Challenge | What's Happening | Try This |
|-----------|------------------|----------|
| **Too generic** | Not enough context about your situation | Add audience, role, constraints |
| **Too long or short** | Claude is guessing the length | Be explicit: "two paragraphs", "under 100 words" |
| **Ignored my format** | Claude knows *what*, not *how* | Show an example or describe the structure |
| **Confident but wrong** | Plausible but incorrect facts, especially niche ones | Verify key facts, ask for sources or confidence, turn on web search |
| **Wrong tone** | Defaults to helpful and professional | Describe the tone plainly or share a sample |

**❌ Bad Example:**
```text
Write an email about the project delay.
```

**✅ Good Example:**
```text
Write an email to our enterprise client explaining that the software
integration will be delayed by two weeks. They've been patient so far but
this is the second delay. Keep it professional but apologetic.
```

---

### 🔍 The Iteration Mindset

**Simple meaning:**
Your first prompt rarely gives a perfect result, and that's okay. It starts a conversation; it's not a one-shot request.

**Effective Claude users:**
- ✅ **Treat first drafts as starting points** - review, then refine
- ✅ **Give specific feedback** - "Cut the first two paragraphs and make the conclusion more action-oriented" beats "make it shorter"
- ✅ **Know when to start fresh** - a new chat with a clearer prompt can be faster than redirecting

**Real-life analogy:**
Working with Claude is like sculpting - the first pass gets the rough shape, and each round of feedback adds detail.

---

### 🎓 AI Fluency and the 4D Framework

**Definition:**
> AI Fluency is the ability to collaborate effectively with AI tools - not just knowing which buttons to click, but having the judgment to use AI well.

The **4D Framework** (Prof. Rick Dakan and Prof. Joseph Feller) defines four competencies:

| Competency | What It Means |
|------------|---------------|
| **Delegation** | Deciding what work humans do, what AI does, and how to split it |
| **Description** | Communicating clearly with AI - outputs, process, behavior |
| **Discernment** | Critically evaluating AI outputs for quality, accuracy, and fit |
| **Diligence** | Using AI responsibly, transparently, and with accountability |

The prompt framework (stage, task, rules) is **Description**. The troubleshooting above draws on **Discernment** and **Diligence**.

---

### 📊 Evaluating Claude for Your Workflows

**Definition:**
> Evals (evaluations) are systematic tests of how well Claude performs on specific tasks that matter to you.

**Why it matters:**
- ✅ Shows where Claude adds the most value
- ✅ Reveals where you need more context or examples
- ✅ Builds confidence for recurring tasks

**A simple eval approach:**
1. **Gather examples** - 5-10 samples of a task you do regularly
2. **Create test prompts** - with the context you'd normally have
3. **Compare outputs** - key info captured? Tone right? What's missing?
4. **Refine** - adjust prompts, add examples, or mark where human review is essential

**Example with data:** take a dataset you already analyzed by hand, ask Claude to do the same analysis, compare results, and note patterns (e.g. right numbers, but missed the overall trend).

**Interview Tip:**
> "Fix weak results with more context, explicit length and format, and verification; use the 4D Framework - Delegation, Description, Discernment, Diligence - and run simple evals on your own examples to see where Claude fits."

---

## Working with Claude on Your Desktop

### 🎯 Three Shapes of Work

**Definition:**
> The Claude desktop app supports three shapes of work: working turn by turn (Chat), handing work off (Cowork), and building software (Claude Code).

**Simple meaning:**
Notice what kind of work is in front of you, and the right tab follows.

| Shape | What It Looks Like | Where It Lives |
|-------|--------------------|----------------|
| **Turn by turn** | You ask, Claude answers, you steer, it revises | **Chat** |
| **Handing work off** | You describe an outcome; Claude plans, does it, returns the result | **Cowork** |
| **Building software** | Claude reads, writes, tests code and runs commands | **Code tab** |

**Real-life analogy:**
Chat is a conversation with a colleague at the whiteboard. Cowork is handing a colleague a project brief and getting the finished deliverable. Code is a developer working in your repository.

---

### 🔧 Turn by Turn (Chat)

**Reach for this when:**
- The answer changes what you ask next (brainstorming)
- You want your judgment on every turn (drafting, editing)
- It's quick - setting up a whole task would be overhead

**Desktop extras:**
- **Quick entry** - double-tap Option (Mac) to bring Claude up over any app
- **Screenshots and window sharing** - Claude sees what you see (Mac)
- **Dictation** - talk instead of type (Mac)
- **Desktop connectors** - work with local tools and files

**Example:** screenshot an unfamiliar dashboard, ask "what do these metrics mean?", then follow up with "which should I worry about?"

---

### 🚀 Handing Work Off (Cowork)

**Reach for this when:**
- The task has several steps you'd normally do in sequence
- The output is finished files saved where you need them
- The work spans several tools (notes, Slack, spreadsheets)
- It should run on a schedule or while you do something else

**You stay in control:** Claude may ask scoping questions, shows its plan, lets you watch and steer, and (when set to ask) pauses before important actions like sending email.

| Cowork Capability | What It Does |
|-------------------|--------------|
| **Local folder access** | Reads a folder and saves finished work back to it (Chat returns downloads instead) |
| **Scheduled tasks** | Runs on a cadence; remote tasks run even when your computer sleeps |
| **Subagents** | Splits big jobs across parallel workers, returns one deliverable |
| **Projects** | Groups tasks with their own files, instructions, and memory |
| **Browser use** | Claude in Chrome navigates sites and pulls data into the task |
| **Computer use** | Operates your computer directly when no connector exists (research preview, Pro and Max) |
| **Plugins** | Bundles of skills, connectors, and agents for a role (sales, finance, legal) |

Cowork is available on Pro, Max, Team, and Enterprise.

**Example:** "Review what we decided about pricing last quarter across meeting notes, Slack, and email, then update the Q3 deck with the findings."

---

### 🏗️ Building Software (Code Tab)

A full development environment with visual diffs, a built-in terminal, and git history.

| Option | Choices |
|--------|---------|
| **Where it runs** | **Local** (a folder on your computer) or **Cloud** (a GitHub repo; sessions continue after you close the app) |
| **How much Claude does alone** | **Manually approve**, **Accept edits**, or **Plan** first |

Available on Pro, Max, Team, and Enterprise.

| You're about to... | Shape | Where |
|--------------------|-------|-------|
| Ask, brainstorm, draft, think it through | Turn by turn | Chat |
| Hand off a multi-step task, cross-tool or scheduled | Handing off | Cowork |
| Write, test, run, and ship code | Building software | Code tab |

**Interview Tip:**
> "The desktop app has three shapes of work: Chat for turn-by-turn thinking, Cowork for handing off multi-step or scheduled tasks that produce finished files, and the Code tab for building software."

---

## Introduction to Projects

### 🎯 Projects

**Definition:**
> Projects are self-contained workspaces with their own memory, chat history, knowledge base, and custom instructions.

**Simple meaning:**
A dedicated space for one work stream, where Claude always has your reference files and knows how you want it to behave.

**Why it matters:**
- ✅ No re-uploading the same files every chat
- ✅ Instructions apply to every conversation in the project
- ✅ Scales automatically for large knowledge bases (RAG)
- ✅ Team and Enterprise users can share projects

**When to use:**
- Reference materials you'll use repeatedly
- Consistent requirements for how Claude responds
- Team collaboration on a shared foundation

**Real-life analogy:**
A project is like a briefing binder for a consultant - every new task starts with the background docs and house rules already in hand.

---

### 🔧 Creating a Project

**Step 1: Set up**
1. Click **Projects** in the sidebar (or go to claude.ai/projects)
2. Click **+ New Project**
3. Give it a descriptive name, e.g. "Q4 Marketing Campaign"
4. Add a description (for people - Claude doesn't see it)
5. Choose visibility: private or shared with your organization

**Step 2: Add instructions**

**❌ Bad Example:**
```text
Be helpful and write good content.
```

**✅ Good Example:**
```text
This project is for creating marketing content for our B2B software product.
First consider a blog structure that will entice this audience, then write
the draft. Use a professional but conversational tone and avoid jargon.
Always include a call-to-action at the end of marketing copy.
When I upload a meeting transcript, create a structured summary using the
template in "Meeting-Summary-Template.docx".
```

Good instructions include **context**, **process**, **tone and style**, and **specific requirements**. They can also automate workflows.

**Step 3: Build the knowledge base**
Click **+** in the files panel to upload PDF, DOCX, CSV, TXT, HTML, and more, or link Google Drive.

**What to upload:**
- Brand guidelines, style guides, templates
- Research, meeting notes, requirements
- Examples of work to emulate
- Technical docs and specs

**💡 Pro tip:** Name files descriptively - "Q4-2024-Brand-Guidelines.pdf", not "document1.pdf". Claude uses file names to find the right information.

---

### 🔍 How Projects Handle Large Knowledge Bases

When project knowledge approaches the context limit, Claude switches to **Retrieval Augmented Generation (RAG)**: it searches your files and pulls in only what's relevant. This expands capacity by **up to 10x** while keeping quality. A visual indicator shows when RAG is on.

---

### 🔐 Sharing and Permissions (Team and Enterprise)

| Permission | Can Do |
|------------|--------|
| **Can view** | See contents, use knowledge, chat - no changes |
| **Can edit** | Change instructions and knowledge, manage members |
| **Owner** | Everything, including who can see the project |

**To share:** open the project → **Share project** → add people by name or email (or paste a list), or share with "Everyone at [your organization]".

---

### 💡 Example Projects and Best Practices

| Project | Knowledge to Upload |
|---------|---------------------|
| **Q4 product launch** | Specs, competitive analysis, messaging notes |
| **Research support** | Competitive review, user research, customer feedback |
| **Client account hub** | Brand guidelines, past deliverables, communication history |
| **Event planning** | Venue contracts, speaker bios, attendee data |
| **Job description generator** | Past JDs, team charters, headcount docs |

**Best practices:**
- ✅ Start focused, then expand
- ✅ Keep knowledge current - outdated docs mean outdated answers
- ✅ Write clear, specific instructions
- ✅ Name and group files descriptively
- ✅ Reference documents by name: "Based on our Q3 report, ..."

**Interview Tip:**
> "Projects are self-contained workspaces with a knowledge base and instructions shared by every chat, they switch to RAG for large knowledge bases, and teams can share them with view or edit permissions."

---

## Creating with Artifacts

### 🎯 Artifacts

**Definition:**
> Artifacts are the outputs you create with Claude - documents, decks, designs, dashboards, prototypes - shown in a dedicated window next to the conversation.

**Simple meaning:**
Instead of a long block of text buried in chat, you see the real thing take shape, ready to edit, reuse, and share.

**Why it matters:**
- ✅ Outputs stand on their own, separate from the chat
- ✅ On paid plans, everything is saved in the **Artifacts tab** to revisit and keep editing
- ✅ Edit directly, comment, or ask Claude to change it
- ✅ Share with controlled permissions or export to files

**Real-life analogy:**
The conversation is the workshop; the Artifacts tab is the shelf where finished pieces live.

**💡 Tip:** To make sure you get an artifact, say "Create this as an artifact."

---

### 🧩 Designs, Decks, and Living Documents

| Experience | Creates | Highlights | Exports |
|------------|---------|------------|---------|
| **Claude Design** | Landing pages, one-pagers, mockups, prototypes | Uses your design system; drag, resize, align on a canvas | .pptx, .pdf, .html |
| **Claude Slides** | Presentations | Outlines and lays out every slide; present inside Claude | .pptx, .pdf |
| **Claude Docs** | Living rich-text documents | Real-time co-editing; Claude explains choices in comments; charts from connected tools (snapshots - ask to refresh) | Google Docs, .docx |

You can convert between them: "turn this doc into a deck".

**Availability:** beta on paid plans. On by default for Pro, Max, and Team; off by default on Enterprise until an admin enables it in **Organization settings > Artifacts**.

---

### ⚖️ Artifacts vs File Creation

| Feature | Artifacts | File Creation |
|---------|-----------|---------------|
| **Output** | Opens and updates inside Claude | Downloadable Word, Excel, PowerPoint, PDF |
| **Sharing** | By link | Send the file |
| **Keeps editing with Claude** | ✅ | ❌ New file each time |
| **Plans** | Dashboards, trackers, flowcharts, code on every plan (incl. Free) | All plans with Skills enabled |

---

### 🔧 Creating and Editing

**Example requests:**
```text
Turn these meeting notes into a five-slide deck for my team meeting
Draft a one-page project brief for the onboarding revamp as a doc I can share with the team
Design a landing page for a productivity app with a hero section and feature list
Build an interactive dashboard that lets me input monthly expenses and see a breakdown
```

Claude uses the context it already has - files, conversation, project knowledge, connected tools.

**Three ways to change an artifact (mix freely):**
1. **Edit directly** - type in a doc, edit a slide, drag on the canvas
2. **Comment for Claude** - on the exact element; in docs, @-mention Claude for an explanation
3. **Just ask** - keep talking in the conversation

Editing, commenting, and sharing happen on desktop or web; on mobile you can create artifacts and view them full screen.

---

### 🔐 Sharing

Artifacts are private until shared. For designs, decks, and docs, give each person **view**, **comment**, or **edit** access (docs: view and edit). Viewers need a Claude account.

| Plan | Sharing Options |
|------|-----------------|
| **Pro / Max** | Private or anyone with the link; can publish designs and decks publicly (conversation stays private) |
| **Team / Enterprise** | Inside the organization by default; external links only after an Owner enables External sharing |
| **Free** | Copy, download, or publish a view-only link |

**Tips:**
- ✅ Ask for the deliverable, not just the content: "turn our Q3 results into a one-page doc for leadership"
- ✅ Be specific: "a monthly budget tracker with categories, a pie chart, and an over-budget warning"
- ✅ Describe the end user ("for new employees" vs "for engineers")
- ✅ Build on work you've already done - the best artifacts come at the end of a conversation
- ✅ Ask Claude to refresh charts when you need current data

**Interview Tip:**
> "Artifacts are standalone outputs - designs, decks, docs, dashboards - that live in the Artifacts tab, can be edited directly, by comment, or by asking Claude, and are shared by link with view, comment, or edit permissions."

---

## Working with Skills

### 🎯 Skills

**Definition:**
> Skills are folders of instructions, scripts, and resources that Claude loads dynamically to perform specialized tasks in a repeatable way.

**Simple meaning:**
Expertise packages that teach Claude how to do a specific task the same way every time.

**Why it matters:**
- ✅ Power Claude's Excel, Word, PowerPoint, and PDF creation
- ✅ Codify whole workflows - variance analysis, brand voice review, compliance checklists
- ✅ Claude picks the right skill automatically
- ✅ Easy to create by chatting with Claude

**Real-life analogy:**
Skills are like recipe cards - the chef doesn't memorize every dish, but pulls the right card when that order comes in.

---

### 🧩 Types of Skills

| Type | Who Makes It | Example |
|------|--------------|---------|
| **Anthropic Skills** | Anthropic | Excel, Word, PowerPoint, PDF creation |
| **Custom Skills** | You or your organization | Apply brand guidelines to decks, format meeting notes, run data analysis workflows |

---

### 🔧 Enabling Skills

Skills are on all plans and need **Code execution and file creation** (Claude's secure sandbox).

1. Go to **Settings > Capabilities**
2. Turn on **Code execution and file creation**
3. Scroll to **Skills**
4. Toggle individual skills on or off

- **Enterprise:** Owners must first enable Code execution and Skills in Admin settings
- **Team:** enabled by default at the organization level

**Prompts that trigger skills:**
```text
Create an Excel spreadsheet tracking monthly expenses with formulas for totals
Turn this meeting notes document into a PowerPoint presentation
Generate a PDF report summarizing this data
Build a financial model in Excel with scenario analysis
```

You'll see the skill mentioned in Claude's chain of thought, and the result is a downloadable file (or saved to Google Drive).

**Working with your files:** upload .xlsx, .pptx, .docx, or .pdf files and Claude creates updated versions (it doesn't edit the original in place). Turn on **Allow limited network access** when prompted.

---

### 🔐 Security Considerations

- ⚠️ Skills can include executable code - only install custom skills from trusted sources
- ✅ Anthropic's built-in skills are tested and maintained by Anthropic
- ✅ Custom skills you upload are private to your account
- ⚠️ Review the contents of any external skill before using it

---

### 🚀 Creating a Custom Skill

1. **Start a new chat** - "I want to create a skill for writing quarterly business reviews"
2. **Answer Claude's questions** - what it should do, what good output looks like, when you'd use it
3. **Upload reference materials** - templates, style guides, examples
4. **Save the skill** - Claude generates a properly structured skill file

Find all your skills in the **Customize** tab. Claude invokes custom skills automatically, and you can ask Claude to edit them over time.

---

### ⚖️ Skills vs Projects

> "Projects store knowledge, skills perform tasks."

| Feature | Projects | Skills |
|---------|----------|--------|
| **Purpose** | Store knowledge Claude references | Define processes Claude executes |
| **Best for** | Long-term context, reference material, team collaboration | Repeatable workflows, multi-step tasks, consistent method |
| **Example** | Customer hub, research buddy | Brand or legal guidelines, blog drafting, PDF creation |
| **Persistence** | Available in every chat in the project | Applied when the skill is invoked |

They work together: a "customer call prep" skill (the *how*) can pull from customer profiles in a project (the *what*).

**Interview Tip:**
> "Skills are packaged instructions and scripts Claude loads automatically to run a task the same way every time; Anthropic provides document skills, you can build custom ones by chatting with Claude, and projects hold knowledge while skills hold process."

---

## Connecting Your Tools

### 🎯 Connectors

**Definition:**
> Connectors give Claude access to the tools, data, and context you use every day, so it can read information and take actions on your behalf. They are powered by the Model Context Protocol (MCP).

**Simple meaning:**
Instead of copy-pasting from Slack, Drive, or Asana, Claude looks there itself.

**Why it matters:**
- ✅ Claude works with your actual information, not a blank slate
- ✅ Can search, read, analyze, create, and update across apps
- ✅ One standard (MCP) means connectors can be built for any tool
- ✅ Claude only sees what you can see

**Real-life analogy:**
MCP is like USB-C for AI - one universal port that lets Claude plug into many different apps.

---

### 🧩 Types of Connectors

| Type | Runs | Examples |
|------|------|----------|
| **Web connectors** | Cloud | Gmail, Google Drive, Notion, Slack, Asana, Linear, Stripe |
| **Desktop extensions** | Locally via the Claude Desktop app | Local files, browser control, native apps like Figma |

Browse the directory at **claude.ai/directory** or click **+ > Connectors** in a chat. One entry can cover several apps - e.g. **Atlassian Rovo** covers both Jira and Confluence. If a tool isn't listed, add it as a **custom connector**.

---

### 🔧 Setting Up

**Web connector:**
1. Find it at claude.ai/directory or **+ > Connectors**
2. Click **Connect**
3. Sign in to the service
4. Review and grant permissions
5. Test: "Can you access my [tool name]?"

**Desktop extension:**
1. Install the Claude Desktop app
2. Go to **Settings > Extensions**
3. Click **Install** on an extension
4. Follow any extra setup steps

---

### 🚀 Using Connectors

| Category | Example Prompt |
|----------|----------------|
| **Project management** (Asana, Linear, Jira) | "What are my highest priority tasks due this week?" |
| **Communication** (Slack, Gmail) | "Find the email thread where we discussed the vendor contract" |
| **Documentation** (Notion, Drive, Confluence) | "What does our style guide say about using contractions?" |
| **Business tools** (Stripe, PayPal, HubSpot) | "List recent transactions over $1,000" |

---

### 🔐 Security and Permissions

- ✅ **Scoped access** - toggle individual permissions per connector
- ✅ **Claude sees what you see** - connecting your email doesn't expose your CEO's inbox
- ✅ **Revocable** - disconnect in Claude's settings or the service's security settings
- ⚠️ Only install connectors (including custom ones) from trusted sources

**Interview Tip:**
> "Connectors, built on the Model Context Protocol, let Claude read and act in your tools - web connectors for cloud apps, desktop extensions for local ones - with scoped, revocable access limited to what you can already see."

---

## Enterprise Search

### 🎯 Enterprise Search

**Definition:**
> Enterprise Search adds an "Ask {Your Org Name}" project to the sidebar that searches across your organization's connected tools and synthesizes a cited answer.

**Simple meaning:**
A pre-built project for your whole company - the knowledge base is already connected, so you just ask.

**Why it matters:**
- ✅ One question across SharePoint, Slack, Gmail, Drive, and more
- ✅ Always cites sources
- ✅ Tuned for information gathering with Anthropic-configured instructions
- ✅ Respects existing permissions

**Availability:** Team and Enterprise plans; must be set up by an admin.

**Real-life analogy:**
It's like asking a long-tenured colleague who has read every channel and document - and who tells you exactly where they found the answer.

---

### 🔍 What You Can Ask

| Use Case | Example |
|----------|---------|
| **Getting up to speed** | "What happened yesterday while I was out?" |
| **Policy and process** | "How do I submit an expense report?" |
| **Research and analysis** | "What are the main reasons customers cite for choosing competitors?" |
| **Onboarding** | "Who should I talk to about learning the billing system?" |
| **Project tracking** | "What were the key decisions from last week's leadership meetings?" |

---

### 🔧 Setup

**Admins (Owners):**
1. Click **Ask Your Org** in the sidebar
2. Click **Set up for your org** (or **Disable**)
3. Connect a **Documents** source (Drive or SharePoint) and a **Chat** source (Slack or Teams); email is optional but recommended
4. Use **+ Add more** for other tools
5. Set the project name (shows as "Ask [Name]")
6. Add a description and click **Finish set up**

**Users:**
1. Open the "Ask {Org Name}" project in the sidebar
2. Follow the onboarding flow
3. Authenticate with each service
4. Start asking

More connectors = more complete answers. Add more via **Connect** in the project's Instructions section.

**🔐 Is it safe?**
Yes. It only shows what you already have permission to see, conversations stay private, and connected data isn't indexed or stored separately.

**Interview Tip:**
> "Enterprise Search is an org-wide project that searches connected documents, chat, and email to give cited answers, set up once by an admin and limited to each user's existing permissions."

---

## Research for Deep Dives

### 🎯 Research

**Definition:**
> Research is an agentic, multi-step mode where Claude plans its approach, runs many searches that build on each other across the web and your connected tools, and delivers a cited report.

**Simple meaning:**
Instead of one quick search, Claude acts like a research assistant who investigates from several angles and writes it up.

**Why it matters:**
- ✅ Covers hundreds of sources in one answer
- ✅ Uses Thinking to plan before searching
- ✅ Every claim has a citation you can check
- ✅ Replaces hours of manual research

**Real-life analogy:**
Web search is asking a librarian for one book. Research is hiring an assistant to read the shelf and hand you a summary with footnotes.

---

### 🔧 How Research Works

1. **Plans its approach** - breaks the request into pieces
2. **Runs multiple searches** - each builds on what it found
3. **Synthesizes findings** - from the web and connected tools (Gmail, Calendar, Drive)
4. **Cites sources** - every claim links back

It takes a few minutes or more, depending on the question.

**To use it:**
1. Click **+** at the bottom left of the chat
2. Select **Research**
3. Enter your prompt
4. Watch the progress indicators

⚠️ **Web search must be enabled** for Research to work.

---

### ⚖️ Research vs Other Features

| Feature | Use When |
|---------|----------|
| **Research** | Multi-source reports, comparisons, hours of manual work, verified citations |
| **Web search** | A quick fact, one or two sources, speed matters most |
| **Thinking** | Deep reasoning (math, debugging, logic) with no outside info needed |
| **Enterprise Search** | Company-specific questions from internal docs, Slack, email |

---

### 💡 Writing Research Prompts

**❌ Bad Example:**
```text
Tell me about the EV market.
```

**✅ Good Example:**
```text
Analyze the electric vehicle battery market - identify key players,
technology trends, and supply chain challenges that might affect
investment decisions.
```

**Tips:**
- ✅ Be specific about your goals
- ✅ Specify the sections you want (e.g. location, amenities, catering, pricing)
- ✅ Include constraints - budget, timeline, geography
- ✅ Ask Claude to help write the Research prompt first

**With connected tools:**
```text
Review my calendar commitments for next week and research each company I'm meeting with
```
Steer it with phrases like "Pull relevant context from my Google Drive".

**Interview Tip:**
> "Research plans with Thinking, runs many searches across the web and connected tools, and returns a cited report in minutes - use it for deep, multi-source questions, and web search for quick facts."

---

## Claude in Action: Use Cases by Role

### 🎯 Use Cases by Role

**Simple meaning:**
The same features apply to every job; the value comes from how each role combines them.

| Role | Example Use Cases |
|------|-------------------|
| **General** | Project status reports, patterns in user feedback, brand guidelines as a skill |
| **Sales** | Battle card library, deal preparation, sales reports |
| **Marketing** | Campaign performance analysis, adapting content across platforms |
| **Finance** | Financial models, investment memos, understanding inherited spreadsheets |
| **HR** | New hire onboarding guides |
| **Legal** | Discovery timelines and pattern analysis |
| **Research** | Literature review plans, verifying statistics from raw data |

**Real-life analogy:**
Claude's features are like a toolbox - a carpenter and an electrician use the same hammer and screwdriver in different ways.

More examples are in the [Use Case Gallery](https://academy.claude.com/all?kind=use-case).

**Interview Tip:**
> "Every role uses the same core features - prompts, projects, skills, connectors, research - but combines them around its own work, like battle cards in sales or financial models in finance."

---

## Other Ways to Work with Claude

### 🎯 Claude Beyond Claude.ai

**Simple meaning:**
Claude is the intelligence; Claude.ai is just one place to use it. Specialized tools bring it to where you already work.

**Real-life analogy:**
Claude is like a consultant who can join you anywhere - the meeting room (Claude.ai), the workbench (Claude Code), the team channel (Slack), or the document you have open (Microsoft 365).

---

### 🔧 The Tools and When to Use Them

**Claude Code** - agentic coding in your terminal, IDE, browser, or Slack
- Build features from plain English; Claude writes code, runs tests, commits
- Debug by pasting errors
- Learn an unfamiliar codebase
- Automate lint fixes, merge conflicts, release notes

**Claude Tag** - Claude inside Slack
- Draft replies, summarize long threads
- Prep for meetings from workspace conversations and files
- Onboard by reviewing channel history
- Tag Claude on a bug report to start a Claude Code session

**Claude Design** - ideas, sketches, or screenshots to interactive prototypes
- Brief to working UI without code
- Compare several design variations
- Use your team's design system so the hand-off matches what engineering builds
- Beta on paid plans; also at claude.ai/design

**Claude for Microsoft 365** - sidebars in Office apps

| App | Use It To |
|-----|-----------|
| **Excel** | Understand formulas across sheets, update assumptions, debug #REF!/#VALUE!/circular references, build pivot tables and charts |
| **PowerPoint** | Draft decks from notes, tighten copy, restructure, apply consistent formatting in your template |
| **Word** | Draft in your template, revise sections, work through tracked changes and comments, ground claims in connected sources |
| **Outlook** (beta) | Triage mail, draft replies with thread and calendar context, summarize long chains |

**Claude in Chrome** - browser sidebar that can act on pages
- Summarize articles and pages
- Manage email, fill repetitive forms
- Test site features and multi-step flows
- Pull context from internal tools, CRMs, dashboards
- ⚠️ On by default for Pro, Max, and Team; admin-enabled on Enterprise; not on Free. Use for low-risk tasks on trusted sites - it asks before high-risk actions, and some site categories are blocked

---

### 📊 Summary

| Tool | Best For | Where It Runs |
|------|----------|---------------|
| **Claude.ai** | General tasks, research, writing, analysis, file creation | Web, desktop, mobile |
| **Claude Code** | Software development, codebase navigation, git | Terminal, IDE, browser |
| **Claude Cowork** | Multi-step tasks: briefs, documents, file organization, analysis | Desktop (web and mobile in beta) |
| **Claude Tag** | Team collaboration, meeting prep, quick answers | Slack |
| **Claude Design** | UI prototypes, design exploration | Conversations (paid), claude.ai/design |
| **Claude for Microsoft 365** | Editing in place across documents | Excel, PowerPoint, Word, Outlook |
| **Claude in Chrome** | Web research, email, browser automation | Chrome sidebar |

**Interview Tip:**
> "Beyond Claude.ai, there's Claude Code for development, Cowork for hand-off tasks, Claude Tag in Slack, Claude Design for prototypes, Microsoft 365 sidebars for Office work, and Claude in Chrome for browser tasks."

---

## Choosing the Right Feature

### ⚖️ Feature Decision Guide

| Scenario | Use | Avoid |
|----------|-----|-------|
| Quick question or rewrite | **Chat** | Setting up a project |
| Ongoing work with the same files | **Project** | Re-uploading every chat |
| A deliverable to edit and share | **Artifact** | A long reply buried in chat |
| A downloadable Office file | **File creation (Skills)** | Copying text into Word by hand |
| Same procedure every time | **Custom skill** | Re-typing instructions |
| Data lives in Slack, Drive, Asana | **Connector** | Copy-pasting |
| Company knowledge question | **Enterprise Search** | Searching each tool by hand |
| Deep, multi-source investigation | **Research** | A single web search |
| Multi-step, scheduled, or file-saving task | **Cowork** | Feeding it to Chat one question at a time |
| Working in a codebase | **Claude Code** | Pasting code into chat |

**Remember:**
> "Projects store knowledge, skills perform tasks, connectors bring in your tools, and artifacts hold what you make."

---

## Common Interview Questions

### Basic Questions

**1. What is Claude?**
> "An AI assistant from Anthropic, trained with Constitutional AI to be safe and steerable, that works as a thinking partner for writing, research, coding, and reasoning."

**2. What are the three elements of a good prompt?**
> "Setting the stage (role, objective, context), defining the task (what Claude should do), and specifying rules (style, tone, format, examples)."

**3. What is a project?**
> "A self-contained workspace with its own knowledge base, instructions, chat history, and memory that every chat in it shares."

**4. What is an artifact?**
> "A standalone output - document, deck, design, dashboard, or prototype - shown next to the chat and saved in the Artifacts tab to edit and share."

**5. What is the context window?**
> "How much Claude can consider at once: 200K+ tokens (about 500 pages), and up to 1M tokens on paid plans with supported models."

### Intermediate Questions

**1. What's the difference between projects and skills?**
> "Projects store knowledge Claude references; skills define processes Claude executes - the project is the what, the skill is the how."

**2. What is the 4D Framework?**
> "A model of AI Fluency with four competencies: Delegation, Description, Discernment, and Diligence."

**3. How do projects handle large knowledge bases?**
> "Near the context limit, they switch to retrieval augmented generation, searching files and pulling in only what's relevant, which expands capacity up to 10x."

**4. When would you use Research instead of web search or Thinking?**
> "Research for multi-source, cited reports; web search for quick facts; Thinking for deep reasoning that doesn't need outside information."

**5. What's the difference between Chat and Cowork?**
> "Chat is turn-by-turn thinking; Cowork is handing off a multi-step task that can span tools, run on a schedule, and save finished files to a folder."

### Advanced Questions

**1. How do connectors keep data secure?**
> "Access is scoped and revocable, Claude can only see what the user can see, and you should only install connectors from trusted sources."

**2. How would you check whether Claude is good at a recurring task?**
> "Run a simple eval: gather 5-10 real examples, write matching prompts, compare Claude's output with yours, and refine the prompts or mark where human review is needed."

**3. Artifacts vs file creation - when do you use each?**
> "Artifacts when you want to keep editing in Claude and share by link; file creation when you need a Word, Excel, PowerPoint, or PDF file to download and use elsewhere."

**4. How would you set up Claude for a marketing team?**
> "A shared project with brand guidelines and instructions, a custom brand-voice skill, connectors to Drive and Slack, Research for competitor analysis, and Slides for decks."

**5. How do you handle confident but wrong answers?**
> "Verify key facts, ask Claude to cite sources or state its confidence, turn on web search, and use Research when citations matter."

---

## 🎓 Summary

**Core ideas:**
1. **Claude** is a thinking partner - you bring context, it brings intelligence
2. **Prompts** = set the stage + define the task + specify rules, then iterate
3. **Desktop** work comes in three shapes: Chat, Cowork, Code
4. **Projects** hold knowledge; **skills** hold process; **artifacts** hold outputs
5. **Connectors (MCP)** bring your tools in; **Enterprise Search** covers company knowledge
6. **Research** runs deep, cited investigations
7. **Other surfaces** - Claude Code, Tag, Design, Microsoft 365, Chrome - meet you where you work

**Remember:**
> "Claude brings the intelligence, you bring the context - the more context it has, the better the work."

---

## 🔗 Further Reading

- [Creating and managing projects](https://support.claude.com/en/articles/9519177-how-can-i-create-and-manage-projects)
- [What are skills?](https://support.claude.com/en/articles/12512176-what-are-skills)
- [Pre-built web connectors using remote MCP](https://support.claude.com/en/articles/11176164-pre-built-web-connectors-using-remote-mcp)
- [Using Enterprise Search](https://support.claude.com/en/articles/12489464-using-enterprise-search)
- [Using Research](https://support.claude.com/en/articles/11088861-using-research-on-claude-ai)
- [AI Fluency course](https://academy.claude.com/courses/ai-fluency-framework-foundations)

---

**Source:** [Claude 101 - Anthropic Academy](https://anthropic.skilljar.com/claude-101)
**Last Updated:** October 2026
