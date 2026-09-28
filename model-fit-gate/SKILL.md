---
name: model-fit-gate
description: Assess whether the explicitly stated Codex model and reasoning level fit a work request before starting, and reassess during execution when real complexity emerges. Use for new work requests and material scope changes.
---

# Model fit gate

Use this gate before acting on a work request, and again when inspection or execution changes the difficulty estimate. Treat **Model** as the model choice and **Level** as its reasoning effort.

## Before work

1. Estimate the work's difficulty from the request: breadth, ambiguity, unfamiliarity, coupling, required judgment, verification burden, and cost of an error. Recommend the least costly currently available model and level that can complete it reliably. Do not infer difficulty from length alone.
2. Look for an explicit **Model** and **Level** stated at the start of the current request. A direct user confirmation for this same active task also counts. A model shown by the app, inferred from an unrelated earlier task, or mentioned only as a possible recommendation does not satisfy this requirement. If either field is missing, **stop before task tools or substantive work**. State the difficulty estimate and a concrete recommended model and level; ask the user to confirm that pair.
3. If both are present, compare the stated pair with the estimate. If it is too weak for reliable and efficient work, **stop** and recommend a sufficient pair. In particular, call out work that genuinely needs an Astra class model. If it is clearly excessive for the task, **stop** and recommend a less costly sufficient pair. Otherwise proceed.

Do not claim to switch models or reasoning levels yourself. Use the model choices and supported levels available in the current environment; if that catalog is unknown, make the recommendation conditional and say what must be checked. Avoid false precision about token cost or capability.

## During work

Reassess when reading source material, inspecting a repository, or testing reveals materially different complexity. Stop promptly if the current pair has become unreliable or clearly wasteful. Report the new evidence, the revised difficulty, a concrete model and level, and the state of any work already done. Leave reversible partial work intact so the next run can continue. Do not keep working with a known mismatch just to finish a milestone.

An ordinary obstacle, failed command, or long task is not by itself proof of a model mismatch. Base the decision on the reasoning and verification the remaining work requires.

## Response at a stop

Keep the stop short: **STOP**, the difficulty judgment, why the current or unspecified pair is unsuitable, the recommended **Model / Level**, and any partial work or verification that affects handoff. Do not present the task as completed.
