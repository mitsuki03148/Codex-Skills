---
name: model-fit-gate
description: Assess model and reasoning-level fit before clear execution tasks or judgments requiring prior context, and reassess when complexity changes. Skip straightforward casual questions and answers.
---

# Model fit gate

First decide whether the request needs this gate. Use it when the user clearly asks you to execute work, or asks for a judgment that depends on understanding prior conversation or other context. A task can be easy and still require the gate when it calls for action. For an obviously simple, casual question or answer that needs no action or contextual judgment, answer directly without requiring Model / Level. Do not turn the exemption into a difficulty test for ordinary conversation.

For requests in scope, apply this gate before acting and again when inspection or execution changes the difficulty estimate. Treat **Model** as the model choice and **Level** as its reasoning effort.

## Before work

1. Estimate the work's difficulty from the request: breadth, ambiguity, unfamiliarity, coupling, required judgment, verification burden, and cost of an error. Recommend the least costly currently available model and level that can complete it reliably. Do not infer difficulty from length alone.
2. Look for an explicit **Model** and **Level** stated at the start of the current request. A direct user confirmation for this same active task also counts. A model shown by the app, inferred from an unrelated earlier task, or mentioned only as a possible recommendation does not satisfy this requirement. If either field is missing, **stop before task tools or substantive work**. State the difficulty estimate and a concrete recommended model and level; ask the user to confirm that pair.
3. If both are present, compare the stated pair with the estimate. If it is too weak for reliable and efficient work, **stop** and recommend a sufficient pair. In particular, call out work that genuinely needs an Astra class model. If it is clearly excessive for the task, **stop** and recommend a less costly sufficient pair. Otherwise proceed.

Do not claim to switch models or reasoning levels yourself. Use the model choices and supported levels available in the current environment; if that catalog is unknown, make the recommendation conditional and say what must be checked. Avoid false precision about token cost or capability.

## During work

At natural phase boundaries, compare the current pair with the reasoning needed for the **remaining** work. Use whichever boundaries the task actually has:

- **Initial understanding → execution:** After the first pass through key files or source material, revise the estimate using the actual scope, dependencies, ambiguity, and likely implementation work.
- **Execution → verification:** Reassess when implementation is substantially complete and the next work is testing, review, or interpreting failures. Account for the consequence of missed errors, not just the amount of code left.
- **Verification → delivery:** Before consequential final actions such as publishing, merging, or pushing, reassess any unresolved judgment and the evidence gathered. A brief mechanical commit or push alone does not justify a model switch.

Also reassess immediately when significant new information appears within a phase: additional systems, higher verification risk, repeated ambiguous failures, or work that proves much simpler than expected. These are decision points, not a requirement to recheck after every tool call or to force phases onto a short task.

Stop promptly if the current pair has become unreliable for the remaining work or clearly wasteful across a meaningful amount of it. Recommend a stronger or lighter pair as appropriate. Report the new evidence, the revised difficulty, a concrete model and level, and the state of any work already done. Leave reversible partial work intact so the next run can continue. Do not keep working with a known mismatch just to finish a milestone.

An ordinary obstacle, failed command, or long task is not by itself proof of a model mismatch. Base the decision on the reasoning and verification the remaining work requires.

## Response at a stop

Keep the stop short: **STOP**, the difficulty judgment, why the current or unspecified pair is unsuitable, the recommended **Model / Level**, and any partial work or verification that affects handoff. Do not present the task as completed.
