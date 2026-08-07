# MuslimOSS — Security Policy

**Status:** Foundational document — v1.0
**Applies to:** All repositories under the `muslimoss` GitHub organization. A repository may publish its own `SECURITY.md` with tighter, project-specific supported-version details, but the reporting process and disclosure policy below are the org-wide baseline.

> **Note on current infrastructure:** MuslimOSS does not yet have a public website. Every reporting path in this document is deliberately GitHub-native (private vulnerability reporting, an email address) rather than pointing to a website page, so this policy is fully functional today and doesn't need to be rewritten once a website exists — it will simply gain an additional, mirrored page at that point.

---

## 1. Our Commitment

Security is treated as a responsibility (Amanah), not a feature bolted on after release. This is a practical, load-bearing commitment, not a values statement for its own sake: it's the reason CodeQL and Dependabot are required baseline tooling for every Active-stage repository (`CONTRIBUTING.md` Section 8), and it's the reason this document exists before MuslimOSS has any large user base — the process should be in place before it's needed, not written hastily after an incident.

## 2. Supported Versions

MuslimOSS repositories are early-stage as of this document's publication (`GOVERNANCE.md` Section 9). Until a repository has a documented version-support policy of its own, the default is:

| Version | Supported |
|---|---|
| Latest tagged release | ✅ Yes |
| Latest major version's prior minor releases | ✅ Security fixes backported where feasible |
| Anything older than the latest major version | ❌ No — upgrade to the latest major version |
| Pre-release / `main` branch (unreleased) | ⚠️ Best-effort only, not a supported target for production use |

Once a repository has multiple actively-used major versions in production, its own `SECURITY.md` should state a concrete support window rather than relying on this default.

## 3. Reporting a Vulnerability

**Do not open a public GitHub issue for a security vulnerability.** Public issues are indexed and visible immediately, which gives potential attackers a head start before a fix exists — this is the single most important rule in this document, and it's why the reporting paths below are both private by design.

### 3.1 Preferred: GitHub Private Vulnerability Reporting

Every MuslimOSS repository should have GitHub's built-in private vulnerability reporting enabled (repository **Security** tab → **Report a vulnerability**). This is the preferred channel because it requires no separate infrastructure MuslimOSS has to build or maintain — GitHub already provides an encrypted, maintainer-only reporting form scoped to the specific repository, which is the right fit for a young organization that doesn't yet have (and shouldn't rush to build) a dedicated security team or a website with its own disclosure portal.

If a repository does not yet have this enabled, use the fallback below.

### 3.2 Fallback: Email

**`security@muslimoss.org`**

Use this if the affected repository doesn't have private vulnerability reporting enabled, if the issue spans multiple repositories, or if it concerns the organization itself (e.g., a compromised org-level credential, a malicious package published under the `muslimoss` npm/PyPI scope) rather than a single codebase.

**This inbox must be a real, monitored address before this document is published anywhere public.** A Google Group forwarding to the Founder (and later, Org Maintainers) is sufficient at this stage — it does not require a website or dedicated security infrastructure to be legitimate, only that someone is actually reading it.

### 3.3 What to Include

- Affected repository and version/commit
- Type of vulnerability (e.g., injection, authentication bypass, data exposure, dependency CVE)
- Steps to reproduce, or a proof-of-concept if you have one
- Potential impact as you understand it
- Whether you intend to publicly disclose independently, and on what timeline (see Section 5)

You don't need a fully weaponized exploit to report something — a credible, well-described concern is enough to open the process.

## 4. Response Process

| Stage | Timeline | What happens |
|---|---|---|
| **Acknowledgment** | Within 3 business days | Confirmation the report was received and is being triaged. |
| **Triage & severity assessment** | Within 7 business days of acknowledgment | Severity assessed using [CVSS](https://www.first.org/cvss/) as a reference scale; reporter is told the assessed severity and expected next steps. |
| **Fix development** | Timeline varies by severity — see below | A maintainer (or, for org-wide issues, an Org Maintainer) develops and tests a fix, coordinating privately with the reporter where useful. |
| **Release & disclosure** | See Section 5 | Patched version released; advisory published; reporter credited (if desired). |

**Target timelines by severity** (guideline, not a contractual SLA — MuslimOSS is a volunteer-driven project at this stage, and stating an unenforceable contractual SLA would be dishonest):

| Severity | Target time to patched release |
|---|---|
| Critical (remote code execution, full data exposure, auth bypass) | As fast as responsibly possible — typically days, not weeks |
| High | Within 2–3 weeks |
| Medium | Within the next scheduled minor release |
| Low | Next regular release cycle |

**Why guideline targets instead of a formal SLA:** A written SLA (e.g., "we guarantee a patch within 48 hours") that a volunteer-maintained project cannot reliably meet is worse than an honest guideline — it creates false confidence for anyone depending on it in production and sets the project up to visibly break its own stated commitment. As MuslimOSS matures and specific repositories gain dedicated, funded maintainers, those repositories can publish their own stricter SLAs in their project-specific `SECURITY.md`.

## 5. Coordinated Disclosure

MuslimOSS follows coordinated (responsible) disclosure:

- The reporter and maintainers agree on a disclosure timeline once a fix is available — by default, **90 days** from initial report, or sooner if a fix ships earlier, matching common industry practice (e.g., Google Project Zero's standard window) as a reasonable balance between giving users time to update and not leaving a known issue undisclosed indefinitely.
- Once a fix is released, a **GitHub Security Advisory** is published on the affected repository, including a description of the issue, affected versions, the fix, and credit to the reporter (unless the reporter requests anonymity).
- If a reporter needs to disclose sooner (e.g., an academic publication deadline) or MuslimOSS needs longer (e.g., a fix requires a breaking change needing broader migration support), both sides are expected to communicate and negotiate in good faith rather than defaulting to the 90-day window unilaterally.

## 6. Scope

**In scope:** All source code in repositories under the `muslimoss` GitHub organization, and packages published under the `@muslimoss` npm scope, `muslimoss` PyPI namespace, or equivalent for other registries.

**Out of scope (for now, pending existence):**
- A public website (does not yet exist — see the note at the top of this document)
- Any third-party fork, mirror, or unofficial redistribution of MuslimOSS code not hosted under the official `muslimoss` GitHub org
- Social engineering, physical security, or denial-of-service testing against any infrastructure — these are not useful reports for a project at this stage and are not in scope for coordinated disclosure handling

## 7. Safe Harbor

MuslimOSS supports good-faith security research. If you discover a vulnerability while acting in good faith — making a reasonable, good-faith effort to avoid privacy violations, data destruction, or service disruption, and reporting through the channels above rather than exploiting or publicly disclosing first — we will not pursue legal action against you for that research. This is a direct extension of treating security researchers as collaborators in the Amanah of protecting users, not adversaries.

## 8. Acknowledgments

Reporters who identify valid vulnerabilities are credited in the resulting GitHub Security Advisory, unless they request otherwise. MuslimOSS does not currently operate a paid bug bounty program — this may be revisited via RFC (`GOVERNANCE.md` Section 4.2) once the organization has the funding and infrastructure to sustain one responsibly, rather than announcing a bounty program it can't reliably fund.

---

*Related documents: [`GOVERNANCE.md`](./GOVERNANCE.md) · [`CODE_OF_CONDUCT.md`](./CODE_OF_CONDUCT.md) · [`CONTRIBUTING.md`](./CONTRIBUTING.md)*