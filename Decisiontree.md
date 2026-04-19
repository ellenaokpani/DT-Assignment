DT-Assignment

Daily Reflection Tree — Deterministic Reflection Agent

## Overview

This project implements a **deterministic end-of-day reflection system** designed to guide employees through structured self-awareness.

Unlike journaling tools or AI chatbots, this system:

* Uses **no LLM at runtime**
* Is **fully deterministic** (same inputs → same outputs)
* Encodes psychological insight into a **navigable decision tree**

The goal is not to evaluate users — but to help them **notice patterns in how they think, act, and relate to others**.

---

## 🧠 Core Concept

The system walks the user through three psychological axes:

### 1. Locus — Victim → Victor

* Do I see my day as something that happened *to me* or something I *shaped*?

### 2. Orientation — Entitlement → Contribution

* Did I focus on what I *received* or what I *gave*?

### 3. Radius — Self → Others

* Was my attention centered on *my experience* or on *shared impact*?

Each axis builds on the previous one — forming a **progressive shift in awareness**.

---

## ⚙️ How It Works

The product is a **tree-structured dataset** (see `/tree/reflection-tree.tsv`).

Each session:

1. Starts at a root node
2. Asks questions with **fixed options only**
3. Routes deterministically via decision nodes
4. Accumulates **signals** (e.g. `axis1:internal`)
5. Displays reflections using **pre-written templates**
6. Ends with a synthesized summary

No randomness. No interpretation. No AI.

---

## 🌲 Tree Structure

Each node contains:

| Field      | Description                                            |
| ---------- | ------------------------------------------------------ |
| `id`       | Unique node identifier                                 |
| `parentId` | Parent node (defines tree structure)                   |
| `type`     | Node type (`question`, `decision`, `reflection`, etc.) |
| `text`     | Display text (supports interpolation)                  |
| `options`  | Fixed user choices (pipe-separated)                    |
| `target`   | Explicit jump (used for bridges)                       |
| `signal`   | State updates (e.g. `axis2:contribution`)              |

---

## 🔁 Node Types

* **start** — Opens the session
* **question** — User selects from fixed options
* **decision** — Routes based on prior answers or signals
* **reflection** — Displays insight/reframe
* **bridge** — Connects axes
* **summary** — Final synthesis of session
* **end** — Closes session

---

## 🧩 Design Philosophy

### 1. Reflection, Not Survey

The system is designed as a **guided conversation**, not a questionnaire.

* Questions are intentionally **ambiguous but meaningful**
* Options represent **real internal states**, not “right vs wrong”

---

### 2. Progressive Awareness

Each axis builds on the previous:

* Agency (Axis 1) → enables → Contribution (Axis 2)
* Contribution → expands → Perspective (Axis 3)

---

### 3. Mirror → Then Reframe

Every reflection follows a pattern:

1. Acknowledge the user’s experience
2. Introduce a subtle shift in perspective

Example:

> “That sounds like a day where things felt out of your control.
> But even in that — you made choices. Some small, some automatic.”

---

### 4. Deterministic but Personal

Although the system is static:

* Interpolation (`{A1_OPEN.answer}`) makes it feel contextual
* Signal accumulation enables **different reflections for different paths**

---

## 🌿 Branching Strategy

The tree branches in two ways:

### 1. Immediate Answer-Based Routing

Example:

* “Productive” → high agency branch
* “Frustrating” → low agency branch

### 2. Accumulated Signal Routing

Example:

* Multiple “external” signals → deeper reflection on agency
* Mixed signals → nuanced reflection

This allows the system to feel **adaptive without being probabilistic**.

---

## 🎯 Design Decisions & Trade-offs

### Why fixed options only?

* Forces clarity in thought
* Eliminates ambiguity in interpretation
* Ensures deterministic branching

Trade-off:

* Less expressive than free text

Mitigation:

* Carefully crafted options that reflect **real internal states**

---

### Why no scoring system?

* Scores feel evaluative and judgmental
* Reflection should promote **awareness, not performance tracking**

Instead:

* The system surfaces **patterns**, not grades

---

### Why multiple reflections per axis?

* One reflection is often too shallow
* Multiple reflections allow:

  * Reinforcement
  * Nuance
  * Emotional progression

---

## 📚 Psychological Foundations

This tree is informed by:

* **Locus of Control (Julian Rotter)**
  Differentiates internal vs external attribution of outcomes

* **Growth Mindset (Carol Dweck)**
  Emphasizes adaptability and learning through effort

* **Psychological Entitlement (Campbell et al.)**
  Highlights focus on perceived deserved outcomes

* **Organizational Citizenship Behavior (Organ)**
  Captures discretionary contribution beyond formal roles

* **Self-Transcendence (Abraham Maslow)**
  Expands focus beyond self to broader meaning

* **Perspective-Taking (Batson)**
  Encourages understanding others’ experiences

---

## 🔍 What Makes This Tree Effective

### 1. Honest Options

Options are not idealized — they reflect **how people actually think**

---

### 2. Non-Moralizing Tone

The system avoids:

* Blame
* Judgment
* Forced positivity

Instead, it:

* Observes patterns
* Invites reconsideration

---

### 3. Continuity Across Axes

Each axis references prior answers, creating a **coherent narrative**

---

## 🚀 Future Improvements

With more time, I would:

### 1. Add Deeper Mid-Branch Variants

* More nuanced reflections for mixed-signal users

### 2. Introduce “Pattern Memory”

* Track trends across multiple days (still deterministic)

### 3. Expand Edge Cases

* Handle disengaged users (fast-clicking behavior)
* Add re-engagement nodes

### 4. UX Enhancements (if building UI)

* Progress indicator across axes
* Visual feedback for reflection depth

---

## 📂 Project Structure

```
/tree/
  reflection-tree.tsv
  tree-diagram.md

/agent/ (optional)
  cli-runner.js / main.py

/transcripts/ (optional)
  persona-1.md
  persona-2.md

write-up.md
README.md
```

---

## 🧪 How to Use (Conceptually)

1. Start at `START`
2. Render node text
3. If `question` → wait for user input
4. If `decision` → route based on rules
5. Accumulate signals
6. Continue until `END`

---

## 💡 Final Thought

This system is built on a simple belief:

> People don’t need better answers.
> They need better questions — asked in the right order.

---
