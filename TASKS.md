# TASKS — onco-research-software-docs

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

## How these tasks map to Hee-Lee Oss

Each task below becomes a Hee-Lee Oss **Task JSON** validated against
`packages/schema/src/schemas.ts`. Field mapping:

- `id` — stable slug ID from the tables (e.g. `onco-research-software-docs-template-003`).
- `title` — the table's Title.
- `project` — `onco-research-software-docs`.
- `type` — `code | research | writing | data | design-spec | maintenance` (per task). Tests/tooling
  contributed as PRs → `code`; tutorials/guides/docstrings → `writing`; triage/outreach → `research`;
  gate/templates → `design-spec`; refresh → `maintenance`. **We do not use `data`** (no datasets
  are produced or redistributed).
- `lane` — `donated` for all tasks (no funded escrow). A funded variant would add `fundedBudgetUsd`.
- `priority` — `high | medium | low`.
- `domain` — array, e.g. `["cancer-research","open-source","bioinformatics","reproducibility"]`.
- `riskTier` — `low` for developer-facing docs/tests on permissive tools with shipped/synthetic
  data; `medium` when a biological/clinical claim needs domain review or data needs nuanced
  license/de-identification judgement. `high` (patient-facing/clinical) is **out of scope** —
  no task here is `high`.
- `urgent` — boolean; `false` for all current tasks.
- `deliverable` — `pr | dataset | document | translation`. Upstream code/tests/docs PRs → `pr`;
  project-internal artifacts (gate, templates, catalog, outcome records) → `document`. **Never
  `dataset`** (data is out of scope).
- `tokenEstimate` — `small | medium | large` (Size column).
- `status` — `open | in-progress | review | delivered | done`; all start `open`.
- `context`, `objective`, `acceptanceCriteria[]`, `resources[]`, `output` — per task.
- `requestor` — **TO BE SECURED** until a named upstream maintainer agrees to review/accept.
- `verifiedNeed` — **`false`** until a named maintainer confirms the contribution is wanted
  (general need is real; per-task delivery need is unproven). Flips to `true` only on confirmation.
- `outputLicense` — **upstream project's license** for code/docs contributed *in-repo*;
  **`CC-BY-4.0`** for standalone tutorials/docs we author; **`MIT`** for standalone Hee-Lee Oss-side
  helper tooling.

---

## Milestone M0 — Foundation & cold-start

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| onco-research-software-docs-reviewer-001 | Name/secure the License + Data-provenance reviewer (blocking gate role) | research | small | low | document | — | Maintainer |
| onco-research-software-docs-gate-002 | Contribution + cancer-data guardrail gate (license, open-access data, no-advice) | design-spec | small | medium | document | — | License+Data |
| onco-research-software-docs-template-003 | Doc/test/tutorial templates + canonical contribution model | design-spec | small | low | document | — | Technical |
| onco-research-software-docs-repro-004 | Reproducible environment recipe + CI harness that runs a tutorial | code | medium | low | pr | template-003 | Technical |
| onco-research-software-docs-catalog-005 | Seed + triage the candidate-software catalog | research | medium | medium | document | gate-002 | License+Data |
| onco-research-software-docs-outreach-006 | Issue-first upstream maintainer outreach + gap shortlist | research | small | low | document | catalog-005 | Steward |
| onco-research-software-docs-pilot-007 | Pilot contribution end-to-end, merged upstream | writing | medium | low | pr | reviewer-001, gate-002, template-003, repro-004, catalog-005, outreach-006 | License+Data, Technical |

**Acceptance criteria — key tasks**

- **reviewer-001 (secure the blocking reviewer)**
  - [ ] A named person (or ≥ 2 in rotation) is appointed who can read SPDX/OSS licenses
        (MIT/BSD/Apache/GPL/LGPL/AGPL/MPL), assess CLA vs. DCO terms, and apply the cancer-data
        guardrail (open-access tiers, de-identification, COSMIC/OncoKB restrictions).
  - [ ] Appointment (name + qualification) recorded; rotation rule documented (≥ 1 always present
        or triage halts).
  - [ ] Until filled, all tasks remain `verifiedNeed: false` and nothing passes the gate.

- **gate-002 (contribution + cancer-data gate)**
  - [ ] Software axis: PASS only if the tool's license is OSI-approved and permits our
        contribution, the contribution policy (CLA/DCO, contributing guide) is recorded and
        acceptable (broad CLAs escalated to governance), and the for-profit-vehicle check passes.
  - [ ] Data axis (binding): example/fixture/tutorial data must be open-access / aggregate /
        de-identified with a verified license; controlled-access (dbGaP/EGA/controlled-tier GDC) and
        identifiable data are EXCLUDED; COSMIC/OncoKB content is **never embedded** (document-by-
        reference only). Data-minimization priority recorded: shipped ▸ synthetic ▸ open-access.
  - [ ] No-advice check: confirms the contribution is developer/researcher-facing and contains no
        medical advice or clinical interpretation; the "not medical advice" disclaimer is required
        on tutorials.
  - [ ] Produces a committed, reviewable PASS/FLAG/EXCLUDE artifact per contribution recording
        which checks ran and what fired (both axes + provenance + de-identification disposition).

- **repro-004 (reproducible environment + CI harness)**
  - [ ] Provides a pinned-environment recipe per ecosystem (conda-lock/pixi/`renv.lock`/hashed
        requirements) + optional container digest; "reproducible" = clean machine + lockfile runs
        the artifact to completion with recorded outputs.
  - [ ] A CI workflow recreates the environment and executes one tutorial/test end-to-end headlessly
        on shipped/synthetic data; the run reference is recorded in `reproEnv.ciRunRef`.
  - [ ] Code MIT-licensed (Hee-Lee Oss-side helper); `pnpm build && pnpm test && pnpm lint` green for any
        Hee-Lee Oss-side tooling; DCO signed-off.

- **pilot-007 (pilot contribution, end-to-end)**
  - [ ] Target tool selected for a realistic merge path: OSI-permissive (MIT/BSD/Apache), actively
        maintained, DCO (not broad-CLA), with a maintainer-labelled "good first issue"/"docs/tests
        wanted" gap, needing only shipped or synthetic data (chosen to avoid a biological claim, so
        the pilot stays `low` and needs no Domain reviewer).
  - [ ] Passed gate-002 (both axes) with the artifact committed; issue-first alignment confirmed
        with the maintainer before authoring.
  - [ ] The docs/tests/tutorial follows the templates; any tutorial runs reproducibly in CI from
        the pinned environment (`reproEnv.ciRunRef` recorded); provenance/citations present.
  - [ ] **Merged upstream** with the Steward's acceptance evidence artifact
        (`outcomes/onco-research-software-docs-pilot-007.json`, merge-commit URL + coverage
        before/after) recorded — or, if not merged, **submitted** with the blocker surfaced.

**M0 Definition of Done:** License+Data reviewer named (blocking role filled before pilot review);
gate + templates + canonical contribution model published; reproducible-environment recipe and CI
harness green on one tutorial; candidate-software catalog seeded and triaged (≥ 10 entries
license-classified); one pilot contribution **merged upstream** end-to-end (evidence artifact
recorded) — or submitted with the blocker surfaced; ≥ 1 issue-first maintainer thread opened.

---

## Milestone M1 — Gate hardened + first merges

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| onco-research-software-docs-snapshot-008 | License-snapshot capture for referenced data sources | code | small | low | pr | gate-002 | Technical |
| onco-research-software-docs-triage-009 | Triage 5 catalog tools through the gate | research | medium | medium | document | gate-002, catalog-005 | License+Data |
| onco-research-software-docs-partner-010 | Secure first confirmed upstream maintainer partner | research | small | low | document | outreach-006 | Steward |
| onco-research-software-docs-contrib-011 | Contribution #2 — docstring/API docs for a permissive genomics tool | writing | medium | low | pr | pilot-007, triage-009 | License+Data, Technical |
| onco-research-software-docs-contrib-012 | Contribution #3 — tests for a permissive survival-analysis library | code | medium | low | pr | pilot-007, triage-009, repro-004 | License+Data, Technical |
| onco-research-software-docs-contrib-013 | Contribution #4 — tutorial with a biological claim (Domain-reviewer path) | writing | medium | medium | pr | pilot-007, triage-009, repro-004 | License+Data, Technical, Domain |

**Acceptance criteria — key tasks**

- **snapshot-008 (license-snapshot capture)**
  - [ ] For any referenced data source, captures a committed copy of the license text/page + SHA-256
        hash + Wayback save URL; `exampleData.provenanceRef` records path + hash + timestamp.
  - [ ] Code MIT-licensed; tests + CI green; no credentials embedded.

- **triage-009 (triage 5 tools)**
  - [ ] Five tools evaluated with a committed gate artifact each (both axes + PASS/FLAG/EXCLUDE +
        rationale), applying the COSMIC/OncoKB "never embed" rule and the for-profit-vehicle check.
  - [ ] Each PASS records license id/URL, contribution policy (CLA/DCO), maintenance status, and the
        data-minimization disposition.
  - [ ] Any non-OSI / broad-CLA / open-core / non-redistributable-data case is FLAGGED/EXCLUDED with
        the concern surfaced.

- **partner-010 (first confirmed partner)**
  - [ ] A named upstream maintainer confirms they will review and accept a contribution.
  - [ ] Contribution mechanism documented (PR flow, DCO/CLA, contributing guide, CI expectations).
  - [ ] Tasks for that tool updated to `verifiedNeed: true` with `requestor` set.

- **contrib-013 (tutorial with a biological claim — Domain path)**
  - [ ] Every biological/clinical assertion carries an inline citation to a primary/authoritative
        source; Domain reviewer (bioinformatician; oncologist if clinical context) signs off.
  - [ ] `riskTier: medium`; mandatory "research/education use, not medical advice" disclaimer.
  - [ ] Tutorial runs reproducibly in CI on shipped/synthetic/open-access data; merged upstream with
        the outcome artifact recorded.

**M1 Definition of Done:** gate applied to ≥ 3 contributions with committed artifacts; ≥ 3
contributions merged across ≥ 2 tools; ≥ 1 confirmed maintainer partner; license-snapshot capture
working; the Domain-reviewer path exercised on ≥ 1 medium-risk contribution.

---

## Milestone M2 — Reproducible tutorials & scale

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| onco-research-software-docs-harness-014 | Generalize the repro harness across ≥ 3 ecosystems | code | medium | low | pr | repro-004 | Technical |
| onco-research-software-docs-contrib-015 | Contribution #5 — imaging/pathology tool tutorial (open imaging) | writing | medium | medium | pr | harness-014, triage-009 | License+Data, Technical, Domain |
| onco-research-software-docs-contrib-016 | Contribution #6 — single-cell toolkit docs + doctests | writing | medium | low | pr | harness-014, triage-009 | License+Data, Technical |
| onco-research-software-docs-coverage-017 | Record doc/test coverage before/after for ≥ 3 tools | research | small | low | document | contrib-011, contrib-012, contrib-016 | Technical |

**Acceptance criteria — key tasks**

- **harness-014 (generalize the harness)**
  - [ ] Reproducible-environment harness works for ≥ 3 ecosystems (e.g. Python/conda, R/`renv`, and
        a container-based tool), each running a tutorial/test end-to-end in CI from its lockfile.
  - [ ] Documented "add a new tool" path; code MIT-licensed; CI green.

- **contrib-015 (imaging/pathology tutorial)**
  - [ ] Uses **open imaging only** (open-tier TCGA/CPTAC or the tool's shipped sample), license +
        de-identification verified in the gate artifact; no controlled-access slides.
  - [ ] Biological claims cited; Domain reviewer sign-off; "not medical advice" disclaimer present.
  - [ ] Runs reproducibly in CI; merged upstream with outcome artifact recorded.

- **coverage-017 (coverage deltas)**
  - [ ] Doc-completeness and/or test-coverage before/after recorded for ≥ 3 tools using the named
        ecosystem tooling; stored in each contribution's gate/provenance artifact.

**M2 Definition of Done:** repro harness used across ≥ 3 ecosystems with every delivered tutorial
green in CI from its lockfile; ≥ 6 contributions merged cumulatively across ≥ 3 tools; measurable
doc/test coverage improvement recorded for ≥ 3 tools; per-contribution effort reduced vs. M0/M1
baseline median.

---

## Milestone M3 — Reuse outcomes & sustainability

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| onco-research-software-docs-reuse-018 | Track and verify external reuse events | research | small | low | document | contrib-011, contrib-013, contrib-015 | Steward |
| onco-research-software-docs-refresh-019 | Anti-bit-rot refresh process + drift detection | maintenance | small | low | document | harness-014 | Maintainer |
| onco-research-software-docs-contrib-020 | Contributions #7–#8 across new tools/ecosystems for breadth | writing | large | medium | pr | harness-014, partner-010 | License+Data, Technical, Domain |

**Acceptance criteria — key tasks**

- **reuse-018 (reuse tracking)**
  - [ ] ≥ 3 verifiable external reuse events recorded (citation / fork-with-activity / docs link /
        issue referencing the tutorial); each links to externally verifiable evidence (no
        self-report).

- **refresh-019 (anti-bit-rot)**
  - [ ] Documented cadence to re-run delivered tutorials against new tool releases; CI flags
        breakage; breakages become `maintenance` tasks; lockfiles updated deliberately.

- **contrib-020 (breadth contributions)**
  - [ ] Two further contributions spanning new tools/ecosystems so delivered work covers ≥ 3
        ecosystems (genomics / imaging / survival-stats); each gate-passed, reproducible, merged,
        with outcome artifacts; Domain reviewer where a biological claim appears.

**M3 Definition of Done:** ≥ 3 verifiable reuse events; ≥ 8 contributions merged cumulatively across
≥ 4 tools and ≥ 3 ecosystems; anti-bit-rot refresh process documented and a Steward identified for
ongoing upstream liaison.

---

## Candidate-software catalog (seed)

The pool of tools we *might* contribute to. This is a **candidate backlog only**: the `License` and
`Notes` columns are first-pass triage signals; **no tool becomes a task until it passes the gate**
(`gate-002`) via the triage task (`triage-009`), which confirms license, contribution policy
(CLA/DCO), maintenance, the for-profit-vehicle check, and the cancer-data disposition. The catalog
biases toward clearly OSI-permissive, actively-maintained tools that work with shipped/synthetic
data. License strings are indicative and **must be re-verified at the gate**.

**Priority:** A = OSI-permissive (MIT/BSD/Apache) + works on shipped/synthetic data (good-first-deed).
B = copyleft (GPL/LGPL/AGPL/MPL) or needs an external open-access dataset (verify at gate).
C = depends on a non-commercial data source (COSMIC/OncoKB) or possible for-profit/open-core nuance
→ escalate; data document-by-reference only, never embedded.

| Tool | Ecosystem | License (verify) | Priority | Notes / cancer-data disposition |
| --- | --- | --- | --- | --- |
| maftools | genomics (R/Bioconductor) | MIT | A | Mutation-annotation viz; ships example MAFs (use shipped data) |
| lifelines | survival-stats (Python) | MIT | A | Survival analysis; synthetic/shipped data; no patient data |
| Scanpy (scverse) | single-cell (Python) | BSD-3-Clause | A | scRNA-seq; shipped PBMC-style example data |
| Seurat | single-cell (R) | MIT | A | scRNA-seq; shipped example data |
| Cellpose | imaging (Python) | BSD-3-Clause | A | Cell segmentation; shipped sample images |
| StarDist | imaging (Python) | BSD-3-Clause | A | Nucleus segmentation; shipped samples |
| PyRadiomics | imaging (Python) | BSD-3-Clause | A | Radiomics features; shipped phantom/sample |
| Arriba | genomics/fusions (C++) | MIT | A | Fusion detection (EWSR1-FLI1 relevant); synthetic/shipped reads |
| nf-core/sarek | genomics pipeline (Nextflow) | MIT | A | Cancer variant calling; test profile uses tiny synthetic data |
| GATK4 | genomics (Java) | BSD-3-Clause | B | Variant calling; large; use bundled test resources only |
| DESeq2 | genomics (R/Bioconductor) | LGPL-3 | B | RNA-seq DE; copyleft → contribute in-repo; shipped airway-style data |
| scikit-survival | survival-stats (Python) | GPL-3.0 | B | Survival ML; copyleft; synthetic/open data |
| QuPath | imaging (Java) | GPL-3.0 | B | Digital pathology; copyleft; open-tier WSI or shipped sample |
| MONAI | imaging/AI (Python) | Apache-2.0 | A | Medical-imaging DL; use open/synthetic; avoid any controlled imaging |
| VEP (Ensembl) | genomics (Perl) | Apache-2.0 | B | Variant effect prediction; needs cache/data — document-by-reference |
| SigProfilerExtractor | genomics (Python) | BSD-2-Clause | B | Mutational signatures; synthetic catalogs |
| cBioPortal | platform (Java/JS) | AGPL-3.0 | B | Cancer genomics portal; copyleft; public/aggregate data only |
| OncoKB-annotator | genomics (Python) | (verify) | C | **OncoKB data non-commercial** → never embed; document-by-reference token use |
| deconstructSigs | genomics (R) | GPL-3.0 | C | Signatures; **bundles COSMIC signatures** → verify/never redistribute COSMIC content |

---

## Backlog / future

| ID | Title | Type | Size | Risk | Deliverable | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| onco-research-software-docs-i18n-021 | Translate a delivered tutorial (domain + language reviewer) | translation | small | medium | translation | Widens reuse; needs language + domain reviewer |
| onco-research-software-docs-dash-022 | Outcome dashboard (merges, reuse, coverage deltas) | code | medium | low | pr | Reads the outcome ledger; supports success metrics |
| onco-research-software-docs-synth-023 | Shared license-clean synthetic cancer fixtures | code | medium | low | pr | Coordinate with `synthetic-cancer-data`; reduces external-data surface |
| onco-research-software-docs-trouble-024 | Troubleshooting/error-message docs for a high-traffic tool | writing | small | low | pr | Cuts maintainer support burden |
| onco-research-software-docs-contribguide-025 | Contributor-onboarding docs for an under-documented tool | writing | small | low | pr | Helps the maintainer community grow |

---

## Generated task index

> Auto-generated by the Hee-Lee Oss task-decomposition agent on 2026-06-29.
> All 25 files in `tasks/` are schema-valid (validated against `packages/schema/dist/index.js`).
> Seed file: `tasks/onco-research-software-docs-reviewer-001.json` (pre-existing).
> New files generated: 24.
> Fan-out dimensions: none (no explicitly enumerated fan-out in TASKS.md).

| File | Type | Priority | Risk | Deliverable | Token |
| --- | --- | --- | --- | --- | --- |
| onco-research-software-docs-reviewer-001 | research | high | low | document | small |
| onco-research-software-docs-gate-002 | design-spec | high | medium | document | small |
| onco-research-software-docs-template-003 | design-spec | high | low | document | small |
| onco-research-software-docs-repro-004 | code | high | low | pr | medium |
| onco-research-software-docs-catalog-005 | research | high | medium | document | medium |
| onco-research-software-docs-outreach-006 | research | high | low | document | small |
| onco-research-software-docs-pilot-007 | writing | high | low | pr | medium |
| onco-research-software-docs-snapshot-008 | code | medium | low | pr | small |
| onco-research-software-docs-triage-009 | research | medium | medium | document | medium |
| onco-research-software-docs-partner-010 | research | medium | low | document | small |
| onco-research-software-docs-contrib-011 | writing | medium | low | pr | medium |
| onco-research-software-docs-contrib-012 | code | medium | low | pr | medium |
| onco-research-software-docs-contrib-013 | writing | medium | medium | pr | medium |
| onco-research-software-docs-harness-014 | code | medium | low | pr | medium |
| onco-research-software-docs-contrib-015 | writing | medium | medium | pr | medium |
| onco-research-software-docs-contrib-016 | writing | medium | low | pr | medium |
| onco-research-software-docs-coverage-017 | research | medium | low | document | small |
| onco-research-software-docs-reuse-018 | research | low | low | document | small |
| onco-research-software-docs-refresh-019 | maintenance | low | low | document | small |
| onco-research-software-docs-contrib-020 | writing | low | medium | pr | large |
| onco-research-software-docs-i18n-021 | writing | low | medium | translation | small |
| onco-research-software-docs-dash-022 | code | low | low | pr | medium |
| onco-research-software-docs-synth-023 | code | low | low | pr | medium |
| onco-research-software-docs-trouble-024 | writing | low | low | pr | small |
| onco-research-software-docs-contribguide-025 | writing | low | low | pr | small |

---

## Example task JSON

A complete, schema-valid Task JSON for the first M0 task (`reviewer-001`). Validated against
`packages/schema/src/schemas.ts` (all required fields present; no additional properties;
`verifiedNeed: false`; donated lane so no `fundedBudgetUsd`).

```json
{
  "id": "onco-research-software-docs-reviewer-001",
  "title": "Name/secure the License + Data-provenance reviewer (blocking gate role)",
  "project": "onco-research-software-docs",
  "type": "research",
  "lane": "donated",
  "priority": "high",
  "domain": ["cancer-research", "open-source", "bioinformatics", "governance"],
  "riskTier": "low",
  "urgent": false,
  "deliverable": "document",
  "tokenEstimate": "small",
  "status": "open",
  "context": "This project contributes documentation, tests, and reproducible tutorials upstream to widely-used open-source cancer research software. Every contribution must pass a blocking gate covering two license axes (the tool's OSS license + contribution policy, and any example/tutorial data's license) plus the binding cancer-data guardrail (open-access/aggregate/de-identified only; no controlled-access or patient-identifiable data; COSMIC/OncoKB content never embedded) and a no-medical-advice check. That gate cannot run without a qualified reviewer, so this role must be filled before the M0 pilot is reviewed.",
  "objective": "Appoint a named License + Data-provenance reviewer (or a rotation of at least two) qualified to read OSS licenses and CLA/DCO terms and to apply the cancer-data guardrail, and record the appointment and rotation rule.",
  "acceptanceCriteria": [
    "A named reviewer (or >= 2 in rotation) is appointed who can read SPDX/OSS licenses (MIT/BSD/Apache/GPL/LGPL/AGPL/MPL), assess CLA vs. DCO terms, and apply the cancer-data guardrail (open-access tiers, de-identification, COSMIC/OncoKB non-commercial restrictions).",
    "The appointment records each reviewer's name and relevant qualification.",
    "A rotation rule is documented requiring at least one qualified reviewer to be present at all times, or triage and contribution work halts.",
    "It is recorded that until the role is filled, all project tasks remain verifiedNeed:false and no contribution may pass the gate."
  ],
  "resources": [
    "C:\\code\\hee-lee-oss\\planning\\projects\\onco-research-software-docs\\PLAN.md",
    "C:\\code\\hee-lee-oss\\docs\\good-deed-definition.md",
    "C:\\code\\hee-lee-oss\\planning\\ROADMAP.md",
    "SPDX license list; OSI-approved license list; Developer Certificate of Origin (DCO)"
  ],
  "output": "A committed appointment record naming the License + Data-provenance reviewer(s), their qualifications, and the rotation rule, unblocking the gate (gate-002) and the M0 pilot review.",
  "requestor": "TO BE SECURED",
  "verifiedNeed": false,
  "outputLicense": "CC-BY-4.0"
}
```
