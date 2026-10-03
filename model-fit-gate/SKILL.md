---
name: model-fit-gate
description: Assess GPT-6 Luna, GPT-6.1 Sol, and GPT-6 Astra model and reasoning-level fit for execution tasks or context-dependent judgments, and reassess as work evolves. Skip straightforward casual Q&A and clearly mechanical, low-stakes clerical or transfer work.
---

# Model fit gate

First decide whether the request needs this gate. Skip it for (a) straightforward casual conversation or a small standalone question that needs no action or contextual judgment, and (b) clearly mechanical, low-stakes clerical or transfer work that follows explicit instructions and needs no meaningful interpretation, such as copying supplied text into a specified place or moving already-identified files. For other requests to execute work or make a judgment that depends on prior conversation or other context, use the gate; a task can be easy and still need it when it calls for judgment. If a seemingly routine task has ambiguity, synthesis, consequential changes, or meaningful verification decisions, use the gate. This is only a model-fit exemption; it does not change applicable permissions or safety requirements.

For requests in scope, assess fit silently before work. Reassess only when new information materially changes the difficulty of the remaining work. Treat **Model** as the model choice and **Level** as its reasoning effort.

## Assess fit

Estimate breadth, ambiguity, unfamiliarity, coupling, required judgment, verification burden, and the cost of an error. Recommend the least costly available pair that can complete the work reliably:

- **GPT-6 Luna:** focused, clearly scoped work where efficiency matters.
- **GPT-6.1 Sol:** broader judgment, coding, research, or synthesis.
- **GPT-6 Astra:** the hardest, most ambiguous or consequential work when lower-cost choices are unlikely to be reliable enough.

Choose a supported reasoning effort for the actual work. Do not infer difficulty from length alone. Keep the recommended pair available as the difficulty assessment for skills such as 百鍊の境, even when no user-facing recommendation is needed.

Use the user's stated pair, their confirmation for the same active task, or reliably available runtime information to assess the current setting. If either field is unknown, keep it unknown and begin with the current setting; missing metadata alone does not justify asking for confirmation or stopping. Do not infer the current setting from an unrelated earlier task.

## When to speak and pause

Proceed quietly when there is no meaningful reason to change settings. Do not require a Model / Level declaration for each request.

Raise an upgrade early when the request or an initial inspection reveals concrete signs that a stronger pair is likely to materially improve reliable completion. Explain the actual difficulty, such as interacting constraints, consequential unresolved judgments, or a verification scope that exceeds the initial estimate. Do not wait for repeated failures. A long task, ordinary obstacle, isolated failed command, or uncertainty by itself is not evidence of a model mismatch.

When recommending an upgrade, end the current turn at a resumable point so the user can switch settings and send a new message. Preserve completed work and avoid beginning the dependent difficult step. The response should briefly include:

- **STOP** (a resumable pause) and the concrete reason for the recommendation, stating uncertainty when the current pair is unknown.
- The recommended **Model / Level**.
- Any completed or in-flight work that materially affects resumption, and the exact next step.
- “切換 Model／Level 後，回覆『繼續』就可以接住做。”

Ending the turn creates the opportunity to switch; do not claim to stop or cancel external processes merely by sending a final response. Resolve or identify any in-flight work whose state affects safe continuation. The user should not need to forcibly interrupt a normally responsive turn.

If the current setting is stronger than needed, continue. Offer a brief, optional cost-saving suggestion only when the remaining work makes the saving meaningful; do not stop for a downgrade.

## Resume and reassess

After the user switches and replies “繼續”, resume the same task from the stated point using the current setting. Do not demand that they repeat the whole task or restate the pair. Do not claim the switch was verified unless it is reliably visible.

If the user chooses to keep their setting, respect that choice where the remaining work can be completed responsibly. If a specific judgment cannot be made reliably, state that limit and pause only the dependent work; do not claim an unsupported outcome.

Reassess when scope, dependencies, consequences, or verification needs materially change. Natural phase boundaries can help notice these changes, but do not turn them into mandatory announcements or checkpoints. Avoid repeating the same recommendation after the user has already made a choice unless new evidence changes it.

Never claim to switch models or reasoning levels yourself. Use the current supported catalog when available; otherwise qualify model availability. Avoid false precision about cost or capability.
