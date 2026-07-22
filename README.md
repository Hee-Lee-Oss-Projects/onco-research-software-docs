# onco-research-software-docs

> Cancer research runs on open-source software — variant callers, differential-expression and single-cell toolkits, mutational-signature engines, fusion detectors, digital-pathology and medical-imaging   ·  **Risk tier:** low  ·  **Status:** planning

Cancer research runs on open-source software — variant callers, differential-expression and single-cell toolkits, mutational-signature engines, fusion detectors, digital-pathology and medical-imaging frameworks, survival-analysis libraries. These tools are widely used and frequently under-documented and under-tested: missing or stale docstrings, no runnable tutorials, undocumented parameters, brittle examples that no longer run, thin test coverage on critical code paths, and tutorials that silently depend on data a new user cannot legally or practically obtain. The result is wasted researcher time, irreproducible analyses, and a high barrier for newcomers — directly slowing the science.

**Definition of shipped:** via a written confirmation for non-GitHub channels), the tutorial/tests **run reproducibly in CI**, the cancer-data guardrail and provenance are satisfied with the gate artifact committed, and the Steward has recorded the acceptance evidence artifact (`outcomes/<task-id>.json`, w

This is an **Hee-Lee Oss** good-deed project. Contributors pull a task, do it with their own coding agent, and open a PR. Platform: https://github.com/jdev1977/hee-lee-oss

## Plan
- [PLAN.md](./PLAN.md) — robust enterprise plan (vision, architecture, roadmap, risks; includes an applied-improvements appendix + review sign-off)
- [TASKS.md](./TASKS.md) — schema-mapped task backlog
- [tasks/](./tasks/) — ready-to-pull task JSON(s)

## Contribute
```bash
hee-lee-oss browse
hee-lee-oss next --repo Hee-Lee-Oss-Projects/onco-research-software-docs --no-fork
```

## Licensing & review
- Open license (see PLAN.md).
- Risk tier **low** — deeds are *delivered, not merged*; standard review applies.

> Planning stage; no adopting partner secured yet (`verifiedNeed: false` on delivery-dependent tasks).
