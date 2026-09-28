This skill is automatically triggered when performing Codex tasks. 
It initially checks if specified current model / compute level in prompt is suitable for the task. 
  If not specified, it reads the prompts and stops to suggest suitable reliable level. 
It will also keep tracking the overall difficulty and ability while running the real task. Will stop to suggest for suitable model and compute level if it finds task / ability does not match.

  Stop condition : Both using too much compute or not enough compute.

This skill mostly serves as a model-fit-gate to serve a great balance for those with budgets or limited Codex usage while maintaining high reliability for the tasks. 
