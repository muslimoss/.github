# Contributing to MuslimOSS

**Status:** Foundational document — v1.0
**Applies to:** All repositories under the `muslimoss` GitHub organization. Individual repositories may add repo-specific setup instructions (build steps, local dev environment) in their own `CONTRIBUTING.md` or `README.md`, but the process, standards, and expectations below apply org-wide unless a repository explicitly states otherwise.

Thank you for considering contributing. This document exists so that contributing to any MuslimOSS repository — whether it's your first PR or your fiftieth — works the same way, without you having to guess.

Before anything else: read `CODE_OF_CONDUCT.md`. Participation in MuslimOSS means agreeing to it, and it applies to every interaction described below.

---

## 1. Ways to Contribute

Code is one of several ways to contribute, not the only one — a documentation-first project needs all of these to function well.

| Contribution type | Where it happens |
|---|---|
| Code (features, bug fixes, refactors) | Pull requests against the relevant repository |
| Documentation | Same as code — docs live alongside code and follow the same PR process |
| Translation and localization | Repository-specific — see that repo's `README.md` for its localization setup once one exists |
| Bug reports and reproductions | GitHub Issues on the relevant repository |
| Design (UI, iconography, illustration) | Follow `BRAND_IDENTITY.md` for visual direction; open a PR or Discussion for review |
| Datasets (Hadith collections, translations, etc.) | Highest scrutiny — see Section 7, these go through Scholar Advisory Board review before merge |
| Answering questions, triaging issues | GitHub Discussions and Issues — this is genuinely valued maintainer-track work, not a lesser form of contribution |

## 2. Before You Open a Pull Request

1. **Check for an existing issue or discussion** covering what you want to do. For anything beyond a small fix, open an issue first and get a maintainer's input before writing code — this avoids the frustrating outcome of a large PR built on an approach a maintainer already knows won't be accepted.
2. **For a new feature or breaking change**, check whether it needs an RFC under `GOVERNANCE.md` Section 4.2 (breaking API/data-format changes, new top-level project categories, license changes). If you're not sure, ask — opening a smaller-scoped issue to ask "does this need an RFC" is always welcome and never seen as a bother.
3. **Fork the repository** and create a branch from the repository's default branch. Branch naming is repository-specific (check that repo's `CONTRIBUTING.md` if it has additional conventions), but `type/short-description` (e.g., `fix/adhan-timezone-offset`) is the org-wide default absent other instruction.

## 3. Commit Convention: Conventional Commits

All commits to MuslimOSS repositories follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<optional scope>): <description>

[optional body]

[optional footer(s)]
```

| Type | Use for |
|---|---|
| `feat` | A new feature |
| `fix` | A bug fix |
| `docs` | Documentation-only changes |
| `test` | Adding or correcting tests |
| `refactor` | Code change that neither fixes a bug nor adds a feature |
| `chore` | Tooling, dependency bumps, build config |
| `perf` | Performance improvement |

**Example:** `fix(adhan-core): correct Isha calculation for high-latitude locations`

**Why this is required, not optional:** Conventional Commits give us three things a free-form commit history doesn't: automated changelog generation (no maintainer manually writing release notes for 100+ repos), a machine-readable signal for whether a change is `feat`/`fix` (patch) or contains `BREAKING CHANGE` (major), which directly drives Semantic Versioning (Section 6), and a searchable history where `git log --grep="^fix"` actually works. At small scale this looks like unnecessary process; at 100+ repositories it's the difference between a maintainer spending an afternoon writing a release note by hand and a release note generating itself correctly.

## 4. Developer Certificate of Origin (DCO)

Every commit must include a `Signed-off-by` trailer, added automatically with `git commit -s`:

```
Signed-off-by: Your Name <your.email@example.com>
```

This certifies that you wrote the contribution or otherwise have the right to submit it under the repository's license (the full text of the [Developer Certificate of Origin](https://developercertificate.org/) is linked from every repository's `CONTRIBUTING.md` reference and enforced by an automated DCO check in CI).

**Why DCO instead of a Contributor License Agreement (CLA):** A CLA requires every contributor — including someone fixing a typo — to sign a separate legal agreement, often through a third-party service, before their PR can be merged. That friction meaningfully discourages small, casual contributions, and is disproportionate for a project aiming for a large, global, often first-time-contributor base. DCO achieves the same practical goal (clear provenance and licensing certainty for every line of code) with a single `-s` flag on a commit, no separate signature process, and no third-party legal service dependency. This is the same reasoning the Linux kernel and most CNCF projects apply.

## 5. Code Review

MuslimOSS follows **lazy consensus** for routine changes (`GOVERNANCE.md` Section 4.1): a maintainer reviews and merges when satisfied, without requiring a formal vote. What to expect as a contributor:

- A first response (not necessarily a full review) within roughly a week for most repositories. Response times vary by repository maturity — an Incubating-stage project may have only one part-time maintainer.
- Review feedback focuses on correctness, tests, and adherence to the standards in this document — not on rewriting your PR to match a reviewer's personal style preference where the existing style guide is already satisfied.
- If a PR sits with unaddressed review feedback for **30 days** with no response from the contributor, it may be closed as stale. It can always be reopened when you're ready to continue.

## 6. Versioning and Releases

- **Semantic Versioning ([SemVer](https://semver.org))** — `MAJOR.MINOR.PATCH`. A `BREAKING CHANGE` footer in a Conventional Commit triggers a major version bump; `feat` triggers minor; `fix` triggers patch.
- **Why this matters beyond convention:** anyone building production software on top of a MuslimOSS library — a mosque's prayer-time display, a Zakat calculator embedded in a donation platform — needs to know that pinning to `^2.1.0` won't silently break their app. SemVer is the contract that makes that possible, and it's only trustworthy if commit types are applied correctly (Section 3), which is why the two are enforced together, not independently.
- **API versioning:** any project exposing a public API (REST, GraphQL, or a library's public interface) must version it explicitly (e.g., `/v1/`, `/v2/` for REST APIs) rather than making breaking changes to an unversioned endpoint. Deprecated versions are supported for a minimum deprecation window, stated in that project's own documentation, before removal.

## 7. Religious-Accuracy Contributions

If your contribution touches anything covered by `GOVERNANCE.md` Section 6.2 — prayer time calculation methods, Zakat rules, Hijri date determination, Qur'an text or translation, Hadith authentication grading, Tafsir attribution — say so explicitly in your PR description. These changes are routed to Scholar Advisory Board review before merge, regardless of how technically correct the code is, because correctness of implementation and correctness of religious content are reviewed separately (`GOVERNANCE.md` Section 6.3). This adds review time; it's the one category of contribution where MuslimOSS deliberately prioritizes getting it right over getting it merged quickly.

## 8. Testing, CI, and Security Tooling

Every repository at Active stage or above (`GOVERNANCE.md` Section 7) is expected to run, at minimum:

| Tool/Practice | Why it's required |
|---|---|
| **GitHub Actions CI** on every PR (build, lint, test) | Nothing merges on the strength of "it works on my machine" — this is the baseline that makes lazy consensus (Section 5) safe to use at all, since a maintainer merging quickly is trusting automated checks to catch what a fast human review might miss. |
| **CodeQL** (or an equivalent static analysis tool for non-CodeQL-supported languages) | Catches a class of security vulnerabilities (injection, unsafe deserialization, etc.) before they reach a release, at zero ongoing cost once configured — this is a direct expression of Amanah: treating users' security as a responsibility means catching what we can before code ships, not only after a report comes in. |
| **Dependabot** (or equivalent) for dependency updates | A 100+ repository organization cannot rely on maintainers manually tracking CVEs across every dependency in every repo — automated update PRs are the only approach that scales. |
| **A meaningful test suite**, not a specific coverage percentage mandate | We deliberately don't mandate a single number like "90% coverage" org-wide — a Qur'an-text-serving API and a small CLI tool have very different risk profiles, and a blanket percentage target tends to produce tests written to hit the number rather than tests that actually catch regressions. Each repository's `CONTRIBUTING.md` may set its own target once it has one; until then, "does this PR include tests for the behavior it changes" is the standard applied in review. |

## 9. Documentation Requirements

A PR that adds or changes public behavior (a new function, endpoint, config option, CLI flag) is expected to update the relevant documentation in the same PR — not as a follow-up. This is "documentation-first" applied practically: documentation is treated as part of the change, not an afterthought bolted on once someone complains it's missing, because a feature without documentation is, in practice, a feature most users will never discover or trust enough to use in production.

## 10. Security Issues

**Do not open a public issue for a security vulnerability.** Follow the disclosure process in `SECURITY.md`. This is called out here as well because it's the single most common mistake new contributors make — reporting a real vulnerability the same way they'd report a typo.

## 11. Becoming a Maintainer

There's no separate application process — see `GOVERNANCE.md` Section 5.1. In short: contribute consistently to a specific repository, and an existing maintainer (or Org Maintainer, for a repo without one yet) will nominate you publicly when your track record supports it. If you're interested in maintaining a repository you've been contributing to and haven't heard anything, it's entirely appropriate to ask directly in that repository's Discussions.

## 12. License

By contributing, you agree that your contribution is licensed under the repository's stated license (MIT by default across MuslimOSS — see `BRAND_IDENTITY.md` Section 3.1 and each repository's `LICENSE` file for any exceptions), certified via the DCO sign-off described in Section 4.

---

*Related documents: [`GOVERNANCE.md`](./GOVERNANCE.md) · [`CODE_OF_CONDUCT.md`](./CODE_OF_CONDUCT.md) · [`SECURITY.md`](./SECURITY.md) · [`BRAND_IDENTITY.md`](./BRAND_IDENTITY.md)*