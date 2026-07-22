# Competitive & Improvement Analysis — `onco-research-software-docs`

> Scope: Hee-Lee Oss donated-lane project contributing documentation, runnable tutorials, and test
> coverage **upstream** to widely-used, genuinely open-source cancer-research software. Low risk.
> Analysis date: 2026-06-29. Sources are inline as URLs.

---

## 1. Correctness & completeness review of PLAN.md

The plan is unusually strong and self-aware: it already separates the two licensing axes
(software vs. data), promotes the cancer-data guardrail to a binding header, defines "delivered =
merged upstream," and carries an honest `verifiedNeed: false` until a named maintainer agrees. The
Appendix-A "25 improvements applied" shows real iteration. The findings below are gaps that remain
or that the current environment (mid-2026) makes more acute.

**Strong / correct as written**
- **Target selection / prioritization** is sound: the candidate-software catalog with A/B/C
  license triage, the data-minimization priority order (shipped ▸ synthetic ▸ open-access), and
  the multi-ecosystem breadth target (genomics / imaging / survival-stats by M3) prevent
  one-tool luck and cherry-picking.
- **Maintainer coordination / CLA-DCO norms** are handled: issue-first alignment is a gate step
  and a non-goal ("no uninvited large PRs"); broad-CLA escalation to governance; for-profit-vehicle
  check. This is the single most important correctness property given the 2026 environment (see §2).
- **Tests not breaking things**: the "a test that surfaces a bug → report upstream, never change
  behavior" rule is explicit and correctly scoped.
- **Measuring impact**: outcome-based metrics with externally-verifiable reuse, coverage deltas
  via named tooling (`interrogate`/`coverage.py`/`covr`), and exclusion of vanity metrics.

**Findings — most material first**

1. **(HIGH) The "AI-generated PR slop" reception risk is under-weighted and not differentiated in
   the contributor identity.** The plan's risk table lists "contribution rejected/ignored" as
   Medium likelihood, but the 2026 reality is that maintainers are actively hostile to *unsolicited
   AI-authored* docs/test PRs — Jazzband shut down, curl killed its bug bounty over "AI slop," Godot
   maintainers call triage "demoralizing" (see §2). Issue-first alignment mitigates this, but the
   plan does not require **disclosing AI authorship**, does not propose **batching/consolidating**
   contributions to reduce maintainer triage load, and does not set an explicit **per-maintainer
   rate limit**. Without these, the project risks becoming exactly the slop it should avoid. This
   is the dominant existential risk and deserves promotion to a first-class design constraint, not
   a single risk row.

2. **(HIGH) Docs-accuracy verification leans on human review but lacks a mechanized "executable
   docs" requirement for non-tutorial docs.** Tutorials must run in CI (good). But docstrings,
   parameter docs, and API references — the highest-volume contribution type — have no equivalent
   forcing function; they rely on the Technical reviewer's eye. Given documented LLM API-doc
   hallucination rates (GPT-4o ~38% valid low-frequency API calls; non-existent parameters that
   pass linters; docstring/code mismatch), every API claim should be mechanically grounded:
   **doctest execution, signature/`__doc__` introspection diffing, or static AST checks** that the
   documented parameters/return types actually exist. The plan should make "no API assertion ships
   without a machine check that the symbol/parameter exists and behaves as documented" a gate item.

3. **(MED) "Actively maintained" is asserted but not operationalized.** The gate records
   `maintenanceStatus` but gives no threshold (e.g., commit/release recency, median PR-merge latency,
   number of active maintainers). Without a concrete liveness test the project can sink effort into
   tools whose review throughput is too slow to ever reach "merged," silently failing the delivery
   bar. Define a measurable maintenance/responsiveness screen in triage.

4. **(MED) Scope realism on cadence vs. review throughput.** Targets (≥8 merged across ≥4 tools in
   6 months) depend entirely on *other people's* review queues — a dependency the plan acknowledges
   but does not buffer. There is no fallback "self-serve acceptance" definition that counts when a
   maintainer is slow but the tool has a docs site the contribution can land in (e.g., a wiki, a
   `CONTRIBUTING`-sanctioned examples gallery). Consider a tiered acceptance definition.

5. **(MED) "Not stepping on maintainers" / sustainability of relationships.** The Steward role is
   well-conceived, but the plan has no **maintainer-burden budget** (how many open threads per
   maintainer at once) and no **graceful-exit** rule when a maintainer signals fatigue. Add an
   explicit "if a maintainer declines or goes quiet, we stop and do not re-litigate" norm.

6. **(LOW/MED) Synthetic cancer data accuracy.** Option (b) "small synthetic data we generate" is
   attractive for zero data-licensing surface, but synthetic genomic/expression data can be
   biologically implausible and produce *misleading* tutorials (wrong distributions, impossible
   variant patterns). The plan flags coordination with `synthetic-cancer-data` as an open question
   but should require a domain-reviewer pass on any synthetic fixture used in a *biological* tutorial.

7. **(LOW) Attribution / provenance of the AI contribution itself.** The plan mandates attribution
   of tools and data sources, and DCO sign-off, but does not address how DCO sign-off interacts with
   AI-assisted authorship (who certifies origin). Worth a one-line policy: a human contributor signs
   the DCO and takes responsibility for the content.

8. **(LOW) Coverage-delta gaming.** "Test coverage delta on touched modules" can be inflated with
   low-value tests. Pair the quantitative delta with the existing Technical-reviewer "tests are
   *meaningful*" check (already present) and state that coverage % alone is never the acceptance bar.

Overall: the plan is **complete against its 17-section spec and internally consistent**; the
binding guardrails (open-access-only data, COSMIC/OncoKB document-by-reference, no medical advice,
provenance-on-every-assertion) are correct and well-placed. The gaps are about **execution in a
hostile-to-AI-PR 2026 environment** and **mechanizing docs accuracy**, not about safety posture.

---

## 2. Competitive landscape

No existing effort does exactly this (organized, AI-accelerated, *upstream* docs/test/tutorial
contributions specifically to open cancer-research software under a hard data guardrail). But
several adjacent programs set the quality bar, define norms, and compete for the same maintainer
attention and "improve scientific OSS" mindshare.

**Bioconductor (documentation standards).** The de-facto standard-setter for R-based genomics/
cancer software. Requires every package to ship ≥1 executable vignette and a man page per exported
function with runnable examples; vignettes must embed *executed* code (no `eval=FALSE` shortcuts)
and are rebuilt/tested several times weekly; `BiocCheck` enforces guidelines mechanically.
Strength: rigorous, executable-docs culture that this project should emulate. Weakness (opportunity
for us): the burden falls on package authors; there is no organized external help corps filling doc
gaps in *existing* packages.
https://contributions.bioconductor.org/docs.html ·
https://www.bioconductor.org/packages/devel/bioc/vignettes/BiocCheck/inst/doc/BiocCheck.html ·
https://www.bioconductor.org/help/package-vignettes/

**Journal of Open Source Software (JOSS).** Peer-reviews the *software* (functionality, docs,
tests, CI, license) plus a short paper with a mandatory "Statement of need" and "state of the
field." Treats an automated test suite + CI as the "good" bar. Strength: a respected, checklist-
driven definition of "well-documented, well-tested OSS" we can align our DoD to, and a venue that
*rewards* maintainers who accept our uplift (a better-documented tool is more JOSS-publishable).
Weakness: one-time gate at publication; no ongoing doc/test contribution mechanism.
https://joss.readthedocs.io/en/latest/review_criteria.html ·
https://joss.readthedocs.io/en/latest/review_checklist.html · https://joss.theoj.org/about

**The Carpentries (Software/Data Carpentry).** Volunteer-instructor model teaching reproducible
computing; the Genomics curriculum covers bioinformatics project organization and command-line/
cloud workflows; adopted at scale by ELIXIR across Europe. Strength: gold standard for *teaching*
reproducibility and a proven volunteer-community model. Weakness/difference: produces standalone
*lessons/workshops*, not upstream contributions to the tools themselves — complementary, not
overlapping. https://carpentries.org/lessons/ · https://datacarpentry.org/lessons/ ·
https://pmc.ncbi.nlm.nih.gov/articles/PMC5516217/

**Open Life Science (OLS / Open Seeds).** 16-week cohort mentorship turning researchers into open-
science project leads (OLS-5 had ~71 participants / 34 projects). Strength: builds *people* and
*projects* and a mentor network we could plug into for domain/maintainer relationships. Weakness:
it mentors project leads; it does not itself ship docs/tests upstream. A natural partner for our
Steward/maintainer-relationship layer. https://we-are-ols.org/openseeds/ ·
https://openlifesci.org/ols-5

**nf-core (docs model).** Strong, template-enforced documentation model for Nextflow pipelines:
all pipelines built from the `nf-core` template, MIT-licensed, docs hosted centrally, `nf-core
lint` enforces standards, mandatory CI tests, automated sync keeps all pipelines current. Strength:
exactly the "reproducible, lint-enforced, template-driven docs" model our harness should imitate;
also a concrete, welcoming contribution target ("improving documentation" explicitly welcomed).
Weakness: scoped to Nextflow pipelines, not the broader tool universe.
https://nf-co.re/docs/contributing/guidelines · https://nf-co.re/docs/contributing/contribute-existing-pipelines

**Google Season of Docs (GSoD).** The closest *programmatic* analog — funded technical writers
paired with OSS orgs (incl. "science and medicine") 2019–2024; 2022 accepted 31 projects / 58
writers. **Critically, the program concluded after 2024.** Strength: validated the "organized
external docs help for OSS" model and leaves 84 public case studies of what works. Weakness / our
opening: **it no longer exists**, leaving a vacated niche for organized docs uplift — and it relied
on scarce paid human writers, exactly the bottleneck AI assistance can relieve.
https://developers.google.com/season-of-docs/ ·
https://opensource.googleblog.com/2024/12/google-season-of-docs-announces-program-results-2024.html

**Scientific-Python / NumPy-SciPy docs efforts.** numpydoc convention + doc sprints set the
docstring standard the Python scientific stack (incl. scanpy/lifelines) follows. Strength: a
ready-made, widely-adopted docstring style to conform to. Weakness: convention-and-sprints, not a
sustained external contribution corps. https://numpy.org/doc/1.19/docs/howto_document.html ·
https://python-sprints.github.io/pandas/guide/pandas_docstring.html

**CZI Essential Open Source Software for Science (EOSS).** Funds *maintenance* of essential
scientific OSS (>$28M committed across cycles; genomics/bioinformatics incl. QIIME2, scikit-learn).
Strength: the money-and-mandate layer for sustaining scientific OSS — a potential *funder/ally*,
not a competitor, and a signal of which tools are "essential" (a ready prioritization list for our
catalog). Weakness: funds maintainers' own work; docs/tests uplift is not its deliverable.
https://chanzuckerberg.com/eoss/proposals/ ·
https://chanzuckerberg.com/newsroom/czi-awards-16-million-for-foundational-open-source-software-tools-essential-to-biomedicine/

**The defining environmental fact (cross-cutting).** As of 2026, open-source maintainers are
**drowning in AI-generated PRs and security reports**; Jazzband shut down, curl ended its bug
bounty (<5% of reports legitimate, ~20% "AI slop"), Godot maintainers report burnout. Any AI-
accelerated contribution program now operates under a **trust deficit** it must actively overcome.
https://thenewstack.io/ai-generated-code-crisis/ ·
https://www.axios.com/2026/03/10/ai-agents-spam-the-volunteers-securing-open-source-software ·
https://groundy.com/articles/are-ai-generated-prs-killing-open-source/

---

## 3. Gaps we can fill (organized, donated-effort docs/test uplift at scale)

1. **The vacated GSoD niche, but AI-scaled.** GSoD proved organized external docs help works and
   then ended; we can fill it for the cancer-software slice without the paid-human-writer bottleneck.
2. **Existing-package doc/test debt.** Bioconductor/JOSS/nf-core enforce standards *at submission*;
   nobody systematically retro-fits docs/tests into the long tail of already-published, widely-used
   tools. That backlog is our core territory.
3. **Reproducibility rot.** Tutorials that "worked once" and silently broke on version drift —
   our pinned-env + CI-executes-the-artifact harness directly targets this, at scale, across tools.
4. **The "data a newcomer cannot legally obtain" trap.** A huge fraction of cancer tutorials assume
   controlled-access data; converting these to shipped/synthetic/open-tier data is high-value and
   almost nobody does it deliberately.
5. **Cross-tool consistency.** A reusable docstring standard + tutorial template + data-license/"not
   medical advice" header applied across many tools — a uniformity no single project produces.
6. **Mechanized doc-accuracy checks** (doctest/introspection/AST grounding) that most volunteer
   docs efforts skip — turning AI's weakness (hallucinated APIs) into a verified strength.
7. **Coverage-debt visibility.** Before/after docstring + test-coverage deltas published per tool —
   a transparency artifact ecosystems lack.

---

## 4. Differentiators to win

1. **Trust-first contribution protocol in a slop-flooded world.** Issue-first, maintainer-invited,
   AI-authorship disclosed, every artifact CI-executed and provenance-stamped — the *opposite* of
   the unsolicited AI-PR flood maintainers now reject. Our credibility *is* the moat.
2. **"Delivered = merged/accepted upstream," not PR-opened.** We are measured on outcomes the
   maintainer actually accepted, aligning our incentives with theirs (the inverse of slop farms).
3. **Binding cancer-data guardrail + provenance-on-every-assertion.** A domain-specific safety
   posture (open-access-only, COSMIC/OncoKB document-by-reference, no medical advice) that generic
   docs programs do not have and that maintainers in this sensitive domain will value.
4. **Reproducible-env harness as a reusable asset.** Every contribution ships a lockfile/container +
   CI that re-runs it; "reproducible" has a hard operational definition, defeating bit-rot and
   reproducibility theatre.
5. **Cross-ecosystem breadth with a single quality bar** (genomics/imaging/survival-stats), proving
   general value rather than one-tool luck.

---

## 5. Claude API leverage — and the hard limits

**Where Claude adds the most (with human + machine verification):**
- **Draft docstrings/API reference from source** (signatures, types, params) — then *ground* each
  claim by introspecting `__doc__`/signatures and running doctests; Documentation-Augmented
  Generation measurably reduces API hallucination, so feed Claude the actual symbol table, never
  let it invent. https://arxiv.org/abs/2407.09726
- **Doc-gap detection at scale:** scan a repo for undocumented exported symbols, stale examples,
  params present in code but absent in docs, and tutorials depending on controlled data — produce a
  prioritized, license-classified candidate catalog (feeds triage).
- **Tutorial/example generation** from a tool's shipped example data, including the mandatory
  data-provenance + "not medical advice" header, with a pinned environment scaffold.
- **Test scaffolding:** propose unit/golden/doctests for under-covered modules using shipped
  fixtures; surface (not fix) suspected bugs as upstream issues.
- **Docstring/code mismatch detection** and consistency cleanup to a chosen standard (numpydoc/
  roxygen/Bioc).
- **Maintainer-thread drafting:** issue-first messages, changelog/PR descriptions, AI-authorship
  disclosure boilerplate.

**Where Claude must NOT decide (hard gates):**
- **Technical accuracy is never accepted on Claude's say-so.** Every documented API behavior must
  be verified by *running the code* (doctest/CI) and/or AST/introspection grounding; LLMs
  confidently emit non-existent params that pass linters. https://arxiv.org/html/2409.20550v1
- **No fabricated API behavior, return values, or biological/clinical claims.** Every biological/
  clinical assertion requires a primary-source citation and Domain-reviewer sign-off (medium-risk
  path); unverified claims do not ship.
- **License/CLA acceptability and for-profit-vehicle judgement** stay with the License+Data
  reviewer, not Claude.
- **Maintainer consent and "is this wanted"** is a human, issue-first decision — Claude drafts,
  humans send and own the relationship.
- **DCO sign-off / responsibility** is a human's certification of origin; Claude does not "sign."
- **Cancer-data de-identification / redistribution calls** (especially COSMIC/OncoKB) are reviewer
  decisions, not model decisions.

---

## 6. Ten concrete optimizations

1. **Add an explicit "AI-authorship disclosure + maintainer-burden" protocol**: disclose assistance
   in every issue/PR, cap concurrent open threads per maintainer, batch related fixes, and stop on
   any decline/silence. Promote from a risk row to a binding design constraint (addresses §1.1).
2. **Make docs accuracy mechanically grounded**: require doctest execution + signature/`__doc__`
   introspection diffing (or AST symbol checks) for every API assertion, not just tutorials
   (addresses §1.2). Bake into the gate and CI harness.
3. **Operationalize "actively maintained"** with a concrete liveness screen (release/commit recency,
   median merge latency, ≥N active maintainers) computed during triage (addresses §1.3).
4. **Define a tiered acceptance ladder** (merged ▸ maintainer-written-accept ▸ sanctioned self-serve
   docs surface) so slow review queues don't auto-fail delivery, while still excluding "PR-opened"
   (addresses §1.4).
5. **Conform to each ecosystem's native standard** out of the box: numpydoc for Python, roxygen2 +
   `BiocCheck` for R/Bioconductor, nf-core template/lint for Nextflow — encode as per-ecosystem
   templates so contributions look native and pass lint first try.
6. **Seed the catalog from CZI-EOSS "essential" lists and JOSS-published tools** as a credibility-
   weighted prioritization signal, intersected with the license gate.
7. **Ship a `BiocCheck`/`interrogate`/`covr` before-after badge artifact** per contribution to make
   coverage deltas auditable and resistant to gaming (pair with "meaningful tests" review).
8. **Require Domain-reviewer sign-off on any synthetic biological fixture**, and prefer coordinating
   shared license-clean fixtures via `synthetic-cancer-data` over ad-hoc generation (addresses §1.6).
9. **Build a reusable "controlled-data → open/synthetic data" tutorial-conversion playbook** — one
   of the highest-value, lowest-risk contribution patterns, packaged for repeat use.
10. **Publish a public "how we contribute responsibly" charter** (trust-first, outcome-measured,
    guardrailed) so maintainers can vet us *before* the first issue — directly countering the AI-PR
    trust deficit (§2).

---

## 7. Parallel & perpendicular spin-offs

- **`ewing-reproducibility` / `ewing-fusion-detection-benchmark`:** the reproducible-env harness and
  "tutorial runs end-to-end in clean CI" capability are directly reusable; a documented, reproducible
  fusion-detection tool tutorial doubles as a reproducibility artifact.
- **`reproducibility-curriculum` / `bioinformatics-from-zero`:** our reproducible tutorials and
  data-minimization patterns are teaching assets; conversely, Carpentries/OLS-style curricula can
  consume our upstream-landed tutorials as canonical examples — a two-way feed.
- **`lab-protocols-open`:** shared "provenance + not-medical-advice header" and open-licensing
  discipline; protocols and software tutorials can share the same provenance/attribution tooling.
- **`synthetic-cancer-data`:** the natural supplier of license-clean synthetic fixtures (open
  question in the plan); formalize a shared fixture set to kill per-tutorial synthetic-data risk.
- **A reusable OSS-docs-uplift *program*** (domain-agnostic): the gate + templates + harness +
  trust-first protocol generalize beyond oncology — a "post-GSoD, AI-scaled, responsibly-run docs
  corps" that could later cover other scientific domains under the same playbook.
- **An MCP server**: expose the doc-gap detector, license/data-guardrail classifier, repro-env
  scaffolder, and docstring-grounding checks as MCP tools so any Claude agent (or maintainer) can
  run "scan this repo for doc/test gaps and produce a gated, provenance-stamped contribution draft"
  on demand — turning the harness into reusable infrastructure.

---

## 8. Open questions

1. **AI-authorship disclosure policy:** exactly how/where do we disclose, and do we pre-register
   with maintainers before opening any thread? (Strongly recommended given the 2026 trust deficit.)
2. **Maintainer-burden budget:** how many concurrent open threads per maintainer/tool is acceptable,
   and what is the graceful-exit rule on decline/silence?
3. **Acceptance-tier definition:** does a sanctioned self-serve docs surface (wiki, examples gallery)
   count as "delivered" when a maintainer is slow, or only a merge/written-accept? (Plan currently
   says merge/accept only.)
4. **Docs-accuracy mechanization bar:** is doctest/CI execution *mandatory* for every API doc, or
   only where feasible? Where it is infeasible (compiled/GPU/imaging tools), what substitutes?
5. **Synthetic-data sourcing:** ad-hoc per tutorial vs. shared `synthetic-cancer-data` fixtures —
   and who domain-reviews biological plausibility? (Plan's existing open question; sharpen.)
6. **Catalog prioritization signal:** do we formally seed from CZI-EOSS/JOSS lists, and how do we
   avoid over-concentrating on already-well-resourced "essential" tools vs. the neglected long tail?
7. **First confirmed maintainer partner + License+Data reviewer** (plan's blocking unknowns) — both
   gate *acceptance*, not foundation work; who and when?
8. **COSMIC/OncoKB narrow-exception policy** (plan open question): always exclude, or allow a
   maintainer who already redistributes under their own non-commercial agreement? Default: exclude.
