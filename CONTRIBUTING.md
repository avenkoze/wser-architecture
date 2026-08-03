# Contributing

This repository is a curated public architecture record, not a source mirror.

## Publication rules

- Record decisions that materially affect product behavior or engineering.
- Explain the context, decision, consequences, and verification requirement.
- Do not publish source code, binaries, credentials, personal data, local file
  paths, private test results, or third-party confidential material.
- Do not present targets or unverified comparisons as completed results.
- Update an existing ADR when clarification does not change the decision.
- Create a new ADR when a decision is replaced or the architecture changes.

## Commit policy

Commits use Conventional Commit-style subjects and represent one coherent
change. Examples:

```text
docs(privacy): define dual protection profiles
docs(ui): adopt web-first interface prototyping
docs(benchmark): establish comparative evidence requirements
```

Empty commits, generated activity, and arbitrary document splitting are not
accepted. The contribution history should remain useful as an engineering log.

