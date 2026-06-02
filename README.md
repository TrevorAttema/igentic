# iGentic

*A way to direct capable models through real work: one document a person can author and read.*

iGentic is a declarative language for Work Plans. A Work Plan is a single document that directs a capable model through a piece of real work, and it is meant to be authored and read by the domain expert who owns the work, not only by an engineer. This repository holds the argument behind iGentic, the specifications for writing it, and a method for using the same discipline by hand.

## The idea in brief

We tend to call software "reliable" when it does two things at once: it gives the right answer (accuracy), and it gives the same answer every time (determinism). A calculator gives both for free. A reasoning model gives neither for free, and holding a reasoning tool to a calculator's standard is where most AI projects on real, human-facing work fall short.

iGentic treats determinism as something the author sets against the stakes, not a property the system has. A Work Plan focuses a capable model's attention on the decisions that matter, keeps its judgement where judgement is wanted, and marks the few places where a decision needs a guarantee. Where a guarantee is required, the plan calls a hard check, and the check, not the model, is what enforces it. The plan is legible before a run and observable during it, so a person can read it beforehand and hold the run against it as it happens.

The full argument is in the thesis. The specifications say how to write a Work Plan. The 7-step method is the same discipline reduced to something a person can use by hand while prompting.

## What is in this repository

- **igentic-thesis.md** is the thesis: what iGentic is, why it works, where the guarantees come from, and what it does not claim. Start here for the argument.
- **igentic-formal-spec.md** is the formal grammar: the eleven elements of a Work Plan and the notation for writing them, with a worked example.
- **igentic-register-spec.md** is the two registers: the same elements written in formal notation or in plain prose, with the conventions of the prose register.
- **igentic-7-step-method.md** is the human method: a reduced, seven-part form of the grammar for prompting generative AI tools by hand, in real time.
- **examples/** holds one worked example for each specification: an incident-intake agent in the formal register, a complaint reviewer shown in both registers, and a 7-step prompting walkthrough for checking a contract.

## Where to start

If you want to understand the idea, read the thesis, beginning with its summary.

If you want to prompt AI tools better today, without building anything, read the 7-step method.

If you want to author Work Plans, read the register spec for the two ways to write them, and the formal spec for the full element definitions and syntax.

## What iGentic does not claim

A Work Plan focuses a model; it does not by itself make the model trustworthy. The trust is in the design and in the checks the plan places. The document does not enforce its own rules; where a constraint must hold, the guarantee is a deterministic check at a gate. A plan can also be confidently wrong, so it is only as good as the expertise written into it. And how well a given plan focuses a given model is an empirical question, to be measured, not asserted.
