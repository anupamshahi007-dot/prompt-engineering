# prompt-engineering
Notes, templates, heuristics, and evaluation checklists for practical prompt engineering and prompt testing.

## Purpose
This repository captures my disciplined approach to crafting and evaluating prompts: templates, testing workflows, evaluation metrics, and a short library of reusable prompt components. It’s a living reference for how I iterate on prompt design.

## Top-level layout
- templates/        Reusable templates (instruction + constraints + format)
- experiments/      Small experiment notes and results (structured)
- checklists/       Test checklists, evaluation rubrics
- scripts/          Small helpers (example callers, sanitizers)
- README.md         This file

## Core content & example templates

1) Minimal instruction template
- system: concise role (what the model should be)
- instruction: goal + constraints
- format: exact output schema (JSON / YAML / markdown)
- validation: checks to run against output

Example: JSON-output template
```
system: "You are an assistant that outputs valid JSON and nothing else."
instruction: "Convert the notes into an object with fields: title, action_items[], summary."
format: "JSON with keys: title (string), action_items (array of {owner,task,due}), summary (string)"
```

## Evaluation & testing
- Manual evaluation: clarity, correctness, completeness
- Automated checks:
  - Schema validation (JSON Schema)
  - Exact-match tests for parts of output
  - Consistency checks across multiple temperatures
- Suggested metrics:
  - Precision / Recall for extracted items (when labeled data exists)
  - Human rating (1–5) for usefulness and readability

## Prompt testing workflow (recommended)
1. Small prototype prompt (system + user) in templates/
2. Run 20 examples across temperature sweep (0.0, 0.2, 0.7)
3. Validate outputs with schema checks + spot human reviews
4. Record results in experiments/ with short notes and final chosen prompt

## Tools & snippets
- Use a lightweight script to assemble system+user+few-shot examples before sending
- Store canonical test examples under experiments/examples.json for regression checks

## Best practices & heuristics
- Always specify expected output format (machine-parseable when possible)
- Use low temperature for extraction tasks; higher for creative tasks
- Provide constraints (length, tokens, banned words) to reduce hallucination
- Prefer few-shot examples for structured transformations

## How to use
1. Clone the repo
2. Read templates/ for pattern you want
3. Run a sample via scripts/run_example.py (or copy the pseudo code shown in ai-prompts)
4. Add experiments/notes for any prompt you tune

## Contributing
- Add templates or experiments as small PRs.
- When adding evaluation data, include a short README explaining the test set.

## License
MIT

## Contact
anupam.shahi007@gmail.com
