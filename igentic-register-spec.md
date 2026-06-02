# iGentic in two registers

*The same Work Plan, written in symbols or in prose.*

## Summary

- *iGentic has two registers. The same eleven elements can be written in a formal notation or in plain prose, and a capable model runs either.*
- *A register is a level of formality, not a different language. Which one to use is a question about the author and the reader, not about what the model can do.*
- *The formal register is compact and close to code. The prose register is narrative and carries its reasons with it. Many real plans mix the two.*
- *The prose register has conventions of its own: the reason travels with the rule, Domain can be a closed reference, Process reads as named phases, evidence is tiered by how firm it is, scope is stated, and the review becomes an active audit pass.*
- *Enforcement is identical in both registers. The notation is never the guarantee. A check behind a gate is.*

---

## Two registers, one language

The formal specification defines the eleven elements of a Work Plan and a notation for writing them: `@tools`, `[containers]`, decisions, and jumps. That notation is precise, but it is not the language. The language is the structure the notation expresses, and a capable model follows that structure whether it is written in symbols or in plain sentences, because the model was never parsing syntax. So the same Work Plan has two registers: two levels of formality that describe the same elements and produce the same behaviour.

The formal register is the notation above. It is compact, unambiguous, and close to code, and it is best when the author is technical and the logic is mechanical. The prose register writes the same elements as structured narrative: steps become phases, taxonomies become described categories, and a rule can carry the reason it exists. It is best when the author is a domain expert and the logic carries judgement that needs explaining.

Neither register is more advanced than the other. A simple routing job is clearest in formal notation. A judgement-heavy audit is clearest in prose. The test is who reads the plan to decide whether to trust it, and what they need to see. If a regulator must read a rule and understand why it exists, write in prose. If an engineer must wire the plan into a runtime and wants no ambiguity, write formally.

## Choosing a register

| Consideration | Lean formal | Lean prose |
|---------------|-------------|------------|
| Author | Engineer, technical PM | Domain expert, analyst, compliance officer |
| Reviewer | The same engineer | An auditor who must read the logic |
| Logic | Mechanical: route, assign, threshold | Judgement: classify, weigh, interpret |
| Why it matters | The reason is obvious | The reason needs to travel with the rule |
| Branching | Many explicit jumps and loops | A few phases, each with internal judgement |
| Output | A structured record for a system | Findings or prose a person will read |

---

## The elements, written both ways

The eleven elements are the same in either register. The formal specification carries their full definitions; here we show the contrast on a few representative elements. The rest follow the same pattern.

**Framing.** The formal register states the objective plainly. The prose register goes further and names the stakes, because that judgement steers the model later.

```
Formal:
FRAMING
Northwind receives a high volume of tickets. Unrouted tickets sit too long.
Classify each ticket and route it, or escalate to a human.
```

> Prose:
> Northwind receives thousands of tickets a day, and an unrouted ticket sits idle while a customer waits. Speed matters, but a confident wrong route costs more than a brief delay, because it sends the customer down the wrong path. When the category is genuinely unclear, prefer a human over a guess.

**Domain.** The formal register closes a vocabulary with pipe-separated values. The prose register can close a richer one, a described set, a lookup, or a decision tree walked in order, while keeping the same discipline: an open classification becomes a bounded match.

```
Formal:
DOMAIN
category: billing | technical | account-access | general
```

> Prose:
> Every ticket resolves to exactly one category. Billing covers charges, invoices, and refunds. Technical covers errors and outages. Account-access covers login and identity, and is treated as sensitive: see the hard gate in Process. General is anything that does not clearly fit the first three; when in doubt between general and a specific category on weak signal, choose general.

**Process.** The formal register uses numbered steps and explicit jumps. The prose register uses named phases, each a short paragraph that states the judgement to make and its place in the order.

```
Formal:
3. Apply the hard gate
   ? [category] = "account-access"
     Y: GOTO step 8   # always escalate
     N: CONTINUE
```

> Prose:
> Phase 3, the hard gate. Before any routing, check the category. Account-access and security tickets are never auto-routed and never auto-resolved; they go to a human every time, regardless of confidence. Apply this gate before the routing in Phase 4, not after.

**Rules.** Both registers use the `MUST`, `ONLY`, `NEVER` prefixes. The prose register's one addition is that a rule may carry its reason on the same line.

```
Formal:
NEVER: auto-route account-access or security tickets, always escalate
```

> Prose:
> Never auto-route account-access or security tickets. An identity mistake is the most expensive error this agent can make, so the call always goes to a human, even when the classifier is certain.

---

## Conventions of the prose register

These conventions are optional, and they formalise the patterns that mature prose Work Plans converge on. None of them changes the eleven elements; they are ways of writing them.

**The reason travels with the rule.** A rule may state why it exists, not only what it forbids. "Never flag on X alone, because X alone over-flags and erodes trust" holds at the boundary better than "Never flag on X alone." A capable model uses the reason to handle the cases the author never enumerated. This is the highest-value prose convention.

**Domain can be a closed reference.** Prose can close a richer vocabulary than a pipe-separated list: a lookup table, a mapping of inputs to approved outcomes, a decision tree walked in order. Closing the vocabulary is the strongest move toward determinism short of a gate, in either register, so reach for it wherever a classification has a knowable answer set.

**Process reads as phases.** Long procedures read better as a handful of named phases than as a long ladder of numbered steps. State ordering constraints explicitly, "apply the exclusion before emitting," "walk the tree before deciding," because cross-phase ordering is where a model is most likely to slip.

**Evidence is tiered.** When a plan draws on sources of differing reliability, label each check by how firm its ground is, and fix the phrasing to the tier. A common scheme: Tier A is directly checkable, a structured field or a timestamp, phrased as fact; Tier B is inferred from free text, phrased as inference; Tier C is out of scope and never emitted. Tiering calibrates how confident the output is allowed to sound to the quality of the evidence behind it.

**Scope is stated.** A prose plan should say what it does not do and who does it instead: "general completeness is delegated to the Assessment plan; this plan checks only the restraint-specific fields." Explicit delegation is what lets many Work Plans compose into an organisation while each stays legible, and it prevents two plans from emitting the same finding twice.

**The review is an audit pass.** The formal register's `VALIDATE RULES` has a prose counterpart: an Audit pass the model performs on its own draft before emitting, framed as active correction rather than a checklist. A useful Audit has three passes: gap-fill ("which applicable check did I skip?"), hallucination ("does every claim trace to fetched data? if not, remove it"), and consistency ("are there duplicate or contradictory findings? reconcile to source"). It carries the same honest limit as any self-review: it raises the floor but does not certify the ceiling, so where independence is required, the plan routes the review elsewhere and says so.

**A conservative default, and the human gate.** Where a determination is high-stakes and genuinely ambiguous, the safest enforced gate is a human. State the bias once, plainly, "when in doubt, do not flag," and let it govern the plan. The model marks the case unclear and hands it up rather than forcing a confident answer it cannot justify. This is determinism allocated to a human at exactly the point where neither accuracy nor the model's confidence can be proven.

---

## Determinism is the same in both registers

Determinism is allocated by the author, and a guarantee comes from an enforced check, not the model's good intentions. That holds identically in both registers.

The formal register makes a hard gate visually obvious: a decision that jumps to escalation, reinforced by a `NEVER` rule that `VALIDATE RULES` enforces. The prose register makes the same gate with a named phase and a reasoned never. Neither the symbols nor the sentences are themselves the guarantee. The guarantee is whatever the gate calls: a deterministic check, a tool, or a human. Choosing prose does not soften a gate, and choosing formal does not harden one. The enforcement lives below the plan, in either case.

## Mixing registers

The registers are not exclusive within a plan. The common pattern for complex work is prose throughout, with formal precision dropped in exactly where it earns its place: a closed Domain table, because an enumerable answer set deserves to be exact; a hard numeric threshold stated as a formal condition, because "over 500" must not be paraphrased; a formal tool signature for a call whose parameters matter. Mix deliberately. Use the formal register for the parts that must not drift, and prose for the parts that carry judgement and need their reasons.

## When to use which

Write formally when the logic is mechanical and the reader is technical. Write in prose when the logic carries judgement and the reader must understand why. Mix the two when a mostly-judgement plan has a few places that must not drift. A capable model runs all three.
