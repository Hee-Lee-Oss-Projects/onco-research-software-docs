# PLAN — onco-research-software-docs

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated
>
> **Cancer-domain guardrails (binding, read first — see "Data, licensing & compliance"):**
> ONLY open-access / aggregate / de-identified data may appear in any example, fixture, or
> tutorial. Controlled-access and identifiable patient data (dbGaP, EGA, controlled-tier GDC,
> individual-level germline/biobank) are **out of scope**. Every data source's license is
> verified before use (open-tier TCGA/CPTAC imaging are acceptable; **COSMIC and OncoKB are
> non-commercial and require special handling/exclusion**). **No medical advice**: any
> patient-facing or clinically-interpretive content is out of scope; the project produces
> developer/researcher-facing material only. **Provenance on every biological or clinical
> assertion.**

## Executive summary

Cancer research runs on open-source software — variant callers, differential-expression and
single-cell toolkits, mutational-signature engines, fusion detectors, digital-pathology and
medical-imaging frameworks, survival-analysis libraries. These tools are widely used and
frequently under-documented and under-tested: missing or stale docstrings, no runnable
tutorials, undocumented parameters, brittle examples that no longer run, thin test coverage on
critical code paths, and tutorials that silently depend on data a new user cannot legally or
practically obtain. The result is wasted researcher time, irreproducible analyses, and a high
barrier for newcomers — directly slowing the science.

This project contributes **documentation, tests, and reproducible tutorials** to widely-used,
genuinely open-source cancer research software, **upstream**, where the work helps every user of
the tool. The unit of work is a single, scoped contribution (a docs PR, a test PR, or a runnable
tutorial) sized for one donated AI session plus human review. The **deliverable is the
contribution merged upstream (or accepted by the maintainer)** — "delivered, not merged" means
the output actually lands where users will benefit, not that a PR was opened.

Two hard constraints shape every task. First, the **contribution gate**: the target tool must be
genuinely open-source (OSI-approved license that permits our contribution), actively maintained,
and not primarily a vehicle for a for-profit's product; our output license must be compatible
with the tool's; and any contributor agreement (CLA/DCO) must be acceptable. Second, the
**cancer-data guardrail**: every byte of example/fixture/tutorial data must be open-access,
aggregate or de-identified, license-verified, and provenance-recorded — with a strong preference
for the tool's own shipped example data or small synthetic data over any external dataset, to
keep the data-licensing surface minimal. Controlled-access data and patient-identifiable data are
never used. The project produces no medical advice and no clinical interpretation.

Risk tier is **low** for the bulk of the work (developer-facing docs/tests on permissively
licensed tools using shipped/synthetic data). Specific tasks escalate to **medium** when a
tutorial or doc makes a biological/clinical claim that needs domain-expert verification, or when
example data requires nuanced license/de-identification judgement. Patient-facing/clinically
interpretive content (which would be `high`) is **out of scope entirely**, not merely gated.

## Problem & beneficiaries

**Who is helped.** Cancer researchers, bioinformaticians, computational biologists, graduate
students, core-facility staff, and the maintainers of the open-source tools themselves. Better
docs and tests lower the barrier to correct use, reduce irreproducible analyses, and reduce the
maintainer support burden (fewer "how do I…" issues). The ultimate beneficiaries are the
patients served by faster, more reproducible cancer research — but the **direct** beneficiaries
of this project are the tool users and maintainers; this project does not touch patients or
patient data.

**The verified need.** Poor documentation and missing tests are repeatedly cited as top barriers
to reproducibility in computational biology and a leading cause of researcher time loss. We treat
the *general* need as well established. The **per-tool, per-contribution need is TO BE SECURED**:
a contribution only counts as needed when a specific upstream maintainer has signalled they want
it (an accepted issue, a "help wanted"/"good first issue" label, a documented gap, or direct
agreement). Until a named maintainer confirms they will review and accept a contribution, the
corresponding tasks carry `verifiedNeed: false`. This honesty is load-bearing: "delivered, not
merged" requires the maintainer to actually accept the work.

**Partner org.** TO BE SECURED. Candidate channels are the maintainer communities of widely-used
open cancer-research tools (e.g. Bioconductor packages, nf-core, MONAI, QuPath, scverse/Scanpy,
lifelines, GATK) reached issue-first. M0 includes explicit, issue-first maintainer outreach; no
partner is assumed, and we never contribute uninvited large changes.

## Goals and non-goals

**Goals**
- Improve the documentation, tests, and tutorials of widely-used **open-source** cancer research
  software, contributed **upstream** so all users benefit.
- Make every tutorial **reproducible**: pinned tool + dependency versions, a committed lockfile
  and/or container, and a CI run that executes the tutorial end-to-end on open/synthetic data.
- Make license/contribution-policy verification and the cancer-data guardrail **non-skippable,
  auditable gates** applied before any work begins.
- Produce reusable templates (docstring standard, tutorial template with mandatory data-license +
  provenance + "research use, not medical advice" header, test patterns) and a reproducible
  environment recipe that every contribution reuses.
- Maintain a license-classified **candidate software catalog** so throughput is transparent and
  the pool is honestly triaged.

**Non-goals**
- We do **not** produce medical advice, clinical interpretation, diagnosis, treatment, or
  patient-facing guidance of any kind. Any task drifting toward this is refused and flagged.
- We do **not** use controlled-access or patient-identifiable data — ever — in examples,
  fixtures, or tutorials.
- We do **not** add features, change behavior, fix algorithms, or refactor for its own sake; the
  scope is docs, tests, and tutorials (a test may reveal a bug — we report it upstream, we do not
  silently change behavior).
- We do **not** contribute to tools that are not genuinely open-source, are unmaintained, or
  primarily serve a for-profit's commercial product (open-core "bait").
- We do **not** redistribute datasets, mirror data, or ship non-redistributable data (e.g.
  COSMIC/OncoKB content) in any artifact.
- We do **not** open uninvited large PRs; contribution is issue-first and maintainer-aligned.

## Success metrics (outcomes)

Outcome-based and beneficiary-centric. Vanity metrics (e.g. "PRs opened", "lines of docs
written") are explicitly excluded.

| Metric | Baseline | Target (first 6 months) |
| --- | --- | --- |
| Contributions **merged/accepted upstream** (last-mile delivered) | 0 | ≥ 8 merged across ≥ 4 tools |
| Tutorials that **run end-to-end reproducibly in clean CI** | 0 | 100% of delivered tutorials green in CI from a pinned environment |
| Tools with measurably improved doc/test coverage (docstring coverage % or closed "docs/tests-needed" issues) | n/a | ≥ 4 tools with a recorded before/after improvement |
| Confirmed upstream maintainer partners (agreed to review/accept) | 0 | ≥ 3 secured |
| License / data-provenance violations in delivered work | n/a | **0** (hard target — any violation is a Sev-1 process failure) |
| Verifiable external reuse (tutorial cited, forked, linked from docs, referenced in an issue) | 0 | ≥ 3 with externally verifiable evidence |
| Domain-accuracy defects found in review (incorrect biological/clinical claim) | n/a | < 1 per 10 delivered; target 0 unreviewed claims shipped |

**Attribution of outcomes.** A "merge/acceptance" is evidenced by a merge-commit URL (or, for
non-GitHub channels, a maintainer's written acceptance) recorded by the Steward in a committed
`outcomes/<task-id>.json`. A "reuse event" must be externally verifiable (a citation, a fork with
activity, a docs link, an issue referencing the tutorial). Self-reported reuse does not count.

**Quantifying "improved coverage" (so DoDs are verifiable).**
- *Doc improvement* per tool is a **doc-completeness delta**: measured docstring/API coverage
  (e.g. `interrogate`/`pydocstyle` for Python, roxygen/`tools::undoc` for R) before vs. after, or
  the count of explicitly-labelled "documentation needed" issues closed. The before/after pair is
  stored in the contribution's gate/provenance artifact.
- *Test improvement* per module is the **coverage delta** on the touched module(s) (line/branch),
  recorded from the project's own CI coverage tooling, before vs. after.
- *Per-contribution effort* is AI-session wall-clock minutes + number of human-review cycles from
  gate-pass to upstream merge, logged in the outcome ledger so later milestones can show the
  reusable harness reducing effort.

## Scope

**In scope**
- **Documentation:** docstrings/API reference, user guides, READMEs/quickstarts, parameter
  documentation, error-message/troubleshooting docs, contribution/onboarding docs — contributed
  upstream.
- **Tests:** unit tests, regression/golden-file tests, documentation/doctests, example-runs-in-CI
  checks — using the tool's shipped fixtures or small synthetic/open-access data.
- **Tutorials:** runnable, reproducible end-to-end tutorials (notebook or script) with a pinned
  environment, that execute on open-access/synthetic data and carry the mandatory data-provenance
  and "research/education use, not medical advice" header.
- **Project infrastructure for the above:** the contribution gate, the doc/test/tutorial
  templates, the reproducible-environment recipe and CI harness, and the candidate-software
  catalog + triage.

**Out of scope**
- Medical advice, clinical interpretation, diagnosis/treatment, or any patient-facing content.
- Controlled-access or patient-identifiable data; redistribution of any dataset; shipping
  non-redistributable data (COSMIC/OncoKB content) in artifacts.
- Feature work, behavior changes, algorithmic fixes, performance refactors, dependency bumps
  beyond what a tutorial/test pins.
- Tools that are not genuinely open-source, are unmaintained/abandoned, or primarily serve a
  for-profit product.
- Contributing under a CLA that assigns broad copyright/patent rights in a way incompatible with
  Hee-Lee Oss's public-good stance (escalated, see gate).
- Standing up or running cancer analysis pipelines as a service; we contribute artifacts, we do
  not operate infrastructure.

## Solution approach & architecture

This is a **software-contribution project with light shared tooling** (templates + a reproducible
environment harness + a triage gate). It contributes to *other people's* repositories; it does
not build or host a product.

**Per-contribution pipeline**
1. **Triage & gate** — identify the target tool, its license, contribution policy (CLA/DCO,
   contributing guide, code of conduct), maintenance status, and whether it is primarily a
   for-profit vehicle. Identify the specific gap and a realistic acceptance path (an accepted
   issue or a self-serve fallback). For any example/tutorial data, run the cancer-data guardrail
   (open-access? aggregate/de-identified? license permits use/redistribution-in-artifact?
   provenance?). PASS only if tool-license + contribution-policy + data-guardrail all clear.
   Record the decision as a committed artifact.
2. **Issue-first alignment** — confirm with the maintainer (via an existing/"good first issue" or
   a new issue) that the contribution is wanted and the approach is acceptable, before writing it.
3. **Author** — write the docs/tests/tutorial against the templates, using the tool's shipped
   example data, small synthetic data, or a license-verified open-access dataset (in that
   priority order). Every biological/clinical assertion carries a citation.
4. **Reproduce** — pin the environment (lockfile/container, tool version), run the tutorial/tests
   end-to-end in the project's CI harness; capture the run as evidence.
5. **Review** — License + Data-provenance reviewer (blocking), Technical reviewer (code/tests/CI),
   and a Domain reviewer for any biological/clinical claim (medium-risk path).
6. **Contribute & confirm** — open the PR upstream (DCO-signed, following the tool's guide); the
   Steward shepherds it to merge and records the acceptance evidence artifact.

**Canonical contribution model.** A single internal object per contribution is the source of
truth; the gate artifact, the PR, and the outcome record are projections of it. Fields:
`id`, `targetTool {name, repo, license, ecosystem, contributionPolicy {cla, dco, guideUrl},
maintenanceStatus, forProfitVehicle:boolean}`, `contributionType {docs|tests|tutorial}`,
`gap {description, issueUrl}`, `exampleData {kind: shipped|synthetic|open-access, source, license,
openAccessTier, permitsArtifactRedistribution:boolean, deIdentified:boolean, provenanceRef}`,
`claims[] {assertion, citation}`, `disclaimerIncluded:boolean`, `reproEnv {toolVersion, lockfile,
container, ciRunRef}`, `review {licenseData, technical, domain}`, `acceptance {channel, prUrl,
mergeCommit}`, `coverage {docBefore, docAfter, testBefore, testAfter}`.

**Reproducible-environment harness.** Because cancer tools are notoriously version-sensitive,
every tutorial/test ships a **pinned environment** — a `conda-lock`/`pixi`/`renv.lock` (or
`requirements.txt`+hashes) plus, where feasible, a container digest — and a thin CI workflow that
recreates the environment and executes the tutorial/tests headlessly on shipped/synthetic/open
data. "Reproducible" is defined as: a clean machine, given only the lockfile, runs the artifact
to completion with the recorded outputs.

**Tech stack.** TypeScript/ESM + pnpm for any Hee-Lee Oss-side shared tooling (catalog validators,
gate-artifact schema, outcome-ledger helpers), per Hee-Lee Oss conventions. The *contributions
themselves* are authored in the target tool's native language and toolchain (Python/R/Java/Nextflow
etc.) and follow that project's style — we do not impose TypeScript on upstream repos. Tutorials
are Markdown + notebooks/scripts; environments are conda/pixi/renv/Docker as the ecosystem
dictates.

**Key decisions.**
- **Upstream-first, issue-first.** We contribute to the tool's own repo and only after the gap is
  confirmed wanted; we never fork-and-replace or open uninvited large PRs.
- **Data-minimization priority order:** tool-shipped example data ▸ small synthetic data ▸
  license-verified open-access data. Prefer the option with the smallest data-licensing surface.
- **Gate is blocking and committed** as an artifact, not an informal judgement.
- **Docs over behavior:** a test that surfaces a bug is reported upstream as an issue; we never
  change algorithmic behavior to make a test pass.
- **Canonical-model-first** so the gate artifact, PR, and outcome record never drift.

## Data, licensing & compliance

**This is the critical section, and it has two axes** — the *software* license (we contribute
code/docs to someone else's repo) and the *data* license (examples/tutorials use cancer data).
Both are treated conservatively. The cancer-data guardrail governs the second axis and is binding.

### Axis 1 — Software (target tool) licensing & contribution policy
- **Accepted tool licenses (permit our contribution and downstream public benefit):** OSI-approved
  permissive (MIT, BSD-2/3-Clause, Apache-2.0) and OSI-approved copyleft (GPL-2.0/3.0,
  LGPL, AGPL, MPL-2.0). Our contributed code is offered under the **tool's own license** (a
  contribution must match the project it joins); standalone tutorials/docs we author are licensed
  **CC-BY-4.0**, and standalone helper code is **MIT**, except where upstream requires otherwise.
- **Contribution policy check (per tool):** record DCO vs. CLA requirements, the contributing
  guide URL, and the code of conduct. **CLAs that assign broad copyright/patent rights to a
  for-profit are escalated** to governance before any work; a DCO sign-off is the default and
  preferred path.
- **For-profit-vehicle check:** confirm the tool is a genuine public-good open-source project, not
  an open-core funnel whose primary benefit accrues to a company (Good-Deed criterion #3). Record
  the rationale.
- **Excluded:** no license / "all rights reserved" / source-available-but-not-OSI (e.g.
  BUSL/SSPL/"non-commercial" *software* licenses), unmaintained/abandoned projects, and tools
  whose contribution would primarily benefit a for-profit. Flagged and excluded, never guessed.

### Axis 2 — Cancer data used in examples/fixtures/tutorials (BINDING GUARDRAIL)
- **Allowed only:** open-access, aggregate, or de-identified data with a verified license that
  permits the use **and** redistribution-in-artifact where the artifact embeds data. In priority
  order: **(a)** the tool's own **shipped example data** (already license-cleared by the tool —
  strongly preferred, near-zero added surface); **(b)** small **synthetic** data we generate; **(c)**
  a **license-verified open-access public dataset**. Acceptable public sources include open-tier
  **GDC/TCGA** data and **CPTAC open imaging**, **DepMap** (CC-BY-4.0), de-identified open **GEO**
  series (per-series license verified), **cBioPortal** public/aggregate exports, and ICGC/PCAWG
  open-tier — each verified per use.
- **Out of scope, never used:** controlled-access data (**dbGaP, EGA**, controlled-tier GDC,
  individual-level germline/biobank) and any **patient-identifiable** data. These require
  authorized access + IRB and are categorically excluded here.
- **Non-commercial / restricted sources — special handling:** **COSMIC** and **OncoKB** are
  **non-commercial** and have redistribution restrictions. Their *content* is **not** embedded,
  mirrored, or redistributed in any artifact. A tutorial may *document how a user supplies their
  own* COSMIC/OncoKB access (API token / their own download under their own license), but we never
  ship their data. Default disposition: **exclude from embedded data; document-by-reference only**,
  recorded in the gate artifact.
- **De-identification check.** Even within open-access tiers, confirm the data is aggregate or
  de-identified (no direct identifiers, no re-identifiable quasi-identifier combinations, no
  sub-aggregation geolocation tied to individuals). Any signal of identifiability → halt, discard,
  exclude.
- **No data redistribution by default.** Tutorials fetch open data from its authoritative source
  at run time (with the source + license + retrieval cited) or use shipped/synthetic data; we do
  not mirror datasets into the contribution unless the data's license explicitly permits
  redistribution and the upstream project accepts it.

**Provenance model.** Every contribution records: target tool + version, the gap/issue link, the
example-data kind + source URL + license id/URL + a captured license snapshot (committed copy +
SHA-256 + Wayback save URL) where data is referenced, de-identification disposition, and — for
every biological or clinical statement in a doc/tutorial — an inline citation to a primary or
authoritative source. **No assertion ships without provenance.**

**Attribution.** Contributions attribute the tool and any data source per their licenses;
standalone tutorials/docs are **CC-BY-4.0**, standalone helper code **MIT**, and contributed-in-repo
code carries the **upstream project's license**. The "not medical advice / research-education use"
disclaimer is mandatory on every tutorial and any doc that could be read clinically.

## Quality, review & risk gates

**Risk tier: low** for the bulk of the work (developer-facing docs/tests on permissively licensed
tools with shipped/synthetic data). **Medium** for any task whose tutorial/doc makes a
biological/clinical claim requiring domain accuracy, or whose example data needs nuanced
license/de-identification judgement. **High (patient-facing/clinical interpretation) is out of
scope** — such tasks are refused, not gated.

**Required review before a deed is "done":**
- **License + Data-provenance reviewer** (mandatory, every contribution): confirms the tool
  license + contribution policy permit the work, the for-profit-vehicle check passed, the
  cancer-data guardrail is satisfied (allowed source, de-identified, no COSMIC/OncoKB content
  embedded), provenance recorded. **Blocking gate** — must be filled before the pilot is reviewed.
- **Technical reviewer:** confirms docs are accurate, tests are meaningful, and the tutorial/tests
  **run reproducibly in CI from the pinned environment** (CI green is real because the harness
  executes the artifact).
- **Domain reviewer (bioinformatician/computational-biologist; oncologist where clinical context
  appears):** required for any task carrying a biological/clinical claim; verifies correctness and
  that nothing constitutes medical advice. Escalates the task to `riskTier: medium`.

**Reproducibility evidence (so "CI green" means something).** Each tutorial/test contribution
ships its pinned environment (lockfile/container digest) and a CI run that recreates the
environment and executes the artifact end-to-end on shipped/synthetic/open data; the CI run
reference is recorded in the contribution's `reproEnv.ciRunRef`. A tutorial that cannot be run
headlessly from its lockfile is not "done".

**Definition of Shipped.** The contribution is **merged upstream** (or accepted by the maintainer
via a written confirmation for non-GitHub channels), the tutorial/tests **run reproducibly in
CI**, the cancer-data guardrail and provenance are satisfied with the gate artifact committed, and
the Steward has recorded the acceptance evidence artifact (`outcomes/<task-id>.json`, with
merge-commit URL + coverage before/after). Opening a PR is **not** shipped; merge/acceptance is.

## Roadmap & milestones

**M0 — Foundation & cold-start (thin)**
- Goal: build the shared tooling (gate, templates, reproducible-environment harness), seed the
  candidate-software catalog, secure the blocking reviewer, and prove the end-to-end flow with one
  merged contribution; begin issue-first maintainer outreach.
- **Cold-start de-risking (pilot selection).** To avoid producing work nothing accepts, the pilot
  targets a tool that is (a) clearly OSI-permissive (MIT/BSD/Apache), (b) actively maintained with
  a published contributing guide and DCO (not a broad-CLA), (c) has a maintainer-labelled
  "good first issue"/"docs/tests wanted" gap, and (d) needs **only shipped or synthetic data** (no
  external dataset). This maximizes the chance of a real *merged* outcome in M0.
- Exit criteria: (1) contribution + cancer-data gate checklist published and applied to the pilot;
  (2) doc/test/tutorial templates + canonical contribution model published; (3) reproducible
  environment recipe + CI harness working on one tutorial; (4) candidate-software catalog seeded
  and triaged (≥ 10 entries license-classified); (5) **License + Data-provenance reviewer named**
  (blocking role filled before pilot review); (6) one contribution **merged upstream** end-to-end
  with the acceptance evidence artifact recorded — or, if no merge materializes, **submitted** with
  the blocker surfaced; (7) ≥ 1 issue-first maintainer thread opened.

**M1 — Gate hardened + first merges**
- Goal: make the gate rigorous and get real contributions merged.
- Exit criteria: (1) gate codified as a reviewable artifact and applied to ≥ 3 contributions;
  (2) ≥ 3 contributions merged across ≥ 2 tools; (3) ≥ 1 confirmed upstream maintainer partner;
  (4) license-snapshot capture working for any referenced data source; (5) the Domain-reviewer
  path exercised on ≥ 1 medium-risk contribution carrying a biological claim.

**M2 — Reproducible tutorials & scale**
- Goal: scale tutorials and tests with the reusable harness; demonstrate reproducibility at scale.
- Exit criteria: (1) reproducible-tutorial harness used across ≥ 3 tools, every delivered tutorial
  green in CI from its lockfile; (2) ≥ 6 contributions merged cumulatively across ≥ 3 tools;
  (3) measurable doc/test coverage improvement recorded for ≥ 3 tools (before/after);
  (4) per-contribution effort measurably reduced vs. the M0/M1 baseline median.

**M3 — Reuse outcomes & sustainability**
- Goal: demonstrate downstream reuse and a durable maintenance model.
- Exit criteria: (1) ≥ 3 verifiable external reuse events; (2) ≥ 8 contributions merged
  cumulatively across ≥ 4 tools; (3) documented maintenance/refresh process (tutorials kept
  green as tools release new versions) and a Steward identified for ongoing upstream liaison.

**Scaling via the catalog.** From M1 onward throughput is driven by triaging entries from the
candidate-software catalog (TASKS.md) through the gate into per-tool contribution tasks. The
catalog is the funnel; the gate is the filter. Targets: M1 ≥ 5 tools triaged (gate artifact each),
≥ 3 merged; M2 ≥ 10 triaged cumulatively, ≥ 6 merged; M3 ≥ 15 triaged cumulatively, ≥ 8 merged
across ≥ 4 tools and ≥ 3 ecosystems (genomics / imaging / survival-stats) to show breadth.
Dependencies: M1 depends on M0 tooling; M2 depends on M1's gate + harness; M3 depends on a body of
merged work from M1–M2.

## Work breakdown

The itemized, schema-mapped backlog lives in `TASKS.md`, organized by the milestones above, each
with a task table (`ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer`),
acceptance criteria for the most important tasks, and a milestone Definition of Done. `TASKS.md`
also carries the **candidate-software catalog** (license-classified, with a triage task and
concrete example per-tool contribution tasks citing real tools), a backlog of sized-but-unscheduled
tasks, and one complete schema-valid example Task JSON.

## Governance, roles & stakeholders

- **Maintainer (Owner):** TBD — owns the shared tooling, the catalog, triage, and the backlog.
- **License + Data-provenance reviewer:** TBD (name TO BE SECURED) — mandatory, **non-skippable**
  gatekeeper for both license axes and the cancer-data guardrail; no deed ships without this
  sign-off. Filled **before the M0 pilot is reviewed** (blocking prerequisite, not a parallel
  hire). Must be able to read OSS licenses (SPDX, GPL/LGPL/AGPL/MPL/MIT/BSD/Apache), assess
  CLA/DCO terms, and apply the cancer-data guardrail (open-access tiers, de-identification,
  COSMIC/OncoKB restrictions). May rotate among ≥ 2 qualified reviewers, but ≥ 1 must always exist
  or triage halts. Until named, all tasks remain `verifiedNeed: false` and nothing passes the gate.
- **Technical reviewer(s):** rotation of contributors who verify docs accuracy, test quality, and
  that the tutorial/tests run reproducibly in CI.
- **Domain reviewer(s):** credentialed bioinformatician/computational biologist (and an oncologist
  where any clinical context appears) engaged per-task for biological/clinical claims (medium-risk).
- **Steward (last-mile owner):** TBD — owns the relationship with upstream maintainers and confirms
  merge/acceptance (the "delivered" signal); records outcome artifacts. Critical because Definition
  of Shipped is acceptance, not PR-opened.
- **Partner / requestor:** TO BE SECURED — named upstream maintainer(s)/communities.

## Dependencies & integrations

- **Upstream OSS projects** (target tools) — their repos, CI, contributing guides, CLAs/DCOs, and
  release cadences. We depend on their review throughput for the "merged" outcome.
- **Environment/repro tooling:** conda/conda-lock, pixi, mamba, Docker/OCI, `renv` (R), Python
  venv + hashes; CI (GitHub Actions or the tool's CI).
- **Coverage/doc tooling:** `interrogate`/`pydocstyle`/`coverage.py` (Python), `covr`/roxygen2/
  `tools::undoc` (R), and equivalents per ecosystem — for before/after measurement.
- **Data sources (referenced, never mirrored by default):** open-tier GDC/TCGA, CPTAC open imaging,
  DepMap, de-identified open GEO, cBioPortal public exports, ICGC/PCAWG open-tier. COSMIC/OncoKB
  are document-by-reference only.
- **Hee-Lee Oss pieces:** Task JSON schema (`packages/schema`), the donated-lane CLI workspace/PR flow
  (`packages/cli`), the good-deed definition + refusal guardrails. No funded-lane/runner
  dependency (this project is donated lane).

## Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
| --- | --- | --- | --- | --- |
| Contribution rejected/ignored by upstream → produced but never merged (fails "delivered") | Medium | High | Issue-first alignment before authoring; pick maintained tools with "good first issue"; Steward shepherds; `verifiedNeed:false` until agreed | Steward |
| Example/tutorial data turns out controlled-access or non-redistributable | Low | High | Cancer-data guardrail as blocking pre-step; prefer shipped/synthetic data; COSMIC/OncoKB document-by-reference only; exclude on any doubt | License+Data reviewer |
| Tutorial/doc makes an incorrect biological/clinical claim | Medium | High | Domain reviewer required for any claim; provenance/citation on every assertion; escalate to medium risk | Domain reviewer |
| Work drifts into medical advice / clinical interpretation | Low | High | Explicit non-goal; mandatory "not medical advice" disclaimer; refuse-and-flag; patient-facing is out of scope | License+Data reviewer |
| Tool license incompatible / restrictive CLA / open-core for-profit vehicle | Medium | Medium | Contribution-policy + for-profit-vehicle checks in the gate; escalate broad CLAs to governance; exclude non-OSI | License+Data reviewer |
| Tutorial bit-rots when tool/data releases a new version | High | Medium | Pinned env (lockfile/container) + CI that runs the artifact; maintenance/refresh process (M3) | Maintainer |
| Reproducibility theatre — "CI green" without actually running the artifact | Medium | Medium | Harness executes the tutorial/tests end-to-end; reproEnv.ciRunRef recorded; no green-on-lint-only | Technical reviewer |
| Test surfaces a real bug; pressure to "fix" behavior out of scope | Medium | Low | Docs/tests-only scope; report bug upstream as an issue; never change algorithmic behavior | Maintainer |
| Single-reviewer bottleneck on the blocking gate | Medium | Medium | ≥ 2 qualified License+Data reviewers in rotation; triage halts rather than skipping the gate | Maintainer |

## Security & privacy

- **Threat surface is small** (no runtime service, no data hosting). Main surfaces are CI and the
  contributions we publish into others' repos.
- **Secrets handling:** contributions require no credentials by default. If a tutorial demonstrates
  an API needing a token (e.g. OncoKB/GDC), the token is supplied by the *user* at run time and is
  **never** committed, logged, or embedded — the tutorial uses environment variables/placeholders
  and documents how the user obtains their own access under their own license (per Hee-Lee Oss rules).
- **PII / patient data:** the dominant privacy concern is upstream cancer data. Handled by the
  cancer-data guardrail: only open-access/aggregate/de-identified data, never controlled-access or
  identifiable patient data, never embedded COSMIC/OncoKB content. We do not download, store, or
  process controlled or identifiable data.
- **Supply-chain:** pinned, hash-locked environments reduce the risk of a tutorial pulling a
  compromised dependency; lockfiles are reviewed; we do not add dependencies to upstream beyond
  what a test/tutorial genuinely needs.
- **Abuse/misuse prevention:** refuse and flag any task steering the work toward de-identification
  reversal, surveillance, clinical advice, weaponizing a tool, or laundering controlled/non-open
  data as open. Contributions stay descriptive, source-verified, and research-facing.

## Sustainability & maintenance

- **Post-delivery ownership:** upstream maintainers own merged contributions going forward; the
  Steward maintains the relationships; the Maintainer keeps the templates, gate, and
  reproducible-environment harness current.
- **Refresh / anti-bit-rot:** because tutorials pin tool/data versions, a tool release can break
  them. A documented refresh process re-runs delivered tutorials against new tool releases on a
  cadence; breakages become `type: maintenance` tasks. Lockfiles + CI make staleness detectable.
- **Outcome tracking:** the Steward records merges and external reuse events against the success
  metrics in the outcome ledger; reviewed each milestone.

## Open questions

- Which specific upstream maintainer(s)/communities will be the first confirmed partner(s)?
- Default disposition for COSMIC/OncoKB is "document-by-reference, never embed" — is any narrow
  exception (e.g. a maintainer who already redistributes under their own non-commercial agreement)
  ever acceptable, or always exclude? (Default: exclude/escalate.)
- For copyleft tools (GPL/AGPL), do we ever author a *standalone* companion tutorial under CC-BY
  outside the repo, or always contribute in-repo under the tool's license? (Default: in-repo.)
- What is the bar for a "verifiable external reuse event" for a tutorial/doc?
- How do we handle a tool whose CI we cannot run our reproducibility check in — host a mirror CI
  in the Hee-Lee Oss project repo, or require the upstream CI to run it?
- Synthetic cancer data for tutorials: do we generate it ad hoc per tutorial, or coordinate with
  the `synthetic-cancer-data` portfolio project for a shared, license-clean fixture set?

## References

- Hee-Lee Oss work rules — `C:\code\hee-lee-oss\CLAUDE.md`
- Good Deed Definition + risk tiers — `C:\code\hee-lee-oss\docs\good-deed-definition.md`
- Task JSON schema — `C:\code\hee-lee-oss\packages\schema\src\schemas.ts`
- Portfolio roadmap (Track 8 cancer guardrails) — `C:\code\hee-lee-oss\planning\ROADMAP.md`
- Companion plan style reference — `C:\code\hee-lee-oss\planning\projects\open-data-datasheets\PLAN.md`
- GDC Data Access (open vs. controlled tiers); dbGaP / EGA controlled-access policy
- TCGA / CPTAC open-access imaging; DepMap (CC-BY-4.0); GEO; cBioPortal; ICGC/PCAWG open-tier
- COSMIC license (non-commercial); OncoKB terms of use (non-commercial / API license)
- Datasheets-style provenance; SPDX license list; OSI-approved license list; Developer Certificate
  of Origin (DCO)

## Appendix A — Improvements applied

The following 25 specific improvements were identified during planning and **have been applied**
to this PLAN and to `TASKS.md` (not left as suggestions). Each cites where it now lives.

1. **Two-axis licensing model made explicit** — separated *software* license from *data* license
   in "Data, licensing & compliance"; both have their own accepted/excluded lists, because
   conflating them is the most likely failure mode for a code-contribution project.
2. **Cancer-data guardrail promoted to the doc header** and made binding, so no reader can miss
   the open-access-only / no-controlled-data / no-advice / provenance rules.
3. **Data-minimization priority order** (shipped ▸ synthetic ▸ open-access) added as a key
   decision and to the gate, shrinking the data-licensing surface to near-zero for most tasks.
4. **COSMIC/OncoKB explicitly handled** as non-commercial "document-by-reference, never embed",
   rather than vaguely "verify license" — turning a known trap into a fixed rule.
5. **"Delivered = merged upstream"** wired through Success metrics, Definition of Shipped, and the
   Steward role, so opening a PR never counts as done.
6. **Issue-first contribution rule** added (gate step 2 + non-goal "no uninvited large PRs") to
   raise the merge rate and respect maintainer norms.
7. **Reproducible-environment harness** elevated to a first-class component with a concrete
   definition ("clean machine + lockfile runs the artifact to completion"), defeating tutorial
   bit-rot and "reproducibility theatre".
8. **CI must execute the artifact**, not just lint — encoded in Quality gates and a dedicated risk
   row, so "CI green" is meaningful.
9. **For-profit-vehicle check** added to the gate (Good-Deed criterion #3) to avoid laundering
   open-core marketing as a good deed.
10. **CLA-vs-DCO handling** specified, with broad-CLA escalation to governance — a real blocker for
    cancer tools backed by companies/institutions.
11. **Docs/tests-only scope hardened** with the "a test reveals a bug → report upstream, never
    change behavior" rule (non-goal + risk row), preventing scope creep into feature work.
12. **Patient-facing/clinical content declared out of scope entirely** (not merely gated as high),
    matching the "low risk" framing while honoring the refusal guardrails.
13. **Domain-reviewer path** added for biological/clinical claims, with explicit risk-tier
    escalation to medium and a provenance-on-every-assertion rule.
14. **Measurable coverage deltas** defined (docstring coverage %, test coverage delta, closed
    "docs needed" issues) with named tooling per ecosystem, so "improved docs" is quantifiable.
15. **Outcome-evidence artifacts** (`outcomes/<task-id>.json` with merge-commit URL + before/after
    coverage) made mandatory and assigned to the Steward.
16. **License-snapshot capture** (committed copy + SHA-256 + Wayback URL) reused from the
    open-data-datasheets pattern for any referenced data source.
17. **Candidate-software catalog** added (license-classified, priority A/B/C) so throughput is
    transparent and the pool is honestly triaged, not cherry-picked.
18. **Blocking reviewer sequencing** — the License+Data reviewer must be named before the pilot is
    reviewed, and is a real prerequisite dependency on the pilot task, not a parallel nicety.
19. **Multi-ecosystem breadth target** (genomics / imaging / survival-stats, ≥ 3 ecosystems by M3)
    so the project proves general value, not one-tool luck.
20. **Secrets/API-token discipline** for tutorials (env-var placeholders, user supplies own token,
    never committed) added to Security & privacy.
21. **Supply-chain mitigation** via hash-locked environments added to Security & privacy.
22. **Reviewer-bottleneck risk** addressed with ≥ 2 rotating qualified License+Data reviewers and
    "halt rather than skip".
23. **Anti-bit-rot maintenance process** (re-run tutorials against new tool releases on a cadence;
    breakages become maintenance tasks) added to Sustainability.
24. **Honest `verifiedNeed: false`** everywhere until a named maintainer agrees, with a clear flip
    condition — matching Hee-Lee Oss's "delivered, not merged" honesty bar.
25. **Cross-project coordination** flagged (synthetic fixtures via `synthetic-cancer-data`; tool
    overlap with `ml-oncology-benchmarks`, `ewing-fusion-detection-benchmark`,
    `pathology-image-benchmarks`) in Open questions/References to avoid duplicated effort.

## Review sign-off

**Reviewed for completeness and correctness against the PLAN_SPEC (17 required sections),
CLAUDE.md, the good-deed definition, and the Track 8 cancer guardrails.**

- **Section completeness:** all 17 required H2 sections present and in order; the data/licensing
  section leads its content with the binding cancer guardrails. ✔
- **Guardrail correctness:** open-access/aggregate/de-identified-only enforced; dbGaP/EGA/
  controlled-tier explicitly excluded; COSMIC/OncoKB handled as non-commercial document-by-reference;
  no medical advice / patient-facing out of scope; provenance required on every assertion. ✔
- **"Delivered, not merged":** Definition of Shipped = merged/accepted upstream + reproducible CI +
  recorded evidence; vanity metrics excluded. ✔
- **Lane/conventions:** donated lane (no funded budget); Hee-Lee Oss-side tooling TS/ESM/pnpm; DCO
  sign-off; CC-BY-4.0 docs / MIT helper code / upstream-license for in-repo code. ✔
- **Honesty:** partner/requestor and per-task `verifiedNeed` are `TO BE SECURED`/`false` until a
  named maintainer agrees; blocking reviewer role flagged as unfilled. ✔
- **Fixes applied during review:** (a) clarified that contributed in-repo code takes the upstream
  project's license while standalone docs are CC-BY-4.0 / helper code MIT (removed an earlier
  ambiguity that implied all code is MIT); (b) made the License+Data reviewer a hard dependency of
  the pilot task in TASKS.md rather than a parallel task; (c) tightened the COSMIC/OncoKB rule from
  "verify" to "never embed, document-by-reference" consistently across PLAN and TASKS; (d) added the
  Domain-reviewer to the pilot's reviewer set only if it carries a biological claim (the pilot is
  chosen to avoid one, keeping it `low`).

**Outstanding items requiring a human decision** (also in Open questions): naming the first upstream
partner and the License+Data reviewer; the COSMIC/OncoKB narrow-exception policy; and whether to
share synthetic fixtures with `synthetic-cancer-data`. None block M0 foundation work; all block the
*acceptance* steps, which is correctly reflected by `verifiedNeed: false`.
