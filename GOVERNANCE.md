# MuslimOSS — Governance

**Status:** Foundational document — v1.0
**Applies to:** All repositories under the `muslimoss` GitHub organization, unless a repository explicitly states an exception (e.g., a vendored third-party project retained under its original governance).

This document defines how decisions are made in MuslimOSS: who holds authority, how that authority is earned and lost, how repositories move through their lifecycle, and how we draw the line between technical decisions and religious ones. It exists so that MuslimOSS can outlive any single contributor — including its founder.

---

## 1. Purpose

Open-source projects fail most often not from lack of code, but from unclear decision-making — disputes with no resolution path, maintainers who can't be replaced, or scope that drifts because no one had the authority to say no. This document exists to prevent all three, deliberately modeled on governance structures that have kept large foundations (Python Software Foundation, Rust Foundation, Apache Software Foundation) functional across leadership changes spanning decades.

Two things make MuslimOSS's governance slightly different from a purely secular foundation, and both are addressed explicitly below:

1. Some projects touch religious accuracy (Zakat calculation rules, Hijri date determination, Qur'anic text) where a purely engineering decision is not sufficient — this is the reason a **Scholar Advisory Board** exists as a distinct role from **Maintainers** (Section 6).
2. MuslimOSS is, as of this document's writing, a founder-led organization with a small number of active maintainers. Pretending otherwise would be dishonest. Section 9 states the current phase plainly and defines the concrete conditions under which authority transitions to a Steering Committee — this document is written for the organization MuslimOSS will become, but it does not claim powers or structures that don't exist yet.

---

## 2. Principles

| Principle | What it means in practice |
|---|---|
| **Authority is earned through contribution, not granted by title** | You become a maintainer by demonstrably doing maintainer work first (reviewing, triaging, shipping), not by request or seniority elsewhere. |
| **Decisions are documented, not verbal** | Any decision with lasting effect (new repo, maintainer promotion, breaking API change, license change) has a written record — an issue, RFC, or meeting note — that a contributor joining two years later can read and understand. |
| **Lazy consensus by default, escalation is the exception** | Most day-to-day decisions (accepting a PR, fixing a bug, minor doc changes) don't need a vote. Voting exists for the small set of decisions listed in Section 4.2, and using it for everything else would slow the project to a crawl — the same failure mode that makes some corporate open-source projects unpleasant to contribute to. |
| **Religious accuracy is never decided unilaterally by engineering** | No maintainer, however senior, resolves a fiqh question by themselves in code. Section 6 defines exactly how this works. |
| **Removal is possible and not personal** | Maintainers and Scholar Advisory Board members can be removed for inactivity or conduct violations through a defined process (Sections 5.3, 6.4) — this protects the project, not the individual's reputation, and is stated up front so it never feels like a surprise or a personal attack when it happens. |

---

## 3. Roles

| Role | Scope | Who |
|---|---|---|
| **Steering Committee** | Org-wide: final authority on governance changes, new top-level project categories, trademark/brand use, and org-level disputes that can't be resolved at the repository level. | Does not yet exist as a multi-person body — see Section 9. Currently exercised by the Founder. |
| **Founder** | Org-wide, transitional | Mehrab Hossain. Holds Steering Committee authority alone until the transition conditions in Section 9 are met. |
| **Org Maintainers** | Org-wide: can create new repositories under `muslimoss`, manage org-level CI/CD templates, and admin the `.github` repository. | Appointed by the Founder/Steering Committee from among proven Repository Maintainers (Section 5). |
| **Repository Maintainers** | Single repository: merge rights, release authority, triage authority for that repo. | Appointed per-repository, see Section 5. |
| **Scholar Advisory Board** | Advisory, cross-repository: consulted on any change touching religious accuracy or interpretation. No merge rights, no code authority. | See Section 6. |
| **Contributors** | Anyone who opens an issue, submits a PR, improves documentation, or participates in Discussions. | Open to all — see `CONTRIBUTING.md`. |
| **Users** | Anyone running MuslimOSS software. No governance authority, but the primary reason any of this exists. | — |

**Why Org Maintainer is a separate tier from Repository Maintainer:** a contributor can be an excellent maintainer of one focused repository (e.g., `hijri-calendar`) without having the context or track record to make org-wide calls like approving a brand-new top-level project category. Conflating the two tiers — as many smaller projects do by default — either under-empowers good repo maintainers (making them wait on the founder for routine repo decisions) or over-empowers them (giving repo-level trust org-wide authority it wasn't earned for). Separating the tiers avoids both failure modes.

---

## 4. Decision-Making Process

### 4.1 Lazy Consensus (default)

Most decisions — accepting a PR, fixing a bug, updating documentation, routine dependency bumps — are made by **lazy consensus**: a maintainer proposes or merges the change, and it stands unless another maintainer objects within a reasonable review window (typically 48–72 hours for routine changes). No formal vote is needed. This is the same model used by the Apache Software Foundation and most healthy open-source projects, and it exists because requiring a formal vote for every merge would make the project unbearably slow to contribute to.

### 4.2 RFC Process (for significant changes)

The following changes require a written **RFC (Request for Comments)**, posted as a GitHub Discussion or in a dedicated `rfcs` repository once it exists, open for community comment for a minimum of **7 days** before a decision:

- Any breaking API or data-format change in a released (non-incubating) project
- Creating a new top-level project category (e.g., adding "Islamic AI" as a new pillar beyond what's listed in the org's stated scope)
- Adopting or changing a license for an existing repository
- Any change to this governance document
- Any decision explicitly escalated by a maintainer who believes lazy consensus is insufficient for the stakes involved

**Why 7 days minimum:** MuslimOSS's contributor base spans time zones and includes people balancing this with full-time work, study, and — deliberately built into the org's rhythm — daily prayer and other commitments. A 24-hour comment window (common in fast-moving corporate projects) would systematically exclude part-time and international contributors from decisions that affect them.

### 4.3 Voting (fallback when consensus isn't reached)

If an RFC does not reach consensus after the comment period, it goes to a vote among the maintainers with standing on that decision (Repository Maintainers for repo-scoped RFCs; Org Maintainers + Steering Committee for org-wide RFCs). Simple majority decides, with the Steering Committee holding tie-breaking authority. Votes and their rationale are recorded in the RFC thread — a decision without a recorded reason is not considered final and can be reopened.

### 4.4 Religious-Accuracy Decisions Are Excluded From This Process

Any RFC or PR that touches religious accuracy (see Section 6.2 for what qualifies) is **paused** from the normal RFC/voting track the moment it's flagged, and routed to the Scholar Advisory Board process instead. Engineering consensus or majority vote is never used to settle a question of religious accuracy — this is a hard rule, not a default that can be overridden by a large enough majority.

---

## 5. Repository Maintainers

### 5.1 Becoming a Maintainer

There is no application form. The path is:

1. Contribute consistently to a specific repository — code, review, triage, or documentation — over a sustained period (as a guideline, several months of regular, substantive contribution; there is no fixed contribution count, because quality and reliability matter more than volume).
2. An existing maintainer of that repository (or the Founder/Org Maintainers, if the repo has none yet) nominates the contributor publicly, in an issue or Discussion, with specific examples of their contributions.
3. Existing maintainers of that repository reach lazy consensus (Section 4.1) on the nomination. If there are no existing maintainers (new repo), the Org Maintainers decide.

**Why nomination is public and example-based:** private, no-reasoning promotions are how projects end up with maintainers the community doesn't trust and can't understand the selection of. A public record also gives future contributors a clear, honest picture of what "earning maintainership" actually looked like in practice.

### 5.2 Responsibilities

A Repository Maintainer is expected to: review and merge PRs in a reasonable timeframe, triage issues, cut releases following the org's [Semantic Versioning](https://semver.org) and Conventional Commits standards, and respond to security reports per `SECURITY.md`. Maintainership is a responsibility, not a title — inactivity is handled per Section 5.3, not treated as a personal failing.

### 5.3 Inactivity and Removal

- **Inactivity:** A maintainer who has had no repository activity (reviews, merges, triage, or communication) for **90 consecutive days** is contacted directly. If there's no response within **14 days**, they are moved to **Emeritus** status — a respectful, permanent public record of past contribution, with access removed but attribution preserved in the repo's `MAINTAINERS.md`. This is not a punishment; life circumstances change, and the project needs active maintainers to function.
- **Conduct removal:** A maintainer can be removed for Code of Conduct violations following the enforcement process in `CODE_OF_CONDUCT.md`. This is handled separately from inactivity and can happen regardless of how active or valuable the person's technical contributions have been — conduct standards apply uniformly.

---

## 6. Scholar Advisory Board

### 6.1 Why This Role Exists

MuslimOSS builds software that sometimes encodes religious determinations — which calculation method to use for prayer times, how to compute Zakat on different asset types, how a Hijri date is determined for moon-sighting versus calculation-based projects, which Hadith grading conventions to display by default. These are not engineering decisions dressed up as religious ones; they are genuine points of legitimate scholarly difference (*ikhtilaf*), and MuslimOSS as an engineering organization has no standing to resolve them on its own. This is the direct, practical expression of the stated boundary that **MuslimOSS is not a religious authority and does not issue rulings** — it is not just a disclaimer in a README, it is enforced here as a governance mechanism.

### 6.2 What Qualifies as a Religious-Accuracy Decision

As a working guideline (refined over time via RFC as edge cases arise):

- Any default calculation method offered where legitimate scholarly disagreement exists (e.g., prayer time calculation conventions, Zakat nisab thresholds, Hijri date determination method)
- Any text presented as an authoritative religious source (Qur'an text/translation selection, Hadith authentication grading, Tafsir attribution)
- Any feature that could reasonably be interpreted as the software itself issuing a ruling, rather than presenting documented positions from named scholarly sources

A change that merely *implements* an already-documented, cited scholarly position (e.g., adding a second supported calculation method alongside an existing one, both clearly labeled and attributed) is an engineering decision and follows the normal process — the Scholar Advisory Board is consulted on *what the software should present as options and how it labels them*, not on routine implementation.

### 6.3 Composition and Engagement

The Scholar Advisory Board is not a standing employed body — it is a maintained list of qualified scholars (with relevant credentials from recognized Islamic institutes, disclosed publicly in `governance/scholar-advisory-board.md` once established) whom MuslimOSS consults on a per-question basis as religious-accuracy questions arise. The Founder/Steering Committee is responsible for establishing and maintaining these relationships. The Board has **no merge rights and no code authority** — its output is guidance that maintainers are expected to follow when implementing the relevant feature, not a veto exercised through the repository itself.

**Why advisory rather than governance-with-merge-rights:** giving scholars direct merge access would blur engineering review (security, correctness, performance) with religious review, and would put scholars in the position of reviewing code, which is not their domain of expertise. Keeping the roles distinct — engineers own *how* it's built, scholars own *what is religiously accurate to present* — keeps both functions doing what they're actually qualified for.

### 6.4 Disputes and Board Changes

If scholarly positions genuinely differ on a question relevant to a project, the default resolution is to **present multiple documented positions with clear attribution**, letting the user or downstream implementer choose (e.g., a prayer-time API that supports multiple calculation methods as named, cited options) rather than MuslimOSS picking one as "correct." This mirrors how the software should behave technically (Section 6.2) and how the organization behaves at the human level — we are not in the business of adjudicating fiqh disagreements, only of building software flexible enough to respect them.

---

## 7. Repository Lifecycle

| Stage | Criteria to enter | What it means |
|---|---|---|
| **Proposed** | An RFC or issue describing the project, its scope, and why it belongs under MuslimOSS | Not yet a repository. Open for community feedback per Section 4.2. |
| **Incubating** | Approved by Org Maintainers/Steering Committee | Repository exists, marked clearly in its README as Incubating. Looser API stability guarantees — breaking changes don't require a full RFC. Purpose: let a project find its shape before committing to stability guarantees. |
| **Active** | Has at least one Repository Maintainer, a tagged release, tests, and documentation meeting the org's Engineering Standards | Full governance and stability guarantees apply — breaking changes require RFC + SemVer major bump. |
| **Graduated** | Sustained multi-maintainer activity, meaningful adoption (downstream dependents, production users), demonstrated stability over time | Highest trust tier — eligible for the org's "flagship project" listing in the org README. |
| **Archived** | No active maintainer for an extended period after the Section 5.3 process fails to find a replacement, or the project is superseded | Marked read-only with a clear README notice pointing to any successor project. Code remains available — we do not delete history. |

**Why an explicit Incubating stage exists:** requiring full API-stability guarantees from a project's very first commit either discourages experimentation or forces premature stability commitments that get walked back later (both bad outcomes). Marking early projects as Incubating sets honest expectations for anyone depending on them, the same way Kubernetes' SIG (Special Interest Group) projects have alpha/beta/stable maturity levels for exactly this reason.

---

## 8. Conflict Resolution

1. **Technical disagreements** follow Section 4 (lazy consensus → RFC → vote).
2. **Interpersonal or conduct disputes** follow the enforcement process defined in `CODE_OF_CONDUCT.md`, handled by the Founder/Steering Committee (and, once it exists, a dedicated Conduct Committee — see Section 9).
3. **Disputes about whether something is a religious-accuracy question at all** (i.e., disagreement over whether Section 6 even applies) are escalated to the Founder/Steering Committee, who consult the Scholar Advisory Board to make that determination. When genuinely uncertain, the default is to treat it as a religious-accuracy question — the cost of unnecessary caution here is much lower than the cost of an engineering team accidentally making a religious determination it had no standing to make.

---

## 9. Current Governance Phase

MuslimOSS is, at the time of this document's publication, in its **Founder-Led phase**: a single founder (Mehrab Hossain) holds Steering Committee authority, and the organization does not yet have multiple Org Maintainers or an established Scholar Advisory Board. This is stated plainly rather than implied away, because a governance document that describes committees and processes that don't actually exist yet is worse than no governance document — it misleads contributors about who really holds authority.

**Transition to a Steering Committee** is triggered when **any two** of the following conditions are met:

- 5 or more Active-stage repositories with independent Repository Maintainers
- 3 or more individuals holding Org Maintainer status for at least 6 months
- Sustained monthly active contributor count (per GitHub Insights, org-wide) exceeding 25 unique contributors over a rolling 3-month period

When triggered, the Founder proposes an initial Steering Committee composition via RFC (Section 4.2), drawn from the most tenured Org Maintainers, for community comment before ratification. This section itself may be amended by RFC as the organization's real trajectory becomes clearer — it is a plan, not a prophecy.

---

## 10. Amending This Document

Changes to GOVERNANCE.md require an RFC (Section 4.2) with a minimum 14-day comment period — longer than the standard 7 days, because governance changes affect every repository and every contributor's understanding of how authority works. During the Founder-Led phase, the Founder makes the final call after the comment period; once a Steering Committee exists, amendments follow the standard voting process in Section 4.3.

---

*Related documents: [`CODE_OF_CONDUCT.md`](./CODE_OF_CONDUCT.md) · [`CONTRIBUTING.md`](./CONTRIBUTING.md) · [`SECURITY.md`](./SECURITY.md) · [`BRAND_IDENTITY.md`](./BRAND_IDENTITY.md)*