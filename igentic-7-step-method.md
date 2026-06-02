# The 7-Step Method

## Structured prompting for capable AI, by hand, in real time

A practical method for getting reliable, focused work out of generative AI tools like Copilot and chat assistants. It is the human form of the iGentic specification: the same discipline that directs an autonomous agent, reduced to seven parts a person can apply selectively, prompt by prompt.

---

## Why it works

A capable model does not give you a poor answer because it is weak. It gives you a poor answer when you leave it too much room. At every step the model is choosing what to do next from a wide field of options, and a wide field is what shows up as a vague, generic, or off-target reply. The method narrows that field. Each part you add puts something useful in front of the model and keeps the rest out of its way.

There is a deeper reason to bother. We tend to call software "reliable" when it does two things at once: it gives the right answer (accuracy), and it gives the same answer every time (determinism). A calculator gives both for free. A reasoning model gives neither for free. The method is how you buy back the parts that matter, by hand, and only where the stakes call for it. A precise task buys accuracy. A verification step buys reliability. A fixed output buys consistency of form. You are not turning the model into a calculator. You are deciding, deliberately, how much rigour each prompt deserves.

That last point is the whole discipline. You do not use all seven parts every time. Which parts you reach for is a risk decision. A throwaway question needs almost nothing. A consequential one, especially in a regulated setting, earns more.

---

## The seven parts

### 01 · Role

**What:** the lens or expertise you want the model to adopt.

**Why:** it sets the vocabulary, depth, and assumptions of the answer. "As a compliance analyst" produces different framing than no role at all.

**Template:** "Act as a [role] who [relevant expertise or perspective]."

**When:** when a specific perspective or domain framing improves the answer. Skip it for simple factual asks.

### 02 · Task

**What:** exactly what you want done, and why. The action and its purpose.

**Why:** this is the highest-leverage part. A vague task leaves the field wide and the model guesses; a precise task aims it at the right target. Stating the purpose, not only the action, helps the model make good calls on everything you did not spell out.

**Template:** "[Verb] [object] so that [purpose]." For example, "Summarise this policy so a new starter can follow it on day one."

**When:** always. If you use only one part, use this one.

### 03 · Inputs

**What:** the material, context, or data the model should use, and ideally only that.

**Why:** it grounds the answer in your reality and stops the model inventing. Naming the source also bounds it.

**Template:** "Use only the text below. Do not add outside information."

**When:** whenever the answer depends on specific material. This is one of the strongest defences against a confident, wrong answer.

### 04 · Steps

**What:** the approach or sequence you want the model to follow.

**Why:** for multi-part work, telling the model how to proceed keeps it from skipping or reordering, and it makes the work easier to check afterwards.

**Template:** "Work in this order: first [X], then [Y], finally [Z]."

**When:** for analysis or anything with a method. Skip it for simple asks.

### 05 · Constraints

**What:** the boundaries. What the model must do, must not do, must avoid.

**Why:** it keeps the answer inside policy and scope. The "must never" lines are where compliance lives.

**Template:** "Must: [requirement]. Never: [prohibition]. Stay within [scope]."

**When:** when scope, policy, or safety matter. Essential in regulated work.

### 06 · Verification

**What:** ask the model to check its own work, against the task, the inputs, and the constraints, before it gives you the answer.

**Why:** left alone, a model hands over a first pass and stops, because it has no standard for "good enough." A verification step catches the errors a first pass misses and steadies the result from one run to the next. It is the cheapest reliability you can buy. It is the re-check instinct: on anything that matters, you do not trust the first figure, you check it.

**Template:** "Before answering, check your draft against [the source / the constraints / the task]. List anything that does not hold, then give a corrected version."

**When:** for anything consequential. After Task, this is the single biggest lever on quality. It only works once the model has done the work. See "Order matters" below.

### 07 · Output

**What:** the form of the answer: structure, tone, length, format.

**Why:** it does not change whether the answer is right, but it removes variance in how the answer arrives, and it makes the result usable and comparable.

**Template:** "Give the answer as [a table with columns X and Y / three short paragraphs / a checklist], in [tone], under [length]."

**When:** whenever the form matters, which is most of the time for work you will reuse.

---

## The three that earn their keep

In everyday use with tools like Copilot, three parts carry most of the value: **Task, Verification, and Output**. Say precisely what you want and why, make the model check its own work, and fix the form of the answer. The other four are there for when the stakes call for them.

If you remember nothing else: a clear task stops the model guessing, verification catches what the first pass missed, and a fixed output saves you reformatting by hand.

---

## Order matters

The seven parts are not a block to paste in one go. Because you work with the model in turns, they unfold in a natural order.

The **Task** comes first, because it defines the work. **Role, Inputs, Steps, and Constraints** scope it. Then the model does the work. **Verification** comes after the work and before you rely on it, because there is nothing to check until the analysis exists. Asking the model to verify on the opening turn, before it has done anything, checks nothing. **Output** shapes what you keep.

In practice this means your first prompt sets the task and scope, and your follow-on prompts are steers:

- "Now check that against the source and correct anything unsupported."
- "Tighten it so it stays within our policy."
- "Give me the final version as a table."

This is how you direct the model in real time, one part at a time.

---

## Worked example

**Bare prompt:**

> Summarise this policy.

You get a generic summary of unknown length, with no guarantee it reflects the document.

**Structured, first turn (Role + Task + Inputs + Output):**

> Act as a compliance analyst. Summarise the policy below so a new team member can follow it on their first day. Use only the text provided and do not add outside rules. Give it as five short bullet points, in plain language, under 150 words.

**Follow-on steer (Verification):**

> Before we finalise, check your summary against the policy text. List any point that is not directly supported, or any obligation you left out, then give a corrected version.

**Follow-on steer (Output reshape):**

> Now turn each point into a one-line action addressed to the new team member.

Each turn adds one part. You did not need all seven, and you added Verification only because the summary will be relied on.

---

## Quick reference

| # | Part | One-line cue |
|---|------|--------------|
| 01 | Role | "Act as a [role] who ..." |
| 02 | Task | "[Verb] [object] so that [purpose]." |
| 03 | Inputs | "Use only [source]. Do not add outside information." |
| 04 | Steps | "Work in this order: first ..., then ..." |
| 05 | Constraints | "Must ... Never ... Stay within ..." |
| 06 | Verification | "Check your draft against [source]. List what fails, then correct it." |
| 07 | Output | "Give it as [format], in [tone], under [length]." |

---

## Common mistakes

- **Dumping all seven on a simple ask.** Match the structure to the stakes. Most prompts need only two or three parts.
- **Asking for verification too early.** Verify after the model has done the work, not on the opening turn.
- **A vague task.** If the model guesses what you wanted, the task was not clear enough.
- **Over-constraining an exploratory ask.** For brainstorming or drafting, too many constraints flatten the result.
- **Forgetting Output, then reformatting by hand.** Decide the form up front when you will reuse the answer.

---

## Where it comes from

This method is the human, reduced form of the iGentic specification, a way of directing capable models set out in the thesis *Directing capable models through real work*. An autonomous agent receives a full Work Plan up front, because it runs unattended. A person uses these seven parts selectively, because they stay in the loop to judge and steer.

The full specification adds the parts an unattended runtime needs, a closed vocabulary, tool definitions, and error handling, which a person supplies by judgement as they go. The principle is the same in both: a capable model does its best work when its attention is shaped, not when it is caged or left wide open.
