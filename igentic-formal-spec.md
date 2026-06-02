# The iGentic specification

*A declarative language for agent Work Plans.*

## Summary

- *iGentic is a declarative language for Work Plans. A Work Plan is one document a domain expert can author and read that directs a capable model through a task.*
- *A Work Plan has up to eleven elements. Four are required, Role, Framing, Task, and Process. The rest are added only as the work demands.*
- *Each element targets one source of uncertainty. Role sets the stance, Domain closes the vocabulary, Process fixes the order of decisions, Rules state the boundaries, and so on. The plan shapes the model's attention rather than scripting its every move.*
- *The language is notation-light and meant to be read by the person who owns the work, not only by an engineer.*
- *Determinism is allocated by the author, decision by decision. Where a decision needs a guarantee, the plan marks a hard check, and the check, not the model, is what enforces it.*
- *We are careful about scope. A Work Plan focuses a model; it does not by itself make the model trustworthy, and how well a given plan focuses a model is an empirical question, to be measured, not asserted.*

---

## What iGentic is

iGentic is a declarative language for Work Plans. A Work Plan is a single document that directs a capable model through a piece of real work, a support conversation, a document review, a batch of records, a multi-step decision. It is declarative: it describes the work and its boundaries, not the control code that runs it. The runtime that executes a Work Plan is a thin harness around a capable model, and the language is written to be read by the domain expert who owns the work, not only by the engineer who wires it up.

The purpose of the language is to focus a model's attention. A capable model, left with an open instruction, chooses its next move from a wide field of options, and a wide field is what surfaces as drift and off-target answers. Each element of a Work Plan narrows that field at one specific point. The plan does not cage the model; it keeps the model's judgement where judgement is wanted and removes the rest of the noise.

Determinism is something the author sets, not a property the system has. Most of a Work Plan is judgement, shaped by the plan rather than scripted by it. A few decisions need a guarantee, and the plan marks those as hard checks. The guarantee then comes from the check, a deterministic test, a tool call, or a human, not from the model's good intentions.

### Design principles

We hold the language to five principles.

It is **human readable**, so a business owner can review a Work Plan and understand what the system will do. It is **model executable**, providing the structure a capable model needs to stay focused. It is **context aware**, structured to keep the model's working context tight rather than sprawling. It is **domain agnostic**, applicable to support, operations, finance, compliance, and beyond. And it is **unambiguous**: one symbol has one purpose, and execution is explicit rather than implied.

### Lineage

iGentic draws on established process-modelling standards and adapts them for a model rather than an engine.

| iGentic | BPMN | UML activity diagram |
|---------|------|----------------------|
| Work Plan | Process | Activity diagram |
| Process step | Task | Action |
| Decision (?) | Gateway | Decision node |
| Data | Data object | Object node |
| Foreach | Loop activity | Loop node |

---

## The eleven elements

A Work Plan is built from up to eleven elements. Four are required; the rest are added only when the work calls for them. Adding elements a task does not need is its own kind of noise.

| Element | Required | Purpose |
|---------|----------|---------|
| Role | Yes | Identity, authority, lens |
| Framing | Yes | The objective and what is at stake |
| Task | Yes | The specific objective for this run |
| Domain | No | Categories, taxonomies, closed vocabularies |
| Tools | No | Capabilities, with guidance on when to use them |
| Data | No | Named information containers, with scope |
| Process | Yes | Steps, decisions, loops, and sequence |
| Rules | No | Hard constraints (must, only, never) |
| Guardrails | No | Soft, conditional boundaries |
| Error | No | How tool and system failures are handled |
| Output | No | The shape of the result |

The sections that follow describe each element: what it is for, how to write it, and a short example. The guiding idea is constant. Each element aims the model at one source of uncertainty, and an element you do not need is an element you should leave out.

---

## The elements, one by one

### Role

Role establishes who the model is, what authority it holds, and the lens it should reason through. It is the cheapest way to set vocabulary, depth, and default assumptions for everything that follows.

Keep it to one or two sentences. Name the agent, say what it is, and say who it works for.

```
ROLE
You are the Triage Agent for Northwind.
You triage inbound support tickets and route them to the right team.
```

### Framing

Framing gives the objective and the stakes: why this agent exists, what problem it solves, and which mistake is most costly. The stakes matter because they steer the model's judgement later. A plan that says which error is worse gives the model a basis for the calls the author did not spell out.

Focus on business impact rather than mechanism, and quantify where you can.

```
FRAMING
Northwind receives a high volume of support tickets, and unrouted tickets
sit too long while customers wait. A wrong route costs more than a brief
delay, because it sends the customer down the wrong path. Your job is to
classify each ticket and route it, or escalate to a human when the call is
not clear.
```

### Task

Task is the single objective for this run: the action and its purpose. One sentence, verb first, with the possible outcomes named. It is the highest-leverage element, because a vague task leaves the field wide and the model fills the gap with a guess.

```
TASK
Triage this ticket and either route it to the right team or escalate it to a human.
```

### Domain

Domain closes the vocabulary. It lists the categories, taxonomies, and statuses the model is allowed to use, so that classification stops being open-ended and becomes a choice from a fixed set. Closing the vocabulary is the strongest move toward determinism that does not require an enforced check: an open judgement becomes a bounded match.

Use snake_case names and pipe-separated values, and keep related categories together. These values become the vocabulary the Process refers to.

```
DOMAIN
category: billing | technical | account-access | general
priority: URGENT | HIGH | NORMAL | LOW
routed_team: billing_team | technical_team | account_team | general_queue
```

### Tools

Tools declares the capabilities the model can call, with guidance on when and why to use each. The model receives the formal signatures from the runtime; the plan supplies the judgement about timing.

Prefix each tool with `@`, give its parameters and return shape, and state when to use it, when to skip it, and when never to use it.

```
TOOLS
@lookupCustomer(customer_id) → {success, data: customer, error}
  USE: at the start of every ticket, to load account context
  SKIP: when no customer id is present

@createTicket(customer_id, category, priority, summary) → {success, data: ticket_id, error}
  USE: once the ticket is classified and ready to route
  NEVER: before a category has been assigned
```

Every tool returns the same envelope, so the plan can branch on success or failure consistently:

```
{ "success": true | false, "data": <response>, "error": { "code": "...", "message": "..." } }
```

### Data

Data names the containers that information flows through, and tags each with its lifecycle and scope. It makes the inputs, the things fetched, the things derived, and the outputs explicit, so the Process can refer to them by name.

```
DATA
input:   [ticket] customer_id, subject, body, channel
fetch:   [customer] account, plan, open_tickets
derive:  [classification] category, priority
         [summary] short description of the issue
persist: [triage_history]@customer past categories and outcomes
output:  [outcome] ROUTED | ESCALATED | NEEDS_INFO
```

The lifecycle tags carry scope. `input` arrives with the request. `fetch` is retrieved through a tool. `derive` is calculated during the run. `persist` survives across runs and takes a scope suffix, `@customer`, `@account`, or `@tenant`, that says how widely the data is shared and how long it lives. `output` is what the run returns or logs. List containers append atomically; scalar containers are last-write-wins.

### Process

Process is the sequence: numbered steps, decisions, loops, and branches. It replaces "decide what to do" with "you are at step four, and these are the branches." It is covered in full in the next section.

### Rules

Rules are the hard constraints, each prefixed with `MUST`, `ONLY`, or `NEVER`. `MUST` is required and non-negotiable. `ONLY` permits something under stated conditions and is otherwise restricted. `NEVER` is prohibited in all cases. Keep each rule to a line, and group related rules.

```
RULES
MUST: assign a category before creating a ticket
ONLY: auto-route tickets in the billing, technical, or general categories
NEVER: auto-resolve or auto-route account-access or security tickets, always escalate
```

Rules are enforced through `VALIDATE RULES` in the Process. A `MUST` or `NEVER` breach is an error and blocks proceeding; an `ONLY` breach is a warning that is logged but allowed to continue.

### Guardrails

Guardrails are the soft, conditional boundaries that guide behaviour without the hard stop of a Rule. Where Rules are binary and validated explicitly, Guardrails are observed throughout the run. They read as `If`, `When`, and `Limit` lines, and they often carry their reason.

```
GUARDRAILS
If a ticket cannot be confidently categorised after one pass: escalate rather than guess
When a ticket signals churn risk: raise priority one level
Limit clarification requests to two, then escalate
```

The line between the two is simple. Use a Rule for an absolute the system must never cross and that you want validated. Use a Guardrail for situational guidance that improves quality and handles edge cases. A Rule says what you must or must not do; a Guardrail says how to behave well.

### Error

Error defines how tool and system failures are handled, so a single failure does not abort the whole run. Each handler names the failure and the recovery, and sets the flow with `CONTINUE`, `ABORT`, `RETRY N`, or a jump.

```
ERROR
@lookupCustomer failure:
  Log the failure
  RETRY 2
  ? still_failing
    Y: continue without account context
       CONTINUE

@createTicket failure:
  Log to [failed_records]
  CONTINUE
```

In a loop, `CONTINUE` skips the failed item, `ABORT` exits the loop, and `RETRY N` retries the current item before giving up. For batch work, track successes and failures in a Data container so the Output can report them.

### Output

Output defines the shape of the result: its format, who can see it, and the fields it carries. Fixing the form does not change whether the answer is right, but it removes variance in how the answer arrives and makes the result usable and comparable.

```
OUTPUT
Triage record:
  Format: JSON
  Visibility: internal

  category:    [classification].category
  priority:    [classification].priority
  routedTeam:  [routed_team]
  outcome:     [outcome]
```

Distinguish external output, which a customer sees, from internal logging. Use `[container]` references for structured fields, and `{{interpolation}}` for values dropped into external messages.

---

## Process in depth

Process carries the control flow, so it has the most syntax. The aim is to make the order of decisions explicit, so the run can be watched against the plan, step by step.

### Steps and decisions

Number the steps. Mark a decision with `?`, and indent its branches beneath it.

```
? condition
  Y: action if true
  N: action if false
```

A decision can also branch on a value, in which case it lists the cases and a default. The default, written `*:`, is required unless every possible value is handled.

```
? [ticket].category
  billing:   SET [routed_team] = "billing_team"
  technical: SET [routed_team] = "technical_team"
  general:   SET [routed_team] = "general_queue"
  *: GOTO step 8   # unexpected value, escalate to a human
```

### Flow control

Explicit keywords carry the flow, so nothing is left to inference.

| Keyword | Purpose |
|---------|---------|
| `GOTO step N` | Jump to a numbered step |
| `SET [x] = value` | Assign data |
| `SET [x] = @tool(...)` | Capture a tool result |
| `END` | Terminate the run |
| `FOREACH [x] IN [y] ... ENDFOR` | Loop over a collection |
| `BREAK` | Exit the current loop |
| `CONTINUE` | Skip to the next iteration |

A jump may only target a valid numbered step. Keep jumps out of loops; use `BREAK` and `CONTINUE` to move within a loop, and `FOREACH` to enter one. A backward jump without an exit condition is an infinite loop, so guard it.

### Loops

Iterate with `FOREACH`, and close every loop with a matching `ENDFOR`. Loops may nest up to three levels for readability, and an inner loop variable shadows an outer one of the same name.

```
FOREACH [invoice] IN [batch].invoices
  SET [result] = @parse_invoice([invoice])
  ? [result].success
    N: CONTINUE   # skip a malformed invoice
  SET [outcome] = @file_invoice([invoice], [result])
ENDFOR
```

### The review step

`VALIDATE` is the review the plan performs on the model's own work, before the output. A model on its own has no standard for "good enough," so it hands over a first pass and stops. `VALIDATE` writes the check in: it tells the model what to re-read, from what angle, which gaps to look for, and how to fill them. The author's standard becomes the model's self-review, which is the difference between a draft and a reviewed draft.

`VALIDATE RULES` is the specific form that checks the Rules and returns a list of violations the Process can branch on.

```
PROCESS
5. Validate before routing
   VALIDATE RULES
   SET [violations] = result
   ? [violations].any
     Y: ? [violations].has_errors
          Y: GOTO step 8   # a blocking breach, escalate
          N: log warnings, continue
     N: continue
```

Be clear about what this is. It is self-review, not independent assurance. The same model is doing the checking, so it can miss the same way twice. It raises the floor; it does not certify the ceiling. Where independence is required, run the review as a separate plan, on a different model, or by a human, and say so in the plan.

---

## A worked example

This Work Plan triages a support ticket. It shows a closed Domain, a hard gate that removes a category from the model's discretion, rule validation, error handling, and data that persists across runs.

```
ROLE
You are the Triage Agent for Northwind.
You triage inbound support tickets and route them to the right team.

FRAMING
Northwind receives a high volume of support tickets. Unrouted tickets sit too
long, and a wrong route costs more than a brief delay. Your job is to classify
each ticket, assess its priority, and route it or escalate it to a human.

TASK
Triage this ticket and either route it to the right team or escalate it to a human.

DOMAIN
category: billing | technical | account-access | general
priority: URGENT | HIGH | NORMAL | LOW
routed_team: billing_team | technical_team | account_team | general_queue
status: ROUTED | ESCALATED | NEEDS_INFO

TOOLS
@lookupCustomer(customer_id) → {success, data: customer, error}
  USE: at the start of every ticket, to load account context

@createTicket(customer_id, category, priority, summary) → {success, data: ticket_id, error}
  USE: once the ticket is classified
  NEVER: before a category has been assigned

DATA
input:   [ticket] customer_id, subject, body, channel
fetch:   [customer] account, plan, open_tickets
derive:  [classification] category, priority
         [summary] short description of the issue
persist: [triage_history]@customer past categories and outcomes
output:  [outcome] ROUTED | ESCALATED | NEEDS_INFO

PROCESS
1. Initialize
   SET [customer] = @lookupCustomer([ticket].customer_id)
   ? [customer].success
     Y: FETCH [triage_history] FROM persist WHERE customer_id = [ticket].customer_id
     N: # the ERROR handler will manage this

2. Classify
   Read [ticket].subject and [ticket].body
   SET [classification].category = one of billing | technical | account-access | general
   SET [classification].priority = assess urgency from impact and language
   SET [summary] = one-line description

3. Apply the hard gate
   ? [classification].category = "account-access"
     Y: GOTO step 8   # account-access is never auto-routed
     N: CONTINUE

4. Validate before routing
   VALIDATE RULES
   SET [violations] = result
   ? [violations].any
     Y: ? [violations].has_errors
          Y: GOTO step 8
          N: log warnings, continue
     N: continue

5. Route by category
   ? [classification].category
     billing:   SET [routed_team] = "billing_team"
     technical: SET [routed_team] = "technical_team"
     general:   SET [routed_team] = "general_queue"
     *: GOTO step 8

6. Create the ticket
   SET [created] = @createTicket([ticket].customer_id, [classification].category, [classification].priority, [summary])
   ? [created].success
     Y: SET [outcome] = "ROUTED"
        GOTO step 9
     N: # the ERROR handler will manage this

8. Escalate to a human
   SET [routed_team] = "account_team"
   SET [outcome] = "ESCALATED"

9. Finalize
   Append [triage_history] with this outcome
   PERSIST [triage_history]
   END

RULES
MUST: assign a category before creating a ticket
ONLY: auto-route tickets in the billing, technical, or general categories
NEVER: auto-resolve or auto-route account-access or security tickets, always escalate

GUARDRAILS
If the ticket body is empty or unintelligible: set outcome to NEEDS_INFO and escalate
If the same customer has three or more open tickets in one category: raise priority one level
When classification confidence is low: prefer general and a human review over a confident wrong route

ERROR
@lookupCustomer failure:
  RETRY 2
  ? still_failing
    Y: continue without account context
       CONTINUE

@createTicket failure:
  RETRY 2
  ? still_failing
    Y: queue for manual entry
       SET [outcome] = "NEEDS_INFO"
       GOTO step 9

OUTPUT
Triage record:
  Format: JSON
  Visibility: internal

  category:    [classification].category
  priority:    [classification].priority
  routedTeam:  [routed_team]
  outcome:     [outcome]
  ticket_id:   [created].data.ticket_id
```

For batch work, the same elements carry a loop. The pattern is to iterate, skip failures rather than abort, and report the totals:

```
PROCESS
1. Process invoices
   SET [results] = { succeeded: 0, failed: 0, failed_ids: [] }
   FOREACH [invoice] IN [batch].invoices
     SET [r] = @classify_invoice([invoice])
     ? [r].error
       Y: append [results].failed_ids with [invoice].id
          SET [results].failed = [results].failed + 1
          CONTINUE
       N: SET [results].succeeded = [results].succeeded + 1
   ENDFOR
   END

ERROR
@classify_invoice timeout:
  Log and CONTINUE   # skip this invoice, do not abort the batch
@classify_invoice rate_limited:
  Wait 60 seconds
  RETRY 1
  ? still_failing
    Y: ABORT
```

---

## Syntax reference

### Symbols

| Symbol | Meaning |
|--------|---------|
| `@` | Tool invocation, `@lookupCustomer(id)` |
| `[ ]` | Data container, `[ticket]` |
| `?` | Decision point |
| `Y:` / `N:` | Decision branches |
| `*:` | Default case in a value decision |
| `\|` | Alternatives in a Domain list |
| `{{ }}` | String interpolation in external messages |
| `[x].field` | Field access on a container |
| `@scope` | Persistence scope, `[history]@customer` |

### Keywords

| Keyword | Purpose |
|---------|---------|
| `GOTO step N` | Jump to a step |
| `SET [x] = value` | Assign data |
| `END` | Terminate the run |
| `FOREACH ... ENDFOR` | Loop |
| `BREAK` / `CONTINUE` | Exit a loop / next iteration |
| `VALIDATE RULES` | Check the Rules |
| `FETCH [x] FROM persist` | Retrieve persisted data |
| `PERSIST [x]` | Save persisted data |
| `RETRY N` / `ABORT` | Error flow control |

### Prefixes

| Prefix | Used in | Meaning |
|--------|---------|---------|
| `MUST:` | Rules | Required (error if breached) |
| `ONLY:` | Rules | Restricted condition (warning if breached) |
| `NEVER:` | Rules | Prohibited (error if breached) |
| `USE:` / `SKIP:` / `NEVER:` | Tools | When to call a tool, and when not to |

### Data lifecycle

| Tag | Meaning | Scope |
|-----|---------|-------|
| `input:` | Arrives with the request | Run |
| `fetch:` | Retrieved through a tool | Run |
| `derive:` | Calculated during the run | Run |
| `persist:` | Survives across runs | `@customer`, `@account`, or `@tenant` |
| `output:` | Returned or logged | Run |

---

## Terminology

| Term | Definition |
|------|------------|
| Work Plan | A complete iGentic specification for one agent |
| Agent | A capable model executing a Work Plan |
| Data container | A named variable, written in `[brackets]` |
| Tool | An external capability, invoked with `@` |
| Run | A single execution of a Work Plan |
| Persistence | Data that survives across runs, with an `@scope` suffix |
| Violation | A Rules breach detected by `VALIDATE RULES` |

---

## What the specification does not do

A specification is most useful when it is honest about its edges.

A Work Plan focuses a model; it does not by itself make the model trustworthy. The trust is in the design and in the checks the plan places, not in the model. Nor does the document enforce its own Rules. Rules are honoured by the model and validated where the Process calls `VALIDATE RULES`, but where a constraint must truly hold, the guarantee is a deterministic check at a gate, and the check, not the plan, is what holds.

A plan can also be confidently wrong. The structure focuses the model whether the plan is right or not, so a poor Work Plan does not fail loudly; it fails toward a wrong answer with conviction. The value is in boundaries that are correct, set by someone who knows the domain.

Finally, how well a given plan focuses a given model is an empirical question. It depends on the plan and on the model, it improves as models improve, and it is something to measure, not to assert.
