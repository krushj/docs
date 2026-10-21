# AI Evals Complete Guide

> My notes from **AI Evals For Engineers & PMs**, taught by Shreya Shankar and Hamel Husain on Maven (October 2025 cohort). They cover all 8 lessons over 4 weeks. The course uses two running examples. The **Recipe Bot** is the homework project: an assistant that suggests recipes. **NurtureBoss** is a real leasing-agent chatbot for apartment communities. Homework code lives in [ai-evals-course/recipe-chatbot](https://github.com/ai-evals-course/recipe-chatbot).

## Table of Contents

### Course Overview
- [Course Map](#course-map)

### Week 1: Fundamentals and Error Analysis
- [What is LLM Evaluation?](#what-is-llm-evaluation)
- [The Three Gulfs](#the-three-gulfs)
- [The Analyze-Measure-Improve Lifecycle](#the-analyze-measure-improve-lifecycle)
- [Prompting Fundamentals](#prompting-fundamentals)
- [Defining Good: Specifications and Agency](#defining-good-specifications-and-agency)
- [Error Analysis](#error-analysis)
- [Synthetic Data with Dimensions](#synthetic-data-with-dimensions)
- [Traces and Open Coding](#traces-and-open-coding)
- [Axial Coding and Theoretical Saturation](#axial-coding-and-theoretical-saturation)
- [Multi-Turn Evaluation](#multi-turn-evaluation)
- [Collaborative Evaluation](#collaborative-evaluation)
- [Inter-Annotator Agreement](#inter-annotator-agreement)

### Week 2: Automated Evaluators
- [Specification vs Generalization Failures](#specification-vs-generalization-failures)
- [Code-Based Evaluators](#code-based-evaluators)
- [LLM-as-Judge](#llm-as-judge)
- [Aligning the Judge: Train, Dev, Test](#aligning-the-judge-train-dev-test)
- [Correcting Judge Bias](#correcting-judge-bias)
- [Confidence Intervals with Bootstrap](#confidence-intervals-with-bootstrap)
- [Automated Evaluation Pitfalls](#automated-evaluation-pitfalls)

### Week 3: Complex Architectures and CI/CD
- [Evaluating RAG](#evaluating-rag)
- [Synthetic Retrieval Datasets](#synthetic-retrieval-datasets)
- [Retrieval Metrics](#retrieval-metrics)
- [Generation Quality in RAG](#generation-quality-in-rag)
- [Tool Calling and Agents](#tool-calling-and-agents)
- [Other Input Modalities](#other-input-modalities)
- [Continuous Integration](#continuous-integration)
- [Continuous Deployment and Monitoring](#continuous-deployment-and-monitoring)

### Week 4: Human Review and Improvement
- [Custom Review Interfaces](#custom-review-interfaces)
- [Sampling Traces](#sampling-traces)
- [Case Studies: EvalGen and DocWrangler](#case-studies-evalgen-and-docwrangler)
- [Improving Accuracy](#improving-accuracy)
- [Reducing Cost](#reducing-cost)
- [Model Cascades](#model-cascades)

### Interview Preparation
- [Common Interview Questions](#common-interview-questions)

---

## Course Map

### 🎯 How the Course Is Organized

**Definition/Purpose:**
> The course teaches **application-centric** LLM evaluation: measuring how *your* pipeline fails on *your* data, rather than chasing generic benchmarks.

**Simple meaning:**
Learn to find out what's broken in your AI product, put a number on it, and fix it.

**Course objective:** master error analysis, automated evaluators, and evaluating complex pipelines.

| Week | Lessons | Topics | Homework |
|------|---------|--------|----------|
| **1** | 1, 2, 3 | Three Gulfs, lifecycle, prompting, error analysis, collaborative evaluation | HW1: Recipe Bot prompt · HW2: error analysis |
| **2** | 4, 5 | Code-based evals, LLM-as-Judge, judge alignment, bias correction | HW3: build and validate an LLM judge |
| **3** | 6 | RAG, tool calling, agents, modalities, CI/CD, monitoring | HW4: RAG retrieval eval · HW5: agent failure analysis |
| **4** | 7, 8 | Review interfaces, sampling, accuracy improvement, cost reduction, model cascades | Optional: vibe-code an annotation app |

**Real-life analogy:**
The course is like learning to run a restaurant kitchen properly. First you taste every dish (analyze), then you set up checklists and thermometers (measure), and only then do you change recipes (improve).

---

## What is LLM Evaluation?

### 🎯 LLM Evaluation

**Definition:**
> Evaluation is the systematic measurement of quality in an LLM pipeline. It can be quantitative (scores) or qualitative (structured summaries and reports).

**Simple meaning:**
A repeatable way to know whether your AI is doing a good job, and where it isn't.

**Why it matters:**
- ✅ Builds user trust: the Recipe Bot must suggest recipes that are safe, edible, and relevant
- ✅ Monitors quality over time: you notice when suggestions get worse
- ✅ Enables systematic improvement instead of random prompt tweaks
- ✅ Without it, you're guessing

**Life without evals:**
- ❌ No idea what is bad
- ❌ No idea *why* it's bad
- ❌ Every fix is whack-a-mole: patch one bug, another one pops up

**Real-life analogy:**
Shipping an LLM without evals is like a restaurant that never tastes its food. You only learn something is wrong when customers stop coming back.

**Interview Tip:**
> "LLM evaluation is the systematic measurement of pipeline quality on your own application's data, so you can find failures, track them over time, and improve with evidence instead of guesswork."

---

## The Three Gulfs

### 🎯 The Three Gulfs Model

**Definition:**
> The Three Gulfs model names the three gaps a developer must bridge to build a reliable LLM pipeline: **Comprehension**, **Specification**, and **Generalization**.

**Simple meaning:**
Building with LLMs is hard because you need to understand your data, describe exactly what you want, and make it work on inputs you've never seen. Each one needs a different mindset.

| Gulf | Question | Pitfall | Recipe Bot Example |
|------|----------|---------|--------------------|
| **Comprehension** | Do I understand my data and how the LLM behaves on it? | You can't read every trace, so you miss failure patterns | Missing that the bot often suggests overly complex recipes for simple queries |
| **Specification** | Did I translate my intent into precise instructions? | Vague words like "easy" make behavior unreliable | "Easy" could mean quick, common ingredients, or few steps |
| **Generalization** | Does it work on new, unusual inputs? | Works on common tests, fails on rare cases | Handles "vegan" fine, fails on "low-FODMAP" or "kosher" |

**🔍 The illusion of generalization:**
Testing "vegan" a few times and seeing good results doesn't mean the model understands *dietary restrictions*. It may have learned one pattern, not the principle. This gulf is the most dangerous because the product *looks* like it works.

**Why it matters:**
- ✅ Tells you which kind of problem you're facing
- ✅ Each gulf needs a different fix: look at data, rewrite the prompt, or change the architecture
- ✅ Switching between these "hats" feels slow, and that's normal

**Real-life analogy:**
Hiring a new cook. **Comprehension**: do you know what your customers actually order? **Specification**: did you write the recipe card clearly? **Generalization**: can the cook handle a dish that isn't on the card?

**Interview Tip:**
> "The Three Gulfs are Comprehension (understanding your data), Specification (turning intent into precise prompts), and Generalization (working on unseen inputs). Error analysis closes the first, and prompt and architecture changes close the other two."

---

## The Analyze-Measure-Improve Lifecycle

### 🎯 The Evaluation Lifecycle

**Definition:**
> After you build an initial pipeline, evaluation is a continuous cycle. **Analyze** failures qualitatively, **Measure** them quantitatively, and **Improve** the pipeline based on what you measured.

**Simple meaning:**
Look at what's broken, count how often it breaks, fix it, repeat.

| Phase | What You Do | Gulf Addressed | Common Pitfalls |
|-------|-------------|----------------|-----------------|
| **Analyze** | Collect representative examples, find and categorize failure modes | Comprehension | ❌ Outsourcing annotation · ❌ Not looking at enough examples |
| **Measure** | Turn failure modes into metrics, build evaluators | Bridges to the other two | ❌ Unaligned LLM judges · ❌ Testing judges on their own few-shot examples |
| **Improve** | Refine prompts, models, and architecture | Specification, Generalization | ❌ Premature improvement · ❌ Jumping to fine-tuning first |

```
Initial Pipeline
      │
      ▼
 ┌─────────┐     ┌─────────┐     ┌─────────┐
 │ ANALYZE │ ──► │ MEASURE │ ──► │ IMPROVE │
 └─────────┘     └─────────┘     └─────────┘
      ▲                               │
      └───────────────────────────────┘
```

**Why it matters:**
- ✅ Gives a repeatable process instead of "prompt-and-pray"
- ✅ Stops you from fixing things you haven't measured
- ✅ Each loop makes the next one faster

**Real-life analogy:**
Like a doctor: diagnose (analyze), run tests to confirm (measure), then prescribe (improve). A doctor who prescribes before diagnosing is guessing.

**Interview Tip:**
> "I follow Analyze-Measure-Improve: error analysis to find failure modes, automated evaluators to quantify them, then targeted fixes. Improving before analyzing is the most common mistake."

---

## Prompting Fundamentals

### 🎯 Components of a Good Prompt

**Definition:**
> A prompt is the full specification you give the LLM. A strong prompt combines role, rules, context, examples, reasoning guidance, and output format.

**Simple meaning:**
Before you can evaluate anything, you need a clear first version of what you're building.

**LLM strengths vs weaknesses:**

| Strengths | Weaknesses |
|-----------|------------|
| ✅ Fluent, coherent, grammatical text | ❌ Nondeterminism: same prompt, different outputs |
| ✅ Summarization, translation, Q&A with context | ❌ Small prompt changes can change output a lot |
| ✅ Few-shot learning from a handful of examples | ❌ Hallucination: predicts likely text, not verified truth |

**The 7 components:**
1. **Role and objective:** "You are a helpful and creative recipe assistant..."
2. **Instructions and response rules:** what to do and what not to do
3. **Context:** available ingredients, dietary restrictions, skill level
4. **Examples (few-shot):** input-output pairs showing format and style
5. **Reasoning steps (CoT):** "think step by step" for complex requests
6. **Output format:** "Respond in JSON with keys recipe_name, ingredients, steps"
7. **Delimiters:** `###`, triple backticks, or XML tags to separate sections

---

**❌ Bad Example:**
```python
# Vague: no role, no rules, no format, no context.
# What is "dinner tonight"? How many servings? Any allergies?
SYSTEM_PROMPT = "Suggest a recipe for {user_query}."
```

**✅ Good Example:**
```python
# Role, rules, context handling, agency, and format are all explicit.
SYSTEM_PROMPT = """
You are a friendly, practical recipe assistant for home cooks.

### Rules
- Always list ingredients with quantities before the steps.
- Never suggest an ingredient the user says they are allergic to.
- Do not suggest rare ingredients unless the user asks for them.
- "Quick" means 30 minutes or less, total time.
- If the request conflicts with itself (e.g. "quick roast"), say so
  and offer the closest quick alternative.

### Output format (Markdown)
## <Recipe name>
**Time:** <minutes> | **Serves:** <n>
### Ingredients
- <qty> <ingredient>
### Steps
1. <step>
"""
```

**Benefits:**
- ✅ Each rule can be checked later ("Does the output have an Ingredients section?")
- ✅ Defines ambiguous words ("quick") instead of leaving them to the model
- ✅ A consistent format makes automated evaluation possible

**Interview Tip:**
> "A good prompt has a role, explicit do/don't rules, context, few-shot examples, reasoning guidance and an output format. Write each rule so you can test it."

---

## Defining Good: Specifications and Agency

### 🎯 Start with User Unhappiness

**Definition:**
> Define "good" by first listing what would make a user unhappy. Those are your candidate failure modes.

**Simple meaning:**
It's easier to say what's wrong than what's perfect, so start there.

**Recipe Bot unhappy paths:**
- Ingredients that aren't commonly available
- Ignores stated dietary restrictions (allergies!)
- Unclear instructions
- Too complex or too simple for the user's skill level
- Unhealthy suggestion when "healthy" was requested

### 🎯 Specifications

**Definition:**
> Specifications are the hard rules of behavior: what the bot must **always** do (positive specs) and must **never** do (negative specs).

**The key habit:** for every rule, ask *"How would I check this?"*

| Rule | Type | How to Check |
|------|------|--------------|
| Always list ingredients with quantities | Positive | Does the output have an Ingredients section? |
| Never include a stated allergen | Negative | Is the forbidden ingredient in the recipe? |
| Never invent unsafe cooking methods | Negative | Needs a human or LLM judge |

### 🎯 Agency

**Definition:**
> Agency is how much freedom the bot has to deviate from the literal request when it sees a conflict.

**Scenario:** "I want a quick dinner using chicken and potatoes." Roasting takes about an hour.

| Agency | Bot Behavior | Trade-off |
|--------|--------------|-----------|
| **High** | Suggests a different, quick chicken recipe | ✅ Helpful · ❌ May override what the user wanted |
| **Medium** | "Roasting takes ~1 hour. OK, or prefer faster?" | ✅ Respects user · ❌ Extra turn |
| **Low** | Gives the roasting recipe and ignores "quick" | ✅ Predictable · ❌ Fails the real need |

### 🎯 Eliciting Ground Truth

For subjective qualities ("is it creative?", "is it helpful?") there are two ways to think about what "good" looks like:
- **Direct grading:** "Rate 1-5." Writing down what a 5-star answer has gives you prompt rules (relevant to my ingredients, matches my skill, clear steps).
- **Pairwise comparison:** "Which of these two recipes is better?" The reasons you give ("fewer unusual spices", "shorter cook time") become rules.

**Real-life analogy:**
Specifications are a job description. Agency is how much the employee may improvise. "Always greet the customer" is a spec; "may offer a discount if the order is late" is agency.

**Interview Tip:**
> "I define specs as testable always/never rules, decide explicitly how much agency the model has when instructions conflict, and for every rule I write down how I would check it."

---

## Error Analysis

### 🎯 Error Analysis Overview

**Definition:**
> Error analysis is the **Analyze** phase: systematically reading pipeline outputs to discover *how* and *why* the system fails, before counting anything.

**Simple meaning:**
Read a lot of real outputs, write down what's wrong, and group the problems into categories.

**The 5 stages:**
1. **Create an initial dataset:** about 100 diverse traces, real or synthetic
2. **Open coding:** read each trace and write free-form notes on problems
3. **Axial coding:** cluster the notes into a taxonomy of failure modes
4. **Label traces** with the new failure modes
5. **Iterate** until new traces reveal no new failure types

**Why it matters:**
- ✅ Closes the **Gulf of Comprehension**: what's really in your data
- ✅ Exposes **Specification** gaps that only show up during testing
- ✅ Reveals **Generalization** failures on certain input types
- ✅ Turns "my bot isn't great" into "fails 30% of the time because of X"

**Real-life analogy:**
Like a mechanic test-driving the car before ordering parts. Did it misunderstand the ingredients? Ignore a restriction? Make up a cooking method? You find the cause before you fix anything.

**Interview Tip:**
> "Error analysis is the highest-ROI activity in AI engineering: read about 100 traces, open-code the problems, cluster them into a failure taxonomy, and only then build evaluators."

---

## Synthetic Data with Dimensions

### 🎯 Creating an Initial Dataset

**Definition:**
> When you lack production data, generate synthetic queries by sampling combinations of **dimensions**. A dimension is an aspect of the query space that varies in meaningful ways for your application.

**Simple meaning:**
Don't ask an LLM for "a bunch of queries". Decide what makes queries different from each other, then build combinations.

**How much data?** About **100 diverse traces**, enough to reach **theoretical saturation**: the point where new traces stop revealing new error types. Use production data whenever you have it.

**NurtureBoss dimensions:**

| Dimension | Example Values |
|-----------|----------------|
| **Feature / intent** | check availability, pet policy, schedule tour, maintenance request |
| **Persona** | prospect (budget), prospect (luxury), resident (urgent), resident (general) |
| **Scenario / complexity** | clear and complete, ambiguous or missing info, off-topic, multi-turn |

**Two-step process:**
1. Prompt an LLM to generate about 50 `(feature, persona, scenario)` tuples. Review them and drop unrealistic ones.
2. Prompt again, once per tuple, to write a realistic natural-language query. Aim for 100+ queries and review again.

---

**❌ Bad Example:**
```python
# Generic prompt produces repetitive, unrealistic queries
prompt = "Generate 100 user queries for a recipe chatbot."
```

**✅ Good Example:**
```python
import itertools, random

# Step 1: define dimensions (wear your product hat)
dimensions = {
    "diet": ["vegan", "gluten-free", "no restriction"],
    "ingredients": ["chicken & broccoli", "pasta & tomatoes", "just eggs"],
    "meal": ["weeknight dinner", "dessert", "snack"],
    "skill": ["beginner", "experienced"],
}

# Step 2: sample tuples (or ask an LLM to propose realistic ones)
all_tuples = list(itertools.product(*dimensions.values()))
tuples = random.sample(all_tuples, 20)

# Step 3: turn each tuple into a natural query with a second prompt
QUERY_PROMPT = """Write one realistic message a user might send to a recipe bot.
Diet: {0}. Ingredients on hand: {1}. Meal: {2}. Cooking skill: {3}.
Write it casually, like a real person typing on their phone."""

prompts = [QUERY_PROMPT.format(*t) for t in tuples]
# Review the generated queries by hand: dedupe, drop unrealistic ones
```

**Benefits:**
- ✅ Covers the query space on purpose instead of by luck
- ✅ Surfaces edge cases (ambiguous, off-topic) you'd never type yourself
- ✅ Each query is traceable to the dimensions that produced it

**Interview Tip:**
> "I generate synthetic data by defining 3-4 product dimensions, sampling tuples, and then turning each tuple into a natural query, reviewing by hand after each step. Asking an LLM for generic queries gives repetitive data."

---

## Traces and Open Coding

### 🎯 Traces

**Definition:**
> A **trace** is the full record of everything that happens in response to one user query: the input, every LLM call, reasoning, tool calls and retrievals across all components, and the final output.

**Why annotate at the trace level?**
- ✅ Many errors only make sense in the context of the whole flow
- ✅ Errors cascade: one early mistake causes several later symptoms
- ✅ You avoid wasting time labeling every symptom

**First (upstream) failure:** label only the *earliest* mistake in a trace at first. Fixing it often fixes everything downstream. Once you're experienced, label all *independent* failures.

### 🎯 Open Coding

**Definition:**
> Open coding (borrowed from qualitative research) means reading each trace and writing short, descriptive notes about anything that looks wrong, surprising, or unexpected, *without* a predefined list of categories.

**Simple meaning:**
Let the error categories come out of the data instead of guessing them in advance.

**Example open codes (NurtureBoss):**
- "Agent offered tour times that were in the past"
- "Incorrectly identified prospect as current resident"
- "Said 'we have a pool' but didn't share the photo link the user asked for"

**❌ Bad Example:**
```text
# Starting with a generic error list before looking at data
Categories: hallucination, toxicity, verbosity, off-topic
# Result: you only find what you expected, and miss app-specific failures
```

**✅ Good Example:**
```text
trace_017: Asked for vegan lasagna; recipe includes ricotta.
trace_018: Fine.
trace_019: User said "quick"; recipe takes 90 min, no warning.
trace_020: Steps reference "the sauce" that was never made.
# Notes are specific and grounded in what actually happened
```

**Real-life analogy:**
Like a detective writing down every clue at a crime scene before deciding on suspects. If you pick suspects first, you only notice clues that fit them.

**Interview Tip:**
> "Open coding means reading traces and writing free-form notes on the first failure in each, without a preset taxonomy. It finds application-specific failures that generic checklists miss."

---

## Axial Coding and Theoretical Saturation

### 🎯 Axial Coding

**Definition:**
> Axial coding groups similar open codes into a structured **taxonomy of failure modes**, each with a title, a one-sentence definition, and examples.

**Simple meaning:**
Turn a messy pile of notes into a short list of named problem types.

**Process:**
1. Read all your open codes
2. Cluster similar notes
3. Name and define each cluster
4. Go back and re-label traces with the new categories
5. Refine: merge similar categories, split overly broad ones

You *can* paste open codes into an LLM and ask for suggested groupings. Always review and define the final categories yourself.

**Example taxonomy (NurtureBoss):**

| Failure Mode | Definition |
|--------------|------------|
| **Hallucinated tool invocation** | Agent calls a tool that doesn't exist (e.g., "reschedule" when only "schedule new" exists) |
| **Missing visual/link for amenities** | Confirms an amenity but doesn't offer photos or links when asked |
| **Unhelpful response** | Generic, passive answer that doesn't guide the user or clarify their need |

**Output to aim for:** a spreadsheet with `trace_id`, `query`, `open_code_notes`, plus one 0/1 column per failure mode. Counting the columns tells you which problems matter most.

### 🎯 Theoretical Saturation

**Definition:**
> Theoretical saturation is the point where reviewing more traces reveals few or no new failure types.

**Rules of thumb:**
- Stay at a step until you saturate
- About 2 rounds of open and axial coding is usually enough
- Evaluation criteria **drift** as you see more data, which is expected

**Common error analysis pitfalls:**
- ❌ Unrepresentative data (weak dimensions)
- ❌ Skipping open coding and listing failure modes before looking at data
- ❌ Using 1-5 Likert scales too early (use **pass/fail per failure mode**)
- ❌ Not iterating on the taxonomy
- ❌ Excluding domain experts in complex domains
- ❌ Jumping to axial coding too early, which leads to confirmation bias

**Trade-offs:**

| Benefit | Cost |
|---------|------|
| **Binary pass/fail is robust and easy to agree on** | Loses nuance a detailed rubric could capture |
| **First-failure labeling is fast** | Misses independent downstream failures |
| **LLM-suggested clusters save time** | Can impose categories that don't fit your data |

**Interview Tip:**
> "Axial coding clusters open codes into a failure taxonomy with clear definitions. I iterate until theoretical saturation and keep each failure mode binary so it can become an evaluator."

---

## Multi-Turn Evaluation

### 🎯 Multi-Turn Gotchas

**Definition:**
> Multi-turn evaluation applies the same error analysis to conversations. The main differences are how you collect traces and how you isolate a failure.

**Simple meaning:**
Nothing magical changes for conversations, but you need tricks to find where the conversation went wrong.

**Practical strategies:**
1. **Collect traces simply:** have your team role-play personas in a chat UI, 10-15 conversations each, about 100 total
2. **Review manually:** apply error analysis to each full conversation
3. **Isolate:** can you reproduce the failure in a single turn?
   - Shopping bot gives the wrong return policy on turn 4 → ask directly: "Return policy for X1000?"
   - Still wrong → it's a retrieval/grounding issue, not a multi-turn issue
4. **For true multi-turn failures** (like forgetting context): truncate to the N-1 turns before the failure and rerun the LLM several times from there
5. **Advanced:** perturb real traces (e.g., the user changes their mind midway) to test robustness

```python
# N-1 replay: did the bot forget "I love sci-fi"?
def replay_from(conversation, fail_turn, runs=10):
    context = conversation[:fail_turn]          # everything before the failure
    outputs = [call_llm(context) for _ in range(runs)]
    failures = [o for o in outputs if "rom-com" in o.lower()]
    return len(failures) / runs                  # how often does it repeat the mistake?
```

**Real-life analogy:**
Like debugging a long phone call. Replay the recording up to just before the misunderstanding, then see if it happens again.

**Interview Tip:**
> "For multi-turn failures, I first try to reproduce them as single-turn tests. If they really are about context, I replay the N-1 turns many times to measure how consistent the failure is."

---

## Collaborative Evaluation

### 🎯 Collaborative Evaluation

**Definition:**
> Collaborative evaluation brings in several domain experts or stakeholders to define, refine and apply evaluation criteria, especially subjective ones like helpfulness or tone.

**Simple meaning:**
When "correct" is a matter of opinion, one person's judgment isn't enough.

**Benevolent dictator vs team:**

| Use a Benevolent Dictator | Use Multiple Experts |
|---------------------------|----------------------|
| Small or medium company | Large organization or complex domain |
| Subject matter is easy to understand | Even experts find it hard to agree |
| Need to move fast (heavy competition) | High-stakes or life-threatening applications |
| One clear owner (CEO, lead psychologist, lead teacher) | Ground truth for subjective criteria is fuzzy |

**Workflow:**
1. **Assemble team:** 2+ annotators with relevant expertise
2. **Draft rubric:** criterion plus initial pass/fail examples
3. **Shared set:** about 20-50 diverse traces, including tricky ones
4. **Independent annotation:** everyone labels without discussing (this surfaces ambiguity)
5. **Measure IAA:** quantify agreement
6. **Alignment session:** discuss disagreements to fix the **rubric**, not just the labels
7. **Iterate** until agreement is high (Kappa ≥ 0.6)
8. **Finalize** the rubric and a "gold" labeled dataset

**🔍 Classroom example: is this response "helpful"?**

> User: "I need a new place soon, maybe a 1-bed? What's good?"
> Bot: talks about how popular 1-beds are, the great location and quiet atmosphere, then asks about move dates.

With the draft rubric ("Pass = provides relevant information"), people split:
- **Pass:** mentions 1-beds, community features, and moves the conversation forward
- **Fail:** no unit details (price, layout, features) and sidesteps "what's good"

**Ways to fix the rubric:**
- ✅ Clarify wording: what does "useful information" mean?
- ✅ Add pass/fail examples, especially borderline ones
- ✅ Add decision rules: "Must ask at least one clarifying question about the user's needs"
- ✅ Split the criterion: "factual relevance" and "proactivity" as separate checks

**Real-life analogy:**
Like judges at a talent show. If they don't agree on what "good" means beforehand, scores are random. They need a shared scorecard and practice rounds.

**Interview Tip:**
> "For subjective criteria, I have multiple experts label the same traces independently, measure agreement with Cohen's kappa, and use the disagreements to sharpen the rubric until kappa is at least 0.6."

---

## Inter-Annotator Agreement

### 🎯 Percent Agreement vs Cohen's Kappa

**Definition:**
> **Inter-Annotator Agreement (IAA)** measures how consistently different people apply the same rubric. **Cohen's kappa (κ)** measures agreement between two raters *beyond what chance would produce*.

**Simple meaning:**
If 90% of traces pass, two people who answer "pass" every time would "agree" 90% of the time without thinking. Kappa removes that luck.

**Formulas:**
- Percent agreement: `Po = items agreed / total items`
- Chance agreement: `Pe = P(A says Pass)·P(B says Pass) + P(A says Fail)·P(B says Fail)`
- Kappa: `κ = (Po − Pe) / (1 − Pe)`

**Interpreting κ (Landis & Koch, 1977):**

| κ | Agreement |
|---|-----------|
| < 0 | Poor |
| 0.00-0.20 | Slight |
| 0.21-0.40 | Fair |
| 0.41-0.60 | Moderate |
| 0.61-0.80 | Substantial |
| 0.81-1.00 | Almost perfect |

**Goal:** κ ≥ 0.6 for reliable labels.

```python
def cohens_kappa(rater_a, rater_b):
    """Cohen's kappa for two raters with Pass/Fail labels."""
    n = len(rater_a)
    po = sum(a == b for a, b in zip(rater_a, rater_b)) / n

    pa_pass = rater_a.count("P") / n
    pb_pass = rater_b.count("P") / n
    pe = pa_pass * pb_pass + (1 - pa_pass) * (1 - pb_pass)

    return (po - pe) / (1 - pe)

a = ["P", "P", "F", "P", "P", "F", "P", "P", "F", "P"]
b = ["P", "F", "F", "P", "P", "P", "P", "P", "F", "P"]
print(cohens_kappa(a, b))
# Output: 0.52 -> 80% raw agreement, but only "moderate" once chance is removed
```

**Trade-offs:**

| Metric | Benefit | Cost |
|--------|---------|------|
| **Percent agreement** | Simple to explain | Inflated when one label dominates (common in evals) |
| **Cohen's kappa** | Corrects for chance | Only two raters; harder to explain |

**Interview Tip:**
> "Percent agreement is misleading when labels are imbalanced, which is the usual case in evals. Cohen's kappa subtracts chance agreement, and I aim for 0.6 or higher before trusting labels."

---

## Specification vs Generalization Failures

### 🎯 What Should You Measure?

**Definition:**
> A **specification failure** happens because your instructions were unclear or incomplete. A **generalization failure** happens when the LLM fails to apply clear instructions across varied inputs.

**Simple meaning:**
If you never told the model to do it, fix the prompt. If you told it clearly and it still fails sometimes, build an evaluator.

| Type | Example | Action |
|------|---------|--------|
| **Specification** | Bot doesn't share amenity photo links because the prompt never asked it to | ➡️ Fix the prompt first. Don't build an evaluator yet |
| **Generalization** | Bot misses a clearly stated constraint on some inputs | ➡️ Good candidate for an automated evaluator |

**Why it matters:**
- ✅ Saves you from building evaluators for problems a one-line prompt fix solves
- ✅ Focuses measurement effort where it pays off
- ✅ Gets you from qualitative failure modes to quantitative metrics

**Real-life analogy:**
If a new hire never filed the report because no one told them to, that's on you (specification). If they were told and forget half the time, you need a checklist and audits (generalization).

**Interview Tip:**
> "I fix specification failures in the prompt first, then build automated evaluators only for generalization failures, where the instructions are clear but the model still fails sometimes."

---

## Code-Based Evaluators

### 🎯 Code-Based Evaluators

**Definition:**
> Code-based evaluators are deterministic functions that check objective, rule-based properties of an output.

**Simple meaning:**
If you can check it with an `if` statement, don't pay an LLM to check it.

**Use for:**
- Parsing structure (valid JSON, SQL syntax)
- Regex or keyword presence and absence
- Structural constraints ("summary has 3 bullets")
- Tool execution errors
- Comparing against a golden reference

**Why it matters:**
- ✅ Fast and cheap
- ✅ Deterministic and interpretable
- ✅ Can run in the critical path as a guardrail and re-prompt on failure

**Example: hallucinated tool invocation**

```python
# Whitelist the tools the agent is allowed to call
ALLOWED_TOOLS = {
    "get_tour_availability",
    "schedule_tour",
    "check_apartment_availability",
    "get_resident_balance",
    "update_contact_info",
}

def eval_hallucinated_tool(trace: dict) -> bool:
    """Pass (True) if every tool call uses a real tool."""
    for call in trace["tool_calls"]:
        if call["name"] not in ALLOWED_TOOLS:
            return False          # e.g. "reschedule_tour" doesn't exist
    return True

trace = {"tool_calls": [{"name": "reschedule_tour", "args": {}}]}
print(eval_hallucinated_tool(trace))
# Output: False
```

**Tool-call checks come in layers:**
1. Did the agent use the tool at all?
2. Did it produce the right *types* of arguments? (validate with Pydantic or Zod)
3. Are the argument *values* actually correct?

**Interview Tip:**
> "Use code-based evaluators for anything objective, like schemas, regex, whitelists or tool errors. They're fast, cheap and deterministic. Save LLM judges for subjective criteria."

---

## LLM-as-Judge

### 🎯 LLM-as-Judge

**Definition:**
> An LLM-as-Judge is a separate LLM, with a carefully designed prompt, that evaluates your pipeline's output for **one narrowly defined failure mode** and returns pass or fail.

**Simple meaning:**
Use an AI to grade the AI, but only on one clearly defined question at a time.

**Prerequisites:**
- Pick **one** failure mode
- Make it well defined and well scoped
- ❌ "Is this good?" is too vague
- ❌ "Check A, B, C, D and E" should be split into 5 judges
- ✅ Binary: easier to align with human judgment

**4 components of a strong judge prompt:**
1. **Task and criterion:** one specific failure mode
2. **Precise pass/fail definitions**
3. **Few-shot examples:** clear pass and fail cases (from the *training set* only)
4. **Structured output:** JSON with `reasoning` and `answer`

**The judge lifecycle:**
1. Write the prompt template
2. Split labeled data (train/dev/test)
3. Iterate on the dev set until it agrees with humans
4. Measure on the test set, then estimate the true success rate in production

---

**❌ Bad Example:**
```python
# Vague, multi-criterion, no examples, free-form output
JUDGE_PROMPT = "Rate this chatbot response from 1-10 for quality, tone, and accuracy."
```

**✅ Good Example:**
```python
import json
import anthropic

client = anthropic.Anthropic()

JUDGE_PROMPT = """You are an expert evaluator. Assess whether the leasing agent's
response to an AMBIGUOUS user query was helpful and proactive.

FAIL if: the response is generic or passive, adds little new information,
or does not try to clarify what the user actually needs.
PASS if: the response acknowledges the ambiguity and asks relevant follow-up
questions or offers concrete next steps.

<example>
Query: "Looking for a 1-bedroom. What do you have?"
Response: "We have 1-bedrooms with modern appliances. Leases are 12 months."
Judgment: {{"reasoning": "Correct but generic; doesn't narrow down needs.", "answer": "Fail"}}
</example>
<example>
Query: "Looking for a 1-bedroom. What do you have?"
Response: "Happy to help! What's your move-in date and budget? Is in-unit laundry important?"
Judgment: {{"reasoning": "Asks targeted clarifying questions.", "answer": "Pass"}}
</example>

Query: {query}
Response: {response}
Return only JSON: {{"reasoning": "<1-2 sentences>", "answer": "Pass" or "Fail"}}"""

def judge(query: str, response: str) -> dict:
    msg = client.messages.create(
        model="claude-sonnet-5-5",   # pin one model version for consistent results
        max_tokens=200,
        messages=[{"role": "user",
                   "content": JUDGE_PROMPT.format(query=query, response=response)}],
    )
    return json.loads(msg.content[0].text)
```

**Benefits:**
- ✅ One criterion, so judge errors are easy to diagnose
- ✅ The examples calibrate what pass and fail mean
- ✅ Reasoning plus answer is machine-readable and auditable

**Trade-offs:**

| Benefit | Cost |
|---------|------|
| **Handles nuance (tone, helpfulness, faithfulness)** | Costs money and adds latency per call |
| **Scales far beyond human review** | Can be biased or inconsistent |
| **Easy to write a first version** | Needs labeled data and validation to trust |

**When to choose LLM-as-Judge:**
- ✅ Criterion is subjective or needs interpretation
- ✅ You have human labels to validate against
- ❌ Avoid if a regex or schema check would work
- ❌ Avoid if the criterion bundles several things at once

**Interview Tip:**
> "A good LLM judge evaluates one binary failure mode with precise pass/fail definitions, few-shot examples from a training split and structured JSON output. I don't trust it until I've measured TPR and TNR against human labels."

---

## Aligning the Judge: Train, Dev, Test

### 🎯 Splitting Labeled Data

**Definition:**
> Judge alignment treats the judge prompt like a machine learning model. Few-shot examples come from a **train** set, the prompt is tuned on a **dev** set, and final accuracy is measured once on a held-out **test** set.

**Simple meaning:**
Don't grade the judge on the same examples you used to teach it.

| Split | Size | Purpose | Rule |
|-------|------|---------|------|
| **Train** | ~10-20% | Source of few-shot examples in the prompt | Only these can appear in the prompt |
| **Dev** | ~40% | Iteratively tune the prompt | Never put dev examples in the prompt |
| **Test** | ~40% | Final unbiased TPR/TNR | Never look at it during tuning |

**Sizes from the course:** label about 100-200 traces, for example ~20 train / 40 dev / 40 test. Balance pass and fail if you can. Use 2-3 pass and 2-3 fail examples in the prompt, and pick diverse, hard ones.

**Metrics (success = positive class):**
- **TPR (true positive rate):** of the traces humans marked Pass, how many did the judge mark Pass? High TPR means the judge is good at recognizing success.
- **TNR (true negative rate):** of the traces humans marked Fail, how many did the judge mark Fail? High TNR means the judge is good at catching failures.

**Refinement loop:**
1. Write a baseline prompt with train examples
2. Run it on the dev set
3. Compute TPR and TNR against human labels
4. Inspect disagreements
5. Refine wording or swap in better train examples
6. Repeat until TPR and TNR are above 85-90%

**If alignment stalls:** use a more capable judge model, split the criterion into smaller failure modes, or improve your labels.

```python
def tpr_tnr(judge_preds, human_labels):
    """Labels: 1 = Pass (success), 0 = Fail."""
    tp = sum(1 for j, h in zip(judge_preds, human_labels) if h == 1 and j == 1)
    tn = sum(1 for j, h in zip(judge_preds, human_labels) if h == 0 and j == 0)
    positives = human_labels.count(1)
    negatives = human_labels.count(0)
    return tp / positives, tn / negatives

human = [1, 1, 1, 1, 0, 0, 0, 1, 1, 0]
judge = [1, 1, 0, 1, 0, 1, 0, 1, 1, 0]
print(tpr_tnr(judge, human))
# Output: (0.833, 0.75) -> keep refining on dev
```

**FAQ:**
- *Can I use prompt optimization tools (e.g., DSPy)?* Yes, as long as you keep the train/dev/test split.

**Real-life analogy:**
Like studying for an exam. Practice problems are the train set, mock exams are the dev set, and the real exam is the test set. If you memorize the real exam beforehand, your score means nothing.

**Interview Tip:**
> "I split labels into train for few-shot examples, dev for tuning and test for a single final measurement, then tune until TPR and TNR are both above about 85%. Leaking dev or test examples into the prompt inflates the numbers."

---

## Correcting Judge Bias

### 🎯 Estimating the True Success Rate (θ)

**Definition:**
> Because the judge is imperfect, its raw pass rate on new data (`p_obs`) is biased. You correct it with the judge's test-set TPR and TNR to estimate the true success rate **θ̂**.

**Simple meaning:**
If your judge says 82% pass, the real number is something else. A judge that wrongly passes failures inflates it, and one that wrongly fails successes deflates it.

**Steps:**
1. **Final judge accuracy:** run the finalized judge once on the test set to get TPR and TNR
2. **Judge new data:** run it on `m` unlabeled production traces; `k` pass, so `p_obs = k / m`
3. **Correct for bias:**

```
θ̂ = (p_obs + TNR − 1) / (TPR + TNR − 1)      clipped to [0, 1]
```

This is only valid when `TPR + TNR − 1` is well above 0, meaning the judge is better than random.

**🔍 Where the formula comes from:**
`p_obs = θ·TPR + (1 − θ)·(1 − TNR)`. True passes the judge catches, plus true failures it wrongly passes. Solve for θ.

```python
def corrected_success_rate(p_obs: float, tpr: float, tnr: float) -> float:
    """Bias-corrected estimate of the true success rate."""
    denom = tpr + tnr - 1
    if denom <= 0.05:
        raise ValueError("Judge is near random; correction is unreliable")
    theta = (p_obs + tnr - 1) / denom
    return min(1.0, max(0.0, theta))

# Judge passed 820 of 1000 new traces; test-set TPR=0.90, TNR=0.85
print(corrected_success_rate(0.82, tpr=0.90, tnr=0.85))
# Output: 0.893 -> the true rate is ~89%, not 82%
```

**Interview Tip:**
> "A judge's raw pass rate is biased by its own errors, so I correct it with θ̂ = (p_obs + TNR − 1)/(TPR + TNR − 1), using TPR and TNR measured on a held-out test set."

---

## Confidence Intervals with Bootstrap

### 🎯 Quantifying Uncertainty

**Definition:**
> A **95% confidence interval** is a range for θ produced by a procedure that captures the true θ 95% of the time if you repeated it. The course builds it by **bootstrapping** the test set.

**Simple meaning:**
"89%" alone hides how unsure you are. "Between 85% and 92%" tells you whether you're meeting your target.

**Bootstrap algorithm:**
1. Resample the test set (predictions plus labels) with replacement
2. Recompute TPR* and TNR*
3. Recompute θ̂* using the original `p_obs`
4. Repeat many times; the 2.5th and 97.5th percentiles form the 95% CI

```python
import random

def bootstrap_ci(test_preds, test_labels, p_obs, n_boot=2000):
    n = len(test_labels)
    thetas = []
    for _ in range(n_boot):
        idx = [random.randrange(n) for _ in range(n)]
        preds = [test_preds[i] for i in idx]
        labels = [test_labels[i] for i in idx]
        if 0 in labels and 1 in labels:            # need both classes
            tpr, tnr = tpr_tnr(preds, labels)
            if tpr + tnr - 1 > 0:
                theta = (p_obs + tnr - 1) / (tpr + tnr - 1)
                thetas.append(min(1, max(0, theta)))
    thetas.sort()
    return thetas[int(0.025 * len(thetas))], thetas[int(0.975 * len(thetas))]
```

The course's open-source package does this for you: [`judgy`](https://github.com/ai-evals-course/judgy) (`pip install judgy`).

**Use it against an SLO:** if your target is above 90% success and the CI is [0.83, 0.87], you're likely missing it.

**What the simulations showed:**
- **About 100 labels (50 pass / 50 fail)** is a good balance of effort and a tight CI
- **Low TPR** (bad at recognizing success): the CI narrows a lot as TPR improves
- **Low TNR** (bad at catching failures): the CI narrows less as TNR improves
- In both cases you **must** correct the estimate

**Interview Tip:**
> "I report a bias-corrected success rate with a bootstrap 95% confidence interval from the judge's test set, so stakeholders see both the estimate and the uncertainty against our SLO."

---

## Automated Evaluation Pitfalls

### ⚠️ Common Mistakes

| Pitfall | What Goes Wrong | Fix |
|---------|-----------------|-----|
| **Misaligned metrics** | Eval passes but users are still unhappy | Ground metrics in error analysis |
| **Over-confidence in scores** | High offline scores don't predict production | Monitor production, keep doing error analysis |
| **Evaluator drift** | Provider updates the judge model; output formats change | Pin model versions, re-align periodically |
| **Bad few-shot examples** | Judge has no grounding for pass/fail | Pick diverse, hard examples from train |
| **Overly broad criteria** | One judge checks tone + correctness + format | One failure mode per judge |
| **Skipping validation** | Assuming the judge "just works" | Measure TPR/TNR on dev and test |
| **Data leakage** | Dev or test examples in the judge prompt | Few-shot examples come from train only |

**Student takeaways from the homework:**
- ✅ "Just use programmatic evals instead of LLM judges if you can"
- ✅ Log exactly which prompt and model were sent, or you can't debug the evaluation pipeline

**Interview Tip:**
> "The biggest judge pitfalls are data leakage, broad multi-criterion prompts and drift from model updates. I keep one criterion per judge, pin versions and re-check alignment regularly."

---

## Evaluating RAG

### 🎯 Retrieval-Augmented Generation

**Definition:**
> RAG grounds LLM outputs in external knowledge. A **retrieval** step fetches relevant information (from a database, docs, a search engine or any API), and a **generation** step uses the LLM to turn it into an answer.

**Simple meaning:**
Look things up first, then answer. Evaluate the lookup and the answer separately.

| Flavor | Flow | Difference |
|--------|------|------------|
| **Vanilla RAG** | Query → Retriever → LLM → Answer | One retrieval pass |
| **Agentic RAG** | Query → LLM ⇄ Retriever (loops) → Answer | LLM decides what to retrieve and when to stop |

**Key rule:** the evals are the same for both. **Evaluate retrieval first, then generation.**

**Common RAG pitfalls:**
- ❌ Optimizing RAG before error analysis shows that retrieval is actually the problem
- ❌ Not tuning the precision/recall trade-off for your product
- ❌ Not analyzing retrieval failures for patterns
- ❌ Bikeshedding: endlessly trying vector DBs and chunking strategies without error analysis to guide you

**Real-life analogy:**
RAG is an open-book exam. You can fail by opening the wrong page (retrieval) or by misreading the right page (generation). Grade both separately.

**Interview Tip:**
> "I evaluate RAG in two parts: retrieval quality with ranking metrics on (query, relevant chunk) pairs, then generation quality for faithfulness and relevance. Error analysis tells me which part to work on."

---

## Synthetic Retrieval Datasets

### 🎯 Building (Query, Relevant Chunk) Data

**Definition:**
> To evaluate retrieval you need a dataset of queries paired with the chunks that answer them. A **chunk** is the unit of text you retrieve, and its size depends on the domain.

**Chunk size by domain:**

| Domain | Chunk |
|--------|-------|
| E-commerce | Whole product description |
| Legal tech | Single clause |
| Leasing agent | FAQ section, policy section, amenity list |
| Recipe Bot (HW4) | One recipe |

**Basic synthetic generation (per chunk):**
1. LLM picks a salient fact a user would care about
2. LLM writes a realistic question answerable *only* by that fact
3. Store `(question, fact, source_chunk_id)`

> Chunk: "Pool hours are 9 AM-10 PM, Tue-Sun... max two guests per apartment."
> Fact: "Max two guests per apartment at the pool."
> Question: "Can I bring my friend to the pool?"

**Adversarial questions (make it harder):**
1. Pick target chunk A with a clear fact
2. Find similar chunks B, C that share terms but not the fact
3. Ask the LLM for a question answerable only by A, *using vocabulary from B and C*

**Filter bad queries:** use an LLM to rate realism (1-5) and drop unrealistic, too-simple or off-domain questions.

**Tips:**
- ✅ Seed generation with real queries as few-shot examples
- ✅ Generate data *independently* of your retrieval method (BM25, semantic), so you don't bias it toward your retriever
- ✅ Include multi-hop, multi-chunk queries

```python
GEN_PROMPT = """Here is a recipe:
{recipe}

1. Pick one specific, salient detail (a temperature, time, technique, or swap).
2. Write a realistic question a home cook might type that can ONLY be
   answered using that detail from this recipe.
Return JSON: {{"fact": "...", "question": "..."}}"""

dataset = []
for recipe in recipes[:100]:
    out = json.loads(call_llm(GEN_PROMPT.format(recipe=recipe["text"])))
    dataset.append({"query": out["question"], "fact": out["fact"],
                    "source_id": recipe["id"]})
# Then manually review 10+ and refine 5+ for realism and unique answerability
```

**Interview Tip:**
> "I build retrieval eval sets by having an LLM pick a salient fact per chunk and write a question only that chunk answers. I add adversarial questions that borrow vocabulary from similar chunks and filter for realism."

---

## Retrieval Metrics

### 🎯 Recall@k, Precision@k, MRR, NDCG@k

**Definition:**
> Retrieval metrics score the *ranking* of retrieved chunks against the known relevant ones.

| Metric | Question It Answers | Best When |
|--------|---------------------|-----------|
| **Recall@k** | Of all relevant chunks, how many are in the top k? | You need completeness (most important for RAG) |
| **Precision@k** | Of the top k, how many are relevant? | Context is small (matters less as context windows grow) |
| **MRR** | How high is the *first* relevant chunk? | One relevant doc per query ("What are pool hours?") |
| **NDCG@k** | Are the *most* relevant chunks ranked highest? | Several docs with graded relevance |

**Formulas:**
- `Recall@k = |relevant ∩ top_k| / |relevant|`
- `Precision@k = |relevant ∩ top_k| / k`
- `MRR = mean over queries of (1 / rank of first relevant)`, scoring 0 if it isn't in the top k
- `DCG@k = Σ rel_i / log2(i + 1)`, and `NDCG@k = DCG@k / ideal DCG@k`

```python
def recall_at_k(retrieved_ids, relevant_ids, k):
    return len(set(retrieved_ids[:k]) & set(relevant_ids)) / len(relevant_ids)

def reciprocal_rank(retrieved_ids, relevant_ids, k):
    for rank, doc_id in enumerate(retrieved_ids[:k], start=1):
        if doc_id in relevant_ids:
            return 1 / rank
    return 0.0

# HW4 style: one source recipe per query, retriever returns top 5
results = [
    (["r7", "r2", "r9", "r1", "r4"], ["r7"]),   # rank 1
    (["r3", "r5", "r8", "r6", "r0"], ["r8"]),   # rank 3
    (["r1", "r2", "r3", "r4", "r5"], ["r9"]),   # not found
    (["r6", "r4", "r2", "r0", "r1"], ["r4"]),   # rank 2
]
mrr = sum(reciprocal_rank(r, rel, 5) for r, rel in results) / len(results)
r1 = sum(recall_at_k(r, rel, 1) for r, rel in results) / len(results)
print(f"MRR={mrr:.3f}, Recall@1={r1:.2f}")
# Output: MRR=0.458, Recall@1=0.25
```

**Trade-offs:**

| Benefit | Cost |
|---------|------|
| **Higher k improves recall** | Lowers precision; more tokens and cost |
| **MRR is simple and intuitive** | Ignores everything after the first hit |
| **NDCG handles graded relevance** | Needs graded labels, which are harder to collect |

**Interview Tip:**
> "For RAG I lead with Recall@k, since the LLM can't use what wasn't retrieved. I use MRR when there's one answer per query and NDCG when there are several relevant chunks of different value."

---

## Generation Quality in RAG

### 🎯 Faithfulness and Relevance

**Definition:**
> Once retrieval is good, generation quality has two parts (from the ARES framework). **Answer faithfulness** asks whether the answer accurately reflects the retrieved context. **Answer relevance** asks whether it addresses the user's actual question.

**Faithfulness failures:**
- ❌ **Hallucination:** information not in the context
- ❌ **Omission:** key context ignored
- ❌ **Misinterpretation:** context represented inaccurately

**Relevance failure:** an answer can be fully faithful to the context and still miss the question.

**Real-life analogy:**
A student quotes the textbook accurately (faithful) but answers a different question than the one asked (not relevant).

**Interview Tip:**
> "I grade RAG generation on faithfulness (no hallucinations, omissions or misreadings of the context) and relevance (it answers the user's actual question), usually with separate LLM judges."

---

## Tool Calling and Agents

### 🎯 Evaluating Tool Calling

**Definition:**
> In tool calling, the LLM chooses a tool from a predefined list, generates its arguments, and processes its output. Each step can fail independently.

**Simple meaning:**
Check every link in the chain: right tool, right arguments, it ran, and the result was used correctly.

**Foundation: clear tool descriptions.** The LLM depends on tool names, descriptions and parameter specs. If they're ambiguous, tool use will be poor. The gulf of specification applies to tools too.

| Step | What to Check | Evaluator |
|------|---------------|-----------|
| **Selection** | Right tool for the intent? Hallucinated tool? | Code (whitelist) + judge |
| **Arguments** | Schema-valid? Required args present? Semantically right (date format)? Safe (SQL injection)? | Code (Pydantic) + judge |
| **Execution** | Runtime errors, timeouts? **Silent failures** (empty results for a bad ID)? | Code |
| **Output handling** | Misread the result? Ignored key details? Failed to integrate it? | Judge |

⚠️ **Silent failures cause most of the problems in ML engineering.** A query that "succeeds" but returns nothing is the hardest failure to notice.

```python
from datetime import date
from pydantic import BaseModel, ValidationError, field_validator

class ScheduleTourArgs(BaseModel):
    prospect_id: str
    unit_type: str
    tour_date: date

    @field_validator("tour_date")
    @classmethod
    def not_in_past(cls, v: date) -> date:
        if v < date.today():
            raise ValueError("tour date is in the past")
        return v

def eval_tool_args(raw_args: dict) -> bool:
    try:
        ScheduleTourArgs(**raw_args)
        return True
    except ValidationError:
        return False
```

### 🎯 Debugging Multi-Step Agents

**Key to debugging: traceability.** Log every input, LLM reasoning step, tool call (args and response) and decision.

**Transition failure matrix:**
- Do error analysis to identify the agent's **states** (e.g., ParseIntent → PlanTools → CallTool → Compose)
- For each failed trace, label the **first** failing state
- Matrix: rows = last successful state, columns = state of first failure, cells = counts
- Hot cells show where the agent breaks most

```python
from collections import Counter

# (last_successful_state, first_failed_state) per failed trace
failures = [("ParseIntent", "PlanTools"), ("PlanTools", "CallTool"),
            ("PlanTools", "CallTool"), ("CallTool", "Compose"),
            ("PlanTools", "CallTool")]
matrix = Counter(failures)
print(matrix.most_common(1))
# Output: [(('PlanTools', 'CallTool'), 3)] -> fix tool invocation first
```

A related idea is **failure funnels**: track how many traces survive each step. Bryan Bischof covered these in his guest lecture.

**Interview Tip:**
> "I evaluate tool calling at each stage: selection, argument validity and semantics, execution including silent failures, and output handling. For agents I label the first failing state and build a transition failure matrix to find hotspots."

---

## Other Input Modalities

### 🔍 Images, Long Documents, PDFs

**Definition:**
> Analyze-Measure-Improve still applies to non-text inputs. What changes is the set of typical failure modes and how a judge sees the input.

| Modality | Common Failures | Evaluation Focus |
|----------|-----------------|------------------|
| **Images (understanding)** | Spatial reasoning, counting, OCR errors, hallucinated objects | Judge must *see* the image (VLM or human) |
| **Images (generation)** | Complex compositions, exact counts, distinct identities, global constraints | Visual rubrics |
| **Long docs: constant-output** ("needle in a haystack") | Info "lost in the middle" | Accuracy vs position of the info |
| **Long docs: variable-output** (extract *all* entities) | Misses as doc length grows | Tune chunk size; check the aggregated result |
| **PDFs** | Bad OCR, mangled tables, wrong reading order | Separate extraction errors from LLM errors |

**Long-document tips:**
- Don't feed the full document to a judge (cost, limits, degraded accuracy). Give it snippets or evaluate per chunk.
- For "extract all logical fallacies from this debate", start with the whole doc as one chunk, then try smaller chunks and compare how many valid items each finds.

**PDF tip:** digitally native PDFs extract far better than scanned ones. How you represent extracted tables to the LLM affects performance. Inspect the intermediate extracted text when debugging.

**Interview Tip:**
> "For PDFs I separate extraction errors from reasoning errors by inspecting the text the LLM actually received. For long documents I tell needle-in-a-haystack tasks apart from variable-output tasks and tune the chunking."

---

## Continuous Integration

### 🎯 CI for LLM Pipelines

**Definition:**
> LLM CI runs a suite of evaluators on a curated **golden dataset** for every change, to catch regressions on **known** failure modes ("known unknowns").

**Simple meaning:**
Unit tests for your prompts. They guard against past bugs coming back. They don't predict production accuracy.

**Why LLM CI/CD is different:**
- Nondeterminism and black-box model updates
- Subjective definitions of quality
- Little labeled data for specific failures

**Golden dataset:**
- Core features and capabilities
- Past critical failures (regression tests)
- Challenging edge cases
- Examples that exercise each pipeline path (tool calls, RAG)
- Usually **100+ examples**, hand-curated, **not** a random production sample

**Example CI checks (real estate assistant):**

| Check | Type | How |
|-------|------|-----|
| **Factual consistency** | LLM judge | Given the output plus the listing data: "Is anything contradicted or unsupported?" |
| **Tool argument schema** | Code | Validate args against the schema |
| **Email address existence** | Code | Recipient email matches the reference |

```python
# tests/test_golden.py, run on every prompt or model change
import json, pytest

GOLDEN = [json.loads(line) for line in open("golden.jsonl")]

@pytest.mark.parametrize("case", GOLDEN, ids=lambda c: c["id"])
def test_golden_case(case):
    output = run_pipeline(case["input"])
    assert eval_hallucinated_tool(output["trace"])
    if "expected_email" in case:
        assert output["email_to"] == case["expected_email"]
    if "listing_data" in case:
        verdict = factual_consistency_judge(output["text"], case["listing_data"])
        assert verdict["answer"] == "Pass", verdict["reasoning"]
```

**Rules:**
- ✅ **Pin judge model versions** for consistent results
- ✅ Keep adding new failure modes, often found through monitoring
- ❌ **Mistake 1:** assuming the CI pass rate predicts production accuracy
- ❌ **Mistake 2:** data leakage, such as golden examples in pipeline or judge prompts

**Interview Tip:**
> "CI runs code and LLM evaluators on a hand-curated golden set of 100+ examples on every change. It measures stability against known failures, not production accuracy."

---

## Continuous Deployment and Monitoring

### 🎯 Online Monitoring

**Definition:**
> CD and online monitoring track live behavior on sampled production traffic to find true performance and surface new failure modes ("unknown unknowns").

**Log everything per request:** input and metadata, every LLM call (prompt, response, reasoning), tool calls (args, responses, errors), retrieved docs, final output, user feedback (thumbs, edits), and evaluator outputs. Organize them into **traces, spans and sessions**.

**Tools:** LangSmith, Arize Phoenix, W&B Weave, OpenTelemetry.

### 🎯 Async Evals vs Guardrails

| Aspect | Async Evals | Guardrails |
|--------|-------------|------------|
| **Timing** | After the response, offline | Before the response, in real time |
| **Purpose** | Estimate accuracy per failure mode | Block known failures |
| **Evaluators** | 5-7 key ones, code + LLM judge | Lightweight code (regex, schema, blocklists) |
| **Coverage** | 1-5% stratified sample | Every request |
| **Output** | θ̂ + 95% CI on a dashboard, with alerts | Reject, retry or fallback |
| **Requirement** | Aligned judges | Very fast, very low false-failure rate |
| **Use for** | Tracking quality trends | PII, toxicity, SQL validity, formats |

```python
import re

SSN = re.compile(r"\b\d{3}-\d{2}-\d{4}\b")

def guarded_response(query, max_retries=2):
    for _ in range(max_retries + 1):
        out = run_pipeline(query)
        if not SSN.search(out):              # guardrail: no SSNs leave the system
            return out                       # pass
    return "Sorry, I can't share that information."  # fallback / safe response
```

### 🎯 Keeping Judges Aligned

**Judges drift** when providers update models or when your team's quality definition changes.

- ✅ **Pin exact model versions** for judges in CI and production
- ✅ **Re-alignment loop:** every few weeks, sample recent traces, get fresh human labels and recompute TPR and TNR
- ✅ If TPR or TNR drops: update the prompt and examples, revalidate, redeploy
- ✅ Re-evaluate the judge whenever its underlying model changes

**Common mistakes:**
- ❌ Stale golden datasets
- ❌ Relying only on automated monitoring. Humans still need to go "failure hunting"
- ❌ Ignoring product metrics. A change in engagement is a signal to do more error analysis
- ❌ Outdated TPR/TNR, which makes θ̂ wrong
- ❌ Insufficient logging

**Real-life analogy:**
CI is the pre-flight checklist: it catches known problems before takeoff. CD monitoring is the in-flight instruments: they warn about things the checklist couldn't anticipate. Guardrails are the autopilot's hard limits.

**Interview Tip:**
> "In production I run async evals on a 1-5% sample to dashboard a bias-corrected success rate per failure mode, use fast code-based guardrails to block critical failures in real time, and re-align judges every few weeks."

---

## Custom Review Interfaces

### 🎯 Why Build Custom UIs?

**Definition:**
> A custom review interface is a lightweight app, built for your domain, for reading and labeling traces. It replaces spreadsheets and generic log viewers.

**Simple meaning:**
Error analysis is the highest-ROI activity, and good review tools are the second highest, because they let humans give far more high-quality feedback.

**Spreadsheet hell:**
- ❌ Thousands of traces jammed into a few columns
- ❌ No keyboard shortcuts, no filtering
- ❌ Fewer than 20 traces/hour, so the feedback loop stalls

**Custom UIs give about 10× throughput:**
- ✅ **Domain-native view:** a generated email looks like an email, not a JSON cell
- ✅ **Hotkeys and one-click tags:** about 200 traces/hour
- ✅ **About 1 hour to prototype** with Streamlit, Gradio or vibe-coded FastAPI + HTML

**HCI principles (Nielsen):**
- **Visibility of status:** trace number and backlog always visible
- **Recognition over recall:** pre-filled failure-mode chips, not free-text hunting
- **Match the real world:** domain terms and visuals
- **User control:** hotkeys, undo, "Defer" for uncertain cases
- **Minimalist:** show less by default, expand on demand

**Speed and accuracy boosters:**
- Single-trace canvas with collapsible panels and inline highlights
- Pass/fail in one key press; number keys select tags
- Progress bar and timer to keep pace and fight fatigue
- Batch-label similar traces after clustering
- Context badges: pipeline version, user segment, prior judge verdict

**Close the loop automatically:**
- "Add to golden set" button writes straight to the CI test file
- Labels export as clean JSON/CSV
- Dashboard flags disagreements between humans and the LLM judge
- Ambitious option: an "Improve prompt" button sends failures to a prompt-improvement agent

**Start small:** a single-trace viewer with open-code notes, pass/fail/skip, saving to JSONL and random sampling. Don't add predefined failure modes until you know them. Build a side-by-side viewer if you're comparing outputs.

```python
# Minimal annotation app: one trace at a time, saves to JSONL
import json, random
import streamlit as st

traces = [json.loads(l) for l in open("traces.jsonl")]
if "i" not in st.session_state:
    st.session_state.i = random.randrange(len(traces))
t = traces[st.session_state.i]

st.caption(f"Trace {t['id']}")
st.chat_message("user").write(t["query"])
st.chat_message("assistant").write(t["response"])

note = st.text_input("Open code (what went wrong?)")
col1, col2, col3 = st.columns(3)
for col, label in [(col1, "pass"), (col2, "fail"), (col3, "skip")]:
    if col.button(label.title()):
        with open("labels.jsonl", "a") as f:
            f.write(json.dumps({"id": t["id"], "label": label, "note": note}) + "\n")
        st.session_state.i = random.randrange(len(traces))
        st.rerun()
```

**Interview Tip:**
> "Custom review UIs give about 10× the throughput of spreadsheets: domain-native rendering, hotkeys, preset failure tags and an 'add to golden set' button. You can vibe-code one in about an hour."

---

## Sampling Traces

### 🎯 Which Traces to Review

**Definition:**
> Sampling picks a manageable subset of production traces (about 100 per week) for human review.

| Strategy | How | Best For |
|----------|-----|----------|
| **Random** | Uniform sample | Starting point; unbiased view |
| **Uncertainty** | Judges disagree or confidence is low | Edge cases; improving judges |
| **Failure-driven** | Guardrail violations, exceptions, user-flagged bugs | Highest-severity issues |

Mix and match strategies. Start with random sampling.

**Interview Tip:**
> "I start with random sampling, then mix in uncertainty sampling where judges disagree and failure-driven sampling from guardrail hits and user reports. About 100 traces a week is usually enough."

---

## Case Studies: EvalGen and DocWrangler

### 🔍 EvalGen

**What:** an early UI (Dec 2023) for human evaluation of single-turn LLM outputs. It has binary thumbs up/down grading, open comments, editable past labels and a rubric builder that extracts criteria from the prompt. A user study with 9 AI/ML engineers found:
- **Criteria drift:** reviewers refine their standards as they grade more outputs, so rubrics and labels must be editable. This is why the course teaches open and axial coding.
- New failure modes appear mid-review, so the UI needs tag creation on the fly
- Code-based and AI-based evaluators need different alignment approaches
- A judge-disagreement queue drove attention to useful edge cases

**EvalGen v2** added visible status indicators and per-criterion grading with live rubric refinement. It's available as a research preview in ChainForge.

### 🔍 DocWrangler

**What:** an IDE for document-level LLM pipelines. You batch-run a prompt over many documents and inspect each result next to its source and the prompt (e.g., "summarize all reported illnesses in these doctor-patient transcripts").
- Free-text notes capture open codes with little friction
- **"Suggest Prompt Update"** turns accumulated notes into a revised prompt, which you can accept, tweak or reject
- **Learning:** people find gulf-of-specification issues within about 5 open codes. Close the specification gulf through fast iteration, *then* move to systematic evals in code.

**Interview Tip:**
> "EvalGen showed that criteria drift as people grade, so labels and rubrics must stay editable. DocWrangler showed that open-coded notes can drive prompt updates directly, closing the specification gulf quickly."

---

## Improving Accuracy

### 🎯 The Improve Phase

**Definition:**
> Improvement means applying targeted fixes to measured failure modes, starting with the lowest-effort, highest-impact change.

**Simple meaning:**
Try the cheap fixes first. Fine-tuning comes last.

| Effort | Strategy | When |
|--------|----------|------|
| **Quick wins** | Clarify wording; add 2-3 targeted few-shot examples; role guidance; step-by-step reasoning with examples | Always start here |
| **Medium** | **Task decomposition** (extract intent → call tool → summarize) | One call is doing too much |
| **Medium** | **Tune RAG:** chunking, number of docs, agentic retrieval | Error analysis points at retrieval |
| **Medium** | **Fix tool misuse:** clarify tool descriptions, params, formats | Bad tool arguments |
| **Advanced** | **Fine-tuning** | 100s of quality labels for a recurring failure prompting can't fix |
| **Advanced** | **Systematic prompt optimization** (A/B, DSPy) against a golden set | The prompt is a tunable artifact |
| **Advanced** | **Human review loops** | High-stakes tasks |

**Trade-offs:**

| Benefit | Cost |
|---------|------|
| **Prompt fixes are fast and cheap** | Can't fix fundamental generalization limits |
| **Decomposition isolates failures** | More calls, more latency, more to evaluate |
| **Fine-tuning locks in behavior** | Expensive; must redo as base models improve |

**Interview Tip:**
> "I improve in order of effort: prompt clarity and targeted few-shot examples, then task decomposition, RAG or tool-description fixes, and fine-tuning only when I have hundreds of labels for a failure that prompting can't fix."

---

## Reducing Cost

### 🎯 Simple Cost Strategies

**Definition:**
> Cost optimization lowers spend per request while holding the accuracy you already measured.

**Strategies:**
- ✅ **Right-size models:** cheap models for easy tasks, expensive ones for hard tasks
- ✅ **Reduce input tokens:** summarize long docs once with a cheap model, then work from the summary
- ✅ **Reduce output tokens:** ask for concise answers; use YAML or XML instead of verbose JSON (when you're not tool calling)
- ✅ **Leverage prompt caching:** static content first, dynamic content last

### 🔧 How KV Caching Works

Transformers compute **Key (K)** and **Value (V)** vectors for every token. That's expensive, so providers cache them. A cache hit requires an **identical prompt prefix**, and cached tokens are billed at a 50-90% discount.

**❌ Bad Example:**
```python
# Dynamic content first: the prefix changes every request, so nothing is cached
prompt = f"User question: {question}\nDocs: {docs}\n\n{LONG_STATIC_INSTRUCTIONS}"
```

**✅ Good Example:**
```python
# Static instructions first: same prefix every time, so cache hits
prompt = f"{LONG_STATIC_INSTRUCTIONS}\n\nDocs: {docs}\nUser question: {question}"
```

**Interview Tip:**
> "Put static instructions and system prompts before dynamic content so the KV cache prefix matches. Cached tokens cost 50-90% less."

---

## Model Cascades

### 🎯 Model Cascades

**Definition:**
> A model cascade sends each query to a cheap **proxy** model first and escalates to an expensive **oracle** model only when the proxy's confidence is below a threshold `T`.

**Simple meaning:**
Let the junior handle easy questions and pass the hard ones to the senior expert.

**Use only when you already have good accuracy** and want to cut cost.

**Measuring confidence with logprobs:**
- APIs can return the log probability of each generated token; closer to 0 means more confident
- For classification (Pass/Fail, True/False), get the logprobs of each label, convert them to probabilities and normalize

```
logprob('True') = -0.1  →  p ≈ 0.90
logprob('False') = -2.3 →  p ≈ 0.10
confidence(True) = 0.90 / (0.90 + 0.10) = 90%
```

**Tuning the threshold (per class):**
1. Run the proxy on a labeled dev set and record `(confidence, correct?)`
2. Sort by confidence
3. For each candidate `t`: keep predictions ≥ `t` and escalate the rest (assume the oracle is right)
4. Pick the **lowest** `t` that meets the accuracy target, which gives the most savings
5. If no `t` works, set it to infinity (always escalate that class)

```python
import math

def confidence(logprobs: dict, label: str) -> float:
    probs = {k: math.exp(v) for k, v in logprobs.items()}
    return probs[label] / sum(probs.values())

def find_threshold(dev, target_acc=0.95):
    """dev: list of (proxy_confidence, proxy_was_correct) for one predicted class."""
    for t in sorted({c for c, _ in dev}):
        kept = [ok for c, ok in dev if c >= t]
        escalated = len(dev) - len(kept)
        acc = (sum(kept) + escalated) / len(dev)      # oracle assumed correct
        if acc >= target_acc:
            return t, escalated / len(dev)            # threshold, escalation rate
    return math.inf, 1.0                              # always escalate

dev = [(0.99, True), (0.97, True), (0.95, True), (0.90, False),
       (0.85, True), (0.70, False), (0.60, True), (0.55, False)]
print(find_threshold(dev, target_acc=0.95))
# Output: (0.95, 0.625) -> accept proxy when confidence >= 0.95, escalate ~62%
```

**Generative tasks:** there are no discrete classes, so treat all examples as one group and score proxy outputs pass/fail against an oracle or human answer, often with an LLM judge. Confidence measures like average logprob per token are **experimental and less reliable**.

**Trade-offs:**

| Benefit | Cost |
|---------|------|
| **Big savings when most queries are easy** | Needs labeled data to tune `T` |
| **Accuracy target is explicit** | Escalated queries pay for both models (more latency) |
| **Reliable for classification** | Experimental for open-ended generation |

**When to choose a cascade:**
- ✅ High volume, mostly easy queries
- ✅ Classification-style outputs with logprobs available
- ❌ Avoid if accuracy isn't already measured and good
- ❌ Avoid if the API doesn't expose logprobs

**Interview Tip:**
> "A model cascade routes queries to a cheap proxy and escalates low-confidence ones to an expensive oracle. Confidence comes from normalized logprobs, and I tune the threshold on labeled dev data to the lowest value that meets the accuracy target."

---

## Common Interview Questions

### Basic Questions

**1. What is LLM evaluation and why does it matter?**
> "It's the systematic measurement of pipeline quality on your application's data. It builds user trust, catches regressions and drives improvement with evidence instead of guesswork."

**2. What are the Three Gulfs?**
> "Comprehension (understanding your data and the model's behavior), Specification (translating intent into precise prompts) and Generalization (working reliably on unseen inputs)."

**3. What is the Analyze-Measure-Improve lifecycle?**
> "Analyze failures qualitatively through error analysis, Measure them with automated evaluators, then Improve the prompts, models or architecture, and repeat."

**4. What is a trace?**
> "The full record of everything that happens for one user query: inputs, every LLM call, tool calls, retrievals and the final output."

**5. Why use pass/fail instead of a 1-5 scale?**
> "Binary judgments per failure mode are easier for humans to agree on, easier to align an LLM judge to and more actionable. Likert scales without detailed rubrics are noisy."

**6. When should you use a code-based evaluator vs an LLM judge?**
> "Use code for anything objective, like schemas, regex, whitelists and tool errors, because it's fast, cheap and deterministic. Use an LLM judge only for subjective criteria like helpfulness or faithfulness."

### Intermediate Questions

**1. How do you do error analysis?**
> "Collect about 100 diverse traces (synthetic from product dimensions if needed), open-code the first failure in each, axial-code the notes into a failure taxonomy, re-label and iterate until theoretical saturation."

**2. How do you generate good synthetic data?**
> "Define 3-4 dimensions like intent, persona and scenario, sample tuples, then have an LLM write a natural query per tuple, reviewing by hand after each step. Never just ask for generic queries."

**3. What's the difference between a specification and a generalization failure?**
> "A specification failure means the instructions were unclear, so you fix the prompt. A generalization failure means the instructions were clear but the model fails on some inputs, and that's where automated evaluators belong."

**4. How do you measure inter-annotator agreement?**
> "Cohen's kappa, which corrects percent agreement for chance: κ = (Po − Pe)/(1 − Pe). I aim for 0.6 or higher and use disagreements to refine the rubric."

**5. How do you evaluate a RAG system?**
> "Separately: retrieval with Recall@k, MRR or NDCG on synthetic (query, chunk) pairs, then generation for faithfulness and relevance. Error analysis tells me which part is failing."

**6. What goes in a CI golden dataset?**
> "100+ hand-curated examples covering core features, past critical failures, edge cases and every pipeline path. It tests stability against known failures, not production accuracy."

### Advanced Questions

**1. How do you build a trustworthy LLM judge?**
> "Pick one binary failure mode and split labels into train/dev/test. Few-shot examples come only from train, I tune the prompt on dev until TPR and TNR are above about 85%, and I measure once on test. If it stalls, I split the criterion or use a stronger model."

**2. Your judge says 82% of production traces pass. Is the true success rate 82%?**
> "No. The raw rate is biased by judge errors. Correct it with θ̂ = (p_obs + TNR − 1)/(TPR + TNR − 1) using test-set TPR and TNR, and report a bootstrap 95% confidence interval."

**3. How do you evaluate a multi-step agent?**
> "Log full traces, identify the agent's states through error analysis, label the first failing state per trace and build a transition failure matrix to find hotspots. Each tool call gets checked for selection, arguments, execution (including silent failures) and output handling."

**4. Async evals vs guardrails?**
> "Async evals run 5-7 evaluators on a 1-5% sample after the fact to track bias-corrected success rates. Guardrails are fast, code-based checks on every request that reject, retry or fall back on critical failures like PII leaks."

**5. How do you keep LLM judges reliable over time?**
> "Pin exact model versions, re-label a fresh production sample every few weeks to recompute TPR and TNR, and re-align and revalidate the judge whenever they drop or the underlying model changes."

**6. How would you cut LLM costs without losing accuracy?**
> "Right-size models per task, cut input and output tokens, put static content first for KV cache hits and, for classification, use a model cascade with a logprob-confidence threshold tuned on labeled data."

**7. When is fine-tuning the right fix?**
> "Only after prompt fixes, decomposition and RAG or tool fixes fail, and only when you have hundreds of high-quality labels for a recurring failure. It's expensive and has to be redone as base models improve."

---

## 🎓 Summary

**The core idea:**
> Move from "prompt-and-pray" to evaluation-driven engineering. Analyze → Measure → Improve is a repeatable process for building reliable AI.

| Week | Key Takeaway |
|------|--------------|
| **1** | Read your data. Error analysis (open → axial coding) is the highest-ROI activity |
| **2** | Measure generalization failures with code first, aligned LLM judges second, and correct for judge bias |
| **3** | Evaluate retrieval and generation separately; CI guards known failures, monitoring finds unknown ones |
| **4** | Invest in review interfaces; improve cheap-first; cut cost with caching and cascades |

**Final advice from the course:**
- ✅ **Start small:** one failure mode, one evaluator, one targeted improvement
- ✅ **Iterate:** your taxonomy, rubrics and judges will all drift, and that's expected
- ✅ **Stay rigorous with data** and never lose sight of the *user's* definition of quality

**Resources:**
- [Course homework repo](https://github.com/ai-evals-course/recipe-chatbot)
- [judgy: bias-corrected success rates](https://github.com/ai-evals-course/judgy)
- [Hamel's field guide to improving AI products](https://hamel.dev/blog/posts/field-guide/)
- [EvalGen write-up](https://ianarawjo.medium.com/evalgen-helping-developers-create-llm-evals-aligned-to-their-preferences-26757f7e145d)
- [Precision and recall at k](https://www.evidentlyai.com/ranking-metrics/precision-recall-at-k)
- [Failure funnels (Hex)](https://hex.tech/blog/im-sorry-but-those-are-vanity-evals/)
- [Cost control guide](https://ai.intellectronica.net/cost-control-guide)
