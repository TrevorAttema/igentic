# Directing capable models through real work

May 2026

## Summary

- *Most AI projects on real, human-facing work do not fall short because the model is too weak. They fall short because of a single confusion: the word "reliable" runs together two different demands, accuracy (is the answer right) and determinism (does it come back the same way every time), and a reasoning model meets them separately. Holding a reasoning tool to a calculator's standard is the root mistake.*
- *Drifting off task is not the model failing; it is the model left to focus on everything at once. The fix is to shape the model's attention with a plan rather than cage it, which keeps its judgement, its empathy, and its read of a person in real time, exactly where the work needs them.*
- *iGentic is that plan: one legible document a domain expert can author and read. It points a capable model at the decisions that matter, and the run can be checked against the plan, step by step, as it happens.*
- *Determinism is a dial set against the stakes, not a property a system has. Most work stays judgement; narrowing the options firms the middle; and a hard gate, enforced by a deterministic check, a tool, or a human, is reserved for the few decisions that need a guarantee. The guarantee comes from the gate, not from the model.*
- *The plan is portable: it runs on any capable model through a thin, swappable harness, and because what carries is the structure rather than the notation, it can be written in symbols or in plain prose. The same discipline composes upward, from a single agent to an organisation of plans.*
- *The same method works without building anything. A person prompting a chat assistant or a coding copilot can apply a reduced, seven-part form of the grammar by hand, choosing the parts the stakes call for. That makes structured prompting a skill a domain expert can use in real time, not only a way to build agents.*
- *We are honest about the limits. iGentic does not make a model trustworthy; the trust is in the design. A plan can be confidently wrong, so it is only as good as the expertise written into it, and how well it focuses a model is an empirical question, to be measured, not asserted.*

---

## Why capable models disappoint on real work

Most AI projects that disappoint on real, human-facing work do not disappoint because the model is too weak. They disappoint because of a single confusion, and it is worth naming precisely. Under one word, *reliable*, we run two different demands together. One is accuracy: is the answer right? The other is determinism: does the same input return the same answer every time? For forty years, software met both for free, so the two fused, and we stopped noticing they were ever distinct. A reasoning model meets neither for free. It is the first tool we have been handed that reasons rather than computes, and the common mistake is to hold a reasoning tool to the standard of a calculator.

The edges of the confusion are easy to see. A spreadsheet adds ten numbers and returns the same total every time, instantly, at no cost. Make a model *be* that spreadsheet and you pay by the token for a weaker guarantee. But ask the spreadsheet to calm a customer who is about to walk, and it cannot, where the model can. Two jobs, two tools. The error is using the model for the spreadsheet's job, or demanding the spreadsheet's guarantee from the model.

This is not a new problem, and we already know how to manage it. We have run organisations on non-deterministic agents for as long as there has been work: people. We never ask a colleague for a bit-identical answer twice. We build graded controls instead, review, sign-off, escalation, a hard check where the stakes are high. We expect an answer; we do not expect a particular one. Determinism, in other words, was always set by the stakes, decision by decision. We never had to say so aloud, because the deterministic machine sat in its own box on the desk. A model puts the reasoning agent inside the software for the first time, and the discipline has to come in with it.

That discipline is the subject of this piece, and it is the difference between a model that demos and a model that deploys. It is not a new trust in the model. It is a single document a domain expert can author and read, one that points a capable model at the few decisions that matter, places a hard check where a decision needs a guarantee, and leaves a trace that can be held against the plan, line by line. It runs on any capable model through a thin harness that can be swapped. The harness changes; the plan is what lasts. The rest of this piece sets out how it works, where the guarantees come from, and where they do not.

## Determinism is a dial, not a property

Determinism is not something a system has. It is a level we set. The field tends to offer a false choice: a deterministic system that runs as code, which is rigid, or a free-form prompt that runs on hope, which drifts. Pick your failure. But the choice was never binary. Even a model is partly deterministic, in that we expect it to reason and converge; even a deterministic system has fuzz at its edges. Determinism is a dial, and most tools in the field are welded to a single point on it.

iGentic lets the dial be set decision by decision, against the stakes: low where the work is judgement, hard over to an enforced check where a decision must be guaranteed. Most of the dial, though, is the middle. Determinism can be raised without an enforced check at all, by closing the vocabulary: give the model a fixed set of answers to choose among, and an open judgement becomes a bounded match. This is the strongest move available short of a gate, and it is where most real plans spend their time.

## Drift is attention, not failure

When a capable model drifts, the drift is usually misread as the model failing. It is better understood as the model left to focus on everything at once. At every step the model chooses what to do next from a field of options, and left open, that field is wide. A wide field is what surfaces as drift, invented branches, and choices that look random.

The useful frame is attention, in the ordinary sense: what we put in front of the model and what we keep out of its way. This is not the architecture's attention weights; it is the everyday meaning of the word. A capable model is far better than the tools built to babysit it tend to assume, but it still loses the thread in a long, unstructured context. That is not a reason to distrust it. It is the reason to give it a structured plan rather than a wall of instructions. We condition the model not by caging it, and not by waiting for a better one, but by pointing it at the decisions that matter and keeping the rest out of its way.

## The plan is the mechanism

The mechanism is the plan itself. A Work Plan is a domain expert's judgement written down as instructions a model can follow. The grammar is small, and each block aims the model at one specific source of uncertainty. ROLE sets the stance. DOMAIN closes the vocabulary, so classification stops being open-ended. PROCESS replaces "decide what to do" with "you are at step four, and these are the branches." RULES state the boundaries. Together they narrow the decisions while keeping the language, the empathy, and the real-time read of a person, which is the part that made a model the right tool in the first place.

Two things about the grammar are easy to miss. First, a boundary can carry its reason. A plan need not only say where a line sits; it can say why, and a model told why holds the line better at the edges the author never enumerated. The reason is not commentary. It is part of what focuses the model, and it compounds with capability, since a stronger model uses the reason better. Second, the grammar is the structure, not the symbols. The same plan reads the same to a capable model whether it is written in terse notation or plain prose, because the model was never parsing syntax; it was following the structure the syntax expressed. That is what lets a domain expert author a plan in the language they already think in, and it is part of why the plan stays legible to the person who has to trust it.

A natural objection is that this is just a state machine. It is not. A state machine fixes the transitions, and the model follows the rail or breaks. iGentic fixes the landscape and lets the model cross it with judgement: adaptive within the bounds, not locked to a rail.

One distinction matters for honesty. The shape of the output, the fields and the tool signatures, is already guaranteed by the model itself; that floor is free. What iGentic shapes is the focus of the contents inside that guaranteed shape. Shape belongs to the platform; focus belongs to the plan. And how well a plan focuses a model is an empirical question, one to be measured rather than asserted.

## Legible before the run, observable during it

Two properties follow from an authored plan, and they operate at different times. Legibility is static: a human reads the document before anything runs, the way a reviewer reads a procedure to know what the system will do. Observability is live: because the plan fixes the order of the steps and the shape of each, the run can be watched and held against the plan, step by step.

Plenty of tools log what a model did, and that is cheap and common. The difference here is that there is an authored plan to diff the run against, the expectation and not just the record. A log alone tells you what happened. A log set beside the plan tells you whether what happened was what you specified.

Legibility reaches one step further, into how firmly the model is allowed to speak. A plan can require the model to mark how solid its ground is: a structured fact stated as fact, an inference stated as inference. The model still reasons freely; what the plan fixes is the confidence it is permitted to project. A reader then sees not only what was decided but how firm each part of it is, which is the accuracy half of the opening section made visible. This is useful after the fact. By itself it is not a guarantee before the fact, which is the subject of the next two sections.

## The review is built into the plan

The first of those guarantees is a review the plan performs on the model's own work, before it answers. A model on its own has no standard for "good enough" on a given task, so it does not look; it hands over a first pass and moves on. iGentic writes the check in. A VALIDATE step fires after the work and before the output, telling the model what to re-read, from what angle, which gaps to look for, and how to fill them. The author's standard becomes the model's self-review, which is the difference between a draft and a reviewed draft.

We are careful about what this is. It is self-review, not independent assurance. The same model is doing the checking, so it can miss the same way twice. It raises the floor; it does not certify the ceiling. Where independence is required, the harness can run the review as a separate plan, on a different model, or by a human, and the plan says where that independence is required. It does not pretend a self-check provides it.

## Determinism, allocated to where it is enforced

The second guarantee is determinism placed only where the stakes demand it, and placed in something that actually enforces. A few decisions need a guarantee: money, identity, safety. These are hard gates, and a hard gate gets a deterministic check, a tool call, or a human, not a model asked to be reliable where reliability must be proven. The guarantee comes from the check, not from the model's good intentions. iGentic's job is to specify the whole and mark exactly where those gates belong.

Not every move toward determinism is a gate. Between free judgement and an enforced check sits the quieter move from earlier: closing the answer set, which is firmer without anything to enforce it. The gate is for the cases where even that is not enough. One such gate is worth naming on its own: the model's own uncertainty. When a decision is high-stakes and genuinely ambiguous, the plan can make the model escalate rather than guess, marking the case unclear and handing it to a human instead of forcing a confident answer it cannot stand behind. The human is the enforcement; the escalation is how the plan reaches one.

Everything else is judgement: the conversation, the triage, the handling of a person who is upset. That part is shaped by the plan, not scripted by it. This is the spreadsheet lesson from the opening, and the model has already learned it. When the work turns quantitative, a capable model reaches for code rather than guess the arithmetic; it does not try to be the calculator, it calls one. So the plan is not imposing determinism on a reluctant model. It is naming the lines the model already respects, and making them explicit and enforced.

## The language outlives the engine

It helps to compare iGentic to SQL. SQL is a language, and an engine runs it; iGentic is a language, and a capable model plus a thin harness runs it. The analogy breaks in one place, and the break is in iGentic's favour: SQL is welded to its syntax, and iGentic is not. What travels is the structure, not the notation, so the same plan can be written in terse symbols or in plain prose and a capable model will run either. The language outlives not just the engine but any one way of writing it down.

There is an engine, of course; SQL needs one too. The harness is the small, unglamorous part: it calls the tools, sequences the steps, runs the gate checks, holds state between turns, and coordinates agents. It is not the product, and it is replaceable. The point was never "no engine." The point is that the language outlives the engine. Change the model, change the harness, and the Work Plan, with the expertise written into it, travels. Every competing artefact is welded to its runtime; a Work Plan is not, and that is what makes it referenceable, reviewable, and yours.

We scope this honestly. Portable does not mean identical. Different models resolve the same plan differently, and a plan tuned on one may need light re-validation on another. It runs anywhere capable. It does not behave the same everywhere.

## How iGentic differs from everything adjacent

Set against the adjacent tools, the pattern is that each welds itself to one posture toward the model, while iGentic makes the posture a setting in a document. All of them limit the model's discretion; what differs is where, how, and what each gives up to do it. How much each actually changes a model's behaviour is itself measurable, and a claim worth measuring rather than asserting.

Deterministic DSLs remove the model's discretion almost entirely. At a hard gate that is not a loss; it is the requirement. iGentic does not compete there. It calls the gate and owns the conversation around it. A free-form prompt sits at the other end: it removes nothing, leaving no bounds and nothing authored to read or diff against. Parlant takes a more interesting position, bounding the model by rationing context inside its runtime, which is a real answer to a real problem, since long-context degradation has not gone away. iGentic makes a different bet: keep the plan legible and bounded in one authored document, and let a thin harness keep the context focused. Same problem, different place to put the plan. The contrast is what separates the two approaches, not a verdict on Parlant.

What iGentic holds that the others do not hold together is a single combination: one document a domain expert authors and reads, portable across models, that says where judgement runs and where a guarantee is enforced.

## From one agent to an organisation

The same authoring discipline composes upward, though the execution does not come for free. A Work Plan need not describe only a single agent. A manager plan can hold the strategy and delegate to worker plans, each its own Work Plan, all keyed to the same strategy, with the same grammar at every level: strategy at the top, execution at the leaves.

What composes cleanly is the design, a hierarchy of authored plans a human can still read. What does not come for free is the execution. Coordinating agents adds real failure modes, handoffs, partial failures, and state held across long-running work, and the harness has to handle them the way any distributed system must. So we keep the claim narrow and real: iGentic keeps an organisation's agent work legible and reviewable as it scales. It does not, on its own, make distributed execution reliable. That is the harness's job, and it is hard.

## Directing the model by hand

Up to here we have described a plan handed to an agent that runs it unattended. The same discipline holds when the operator is a person. Someone prompting a chat assistant or a coding copilot is doing by hand what the harness does for an agent: supplying the structure that focuses the model's attention. The difference is that a person supplies it a little at a time, and stays in the loop to judge and redirect.

This gives the specification a second, lighter form, which we teach as a seven-part frame: Role, Task, Inputs, Steps, Constraints, Verification, and Output. It is the same grammar with the parts an autonomous runtime needs set aside, the closed vocabulary, the tool wiring, the error handling, because a person in the loop supplies those by judgement as they go.

It is also selective. An agent receives the whole plan up front, because it cannot ask; a person invokes only the parts the stakes call for, which is the determinism dial from earlier, turned by hand. Recall the calculator. It returns the right answer the same way every time, for nothing, and a model returns neither for free. The frame is how a person buys back a slice of each, accuracy and consistency both, and spends the effort only where the stakes earn it.

Three parts do most of the work, and it is worth saying exactly why.

Task is the action and its purpose: the verb, and the reason for it. It is the highest-leverage part, because a vague task leaves the field of options wide, and the model fills the gap with a guess, which is the drift described earlier. A precise task narrows the field and aims the model at the right target, which is accuracy bought directly. Stating the purpose as well as the action matters for the same reason a rule carries its reason: told why, the model makes better choices on everything the prompt did not spell out.

Verification is the model checking its own work before you rely on it. Left alone, a model has no standard for good enough; it hands over a first pass and stops. Asking it to check, against the inputs, against the constraints, against the task, is the built-in review invoked by hand, and it is the cheapest reliability available. It catches the errors a first pass misses, and it narrows the gap between one run and the next. It is the calculator instinct applied to reasoning: on anything consequential, you re-check the figure rather than trust it once.

Output fixes the form of the answer: a table, a paragraph, a tone, a length. It does not change whether the answer is right, but it removes variance in how the answer arrives, which is determinism over presentation, and it makes the result usable and comparable from one run to the next.

Because a model works in turns, the order of these parts is itself load-bearing. They are not a block to paste at once; they unfold. The task comes first, because it defines the work. The model then does the work. Verification comes after the work and before the answer is trusted, because there is nothing to check until the analysis exists. Asking a model to audit its work on the opening turn, before it has done any, verifies nothing. Output comes last, shaping what survives. This is why the method is interactive: the first prompt sets the task and scope, and the follow-on prompts are where the steering happens, a verification pass here, a tightened constraint there, the output reshaped there. An agent's plan is fixed before the run. A person's structure accrues across it, in the order the work requires.

So the thesis reaches past agents. The mechanism is the same, attention shaped rather than the model caged, and attention can be shaped by an authored plan or by a person at a keyboard. The problem the opening set out, that a model gives neither accuracy nor determinism for free, is one a person can answer by hand: name the task, make the model check itself, fix the form, and spend that structure only where the stakes earn it. We are now teaching this frame to people who work in regulated environments, to raise the quality and focus of their prompting in real time. It asks for no engineering, and it is available today.

## What iGentic does not claim

A claim that hides its limits is dismantled in the first serious conversation, so we state the limits plainly.

iGentic does not make the model trustworthy. It makes the system legible and puts the guarantees where they can be enforced. The trust is in the design, not the model. Nor does it enforce by itself. Its rules are honoured by the model, not policed by the document, and where a rule must hold, that holding is a deterministic check at the gate. The check, not the plan, is what holds.

A plan can be confidently wrong. The mechanism that focuses the model focuses it whether the plan is right or not, so a bad Work Plan does not fail loudly; it fails with conviction, straight to the wrong answer. The value lives in boundaries that are correct, set by someone who knows the domain. iGentic makes a wrong plan legible. It does not make it right. In the same spirit, the self-review catches only what the author wrote into it: a blind spot in the plan is a blind spot in the run, and the plan is only as good as the expertise written into it.

The uncertainty gate is honest about only half of itself. Its resolution is a human, which is real enforcement. Its trigger is the model's own read of its own doubt, which is not. A model certain of a wrong answer does not escalate it, so the gate catches the doubt the model can feel, not the blind spot it cannot. This is worth saying plainly, because the first serious reviewer will say it.

Finally, the capability iGentic assumes is real today and grows with every model, but it is not a theorem. The claim is a specification plus a thin harness that keeps a capable model focused, not a specification alone, at any size, on any model.

## The claim, in one line

> *iGentic turns a domain expert's judgement into a legible, portable plan. It points a capable model at the decisions that matter, allocates determinism to the gates that need a guarantee, stays inspectable in production, and composes from one agent to an organisation of them.*

Each camp can match a piece of this. The deterministic tools enforce, but cannot stay adaptive or stay legible to a domain expert. The free-form prompt is adaptive, but has no plan to read or diff against. The runtime-bound frameworks are powerful, but welded to their engine. iGentic's claim is the combination, honestly scoped: not that it makes a model obey, but that it makes the whole system legible, portable, and inspectable, and puts enforcement exactly where it belongs. The model is the executor. The plan is the product.
