# Checking a Vendor Contract with the 7-Step Method

> **Purpose**: A worked example for the 7-step method. It follows a compliance analyst using a chat assistant to check whether a vendor contract meets the company's data-protection requirements. Unlike the agent examples, this is a person prompting by hand, adding parts of the method across turns rather than handing over a whole plan.
>
> Synthetic example. Not drawn from any client engagement.

## The situation

Dana is a compliance analyst. A new vendor contract has come in, and she needs to know whether it meets the company's eight data-protection requirements before it goes for signing. She cannot read every clause of every contract closely, and a missed requirement is a real risk in a regulated setting.

This is a consequential, regulated task, so it earns more structure than a casual question. Dana reaches for the parts of the method the stakes call for, and leans on the three that carry the most weight: a precise Task, a Verification pass, and a fixed Output. She sets Role, Inputs, and Constraints up front, then weaves Verification and Output in as follow-on steers.

## Turn 1: the first prompt

Role, Task, Inputs, Constraints, and Output, set at the start.

> Act as a data-protection compliance analyst.
>
> Check whether the vendor contract below meets each of our eight data-protection requirements, so I can decide whether it is ready to sign.
>
> Use only the contract text and the requirements list I have pasted. Do not rely on general knowledge of privacy law, and do not assume anything that is not written in the contract.
>
> For each requirement, say whether it is met, partly met, or not met, and quote the exact clause that supports your finding. If no clause addresses a requirement, say so plainly rather than inferring.
>
> Requirements: [the eight requirements pasted here]
> Contract: [the contract text pasted here]

Why these parts. The **Task** names the action and its purpose, so the model aims at a sign-or-not decision rather than a generic summary. **Inputs** bound it to the contract and the list, which is the main defence against a confident, wrong answer in a legal document. The **Constraints** stop it filling gaps with general privacy knowledge, which here would be a liability. The **Output** fixes the shape so Dana can act on it. She does not use **Steps**, because the work does not need a prescribed method, and she leaves out the agent-only machinery entirely.

## The model's first pass

The assistant returns a finding for each requirement, with quoted clauses. It is a solid draft. On a contract, though, a first pass is not enough, because a first pass is exactly where a clause that only half-supports a requirement gets marked as met.

## Turn 2: the verification steer

Verification, added once there is work to check.

> Before we treat this as final, check your own assessment against the contract text. For every requirement you marked met or partly met, confirm that the clause you quoted actually says what you claim. List any finding where the quote does not fully support the conclusion, then give a corrected assessment.

Why now, and not earlier. There was nothing to verify until the assessment existed. Asking for a self-check on the opening turn, before any analysis, would have checked nothing. Now the model has a draft to audit, and this is where the reliability is bought: the verification pass catches the requirement the first pass marked met on a clause that only partly supports it.

## Turn 3: the output reshape

Output, refined now that the content is settled.

> Now put the final, corrected assessment into a table: one row per requirement, with columns for status (met, partly, not met), the clause reference, and a one-line note. Add a final row that states, on this evidence, whether the contract is ready to sign or needs changes first.

Why. The form matters because this goes to a decision. A table makes the gaps obvious at a glance and gives Dana something she can attach to the file and defend later. The content did not change; the shape did.

## What this shows

Dana never used all seven parts. She used Role, Task, Inputs, Constraints, Verification, and Output, and she left out Steps and everything an autonomous agent would need. She added the parts in the order the work required: task and scope first, verification once there was work to check, output last. Asking for verification before the analysis existed would have done nothing, which is why it came as a follow-on steer rather than part of the first prompt.

The three that did the heavy lifting are the three the method leans on. The **Task** bought accuracy, by aiming the model at the right question. The **Verification** bought reliability, by making the model check its own work before Dana relied on it, the way she would re-check a figure that mattered. The **Output** bought consistency of form, a result she can reuse and defend.

This is the thesis in a person's hands. A model gives neither accuracy nor determinism for free, so Dana bought back the parts the stakes demanded, by hand, and spent the effort where it mattered: on a regulated decision, not on a throwaway question.
