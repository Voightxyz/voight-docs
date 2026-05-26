---
title: "GDPR Compliance Documentation"
subtitle: "How Voight aligns with Regulation (EU) 2016/679"
author: "Voight"
date: "May 2026"
subject: "Data Protection & Privacy"
keywords: [GDPR, Privacy, Data Protection, Voight, Observability]
titlepage: true
titlepage-color: "FFFFFF"
titlepage-text-color: "0A0A0F"
titlepage-rule-color: "0A0A0F"
titlepage-rule-height: 2
toc: true
toc-own-page: true
toc-depth: 2
colorlinks: true
linkcolor: black
urlcolor: blue
toccolor: black
book: false
classoption: [oneside]
mainfont: "Helvetica Neue"
sansfont: "Helvetica Neue"
monofont: "Menlo"
fontsize: 11pt
geometry: [a4paper, margin=2.5cm]
header-left: "Voight — GDPR Compliance"
header-right: "v1.0 · May 2026"
footer-left: "Voight Inc. — Confidential"
footer-right: "Page \\thepage\\ of \\pageref{LastPage}"
footer-center: ""
listings-no-page-break: true
disable-header-and-footer: false
caption-justification: centering
---

\newpage

# Document Control

| Field | Value |
| :--- | :--- |
| Document Title | GDPR Compliance Documentation |
| Version | 1.0 |
| Status | Published |
| Issue Date | May 26, 2026 |
| Owner | Voight — Privacy Office |
| Approver | Founding Team |
| Classification | Public |
| Next Review | November 26, 2026 |
| Distribution | Customers, prospects, supervisory authorities, the public |

This document describes how Voight ("Voight", "we", "us", "our") aligns its observability platform with **Regulation (EU) 2016/679** — the General Data Protection Regulation ("GDPR") — and the implementing national legislation of Member States.

It is intended for procurement teams, security reviewers, data protection officers, supervisory authorities, and individual data subjects who wish to understand how Voight collects, processes, stores, secures, and deletes personal data.

\newpage

# 1. Executive Summary

Voight is an AI observability platform that captures telemetry from agents and large language model (LLM) applications and presents it to the developers and operators who built those agents. Voight is provided as a hosted SaaS at `voight.xyz` and as an open-source SDK distributed via npm and PyPI.

This document confirms the following:

- **Voight is subject to the GDPR.** Although Voight is incorporated in the United States, its founding team operates from Spain and the platform is offered to data subjects in the European Union. The GDPR applies pursuant to Article 3(2).

- **Voight has a main establishment in the European Union.** Decisions regarding personal data processing are taken and implemented from Spain. The competent supervisory authority is the **Agencia Española de Protección de Datos (AEPD)**.

- **Voight acts as both Data Controller and Data Processor**, depending on the data category:
    - **Controller** — for account data of Voight customers (name, email, identifier, billing).
    - **Processor** — for the application-level telemetry that customers send through the SDK on behalf of their own end users.

- **Voight relies on a single lawful basis** for the processing it controls: **performance of a contract** (Article 6(1)(b)). No cookie consent banner, no marketing opt-in, no profile building.

- **Voight uses three carefully selected sub-processors**: Vercel, Railway, and Privy. All three have published Data Processing Agreements and certified security postures. No data is shared with advertisers, brokers, or analytics vendors.

- **International transfers** of personal data are governed by the **European Commission's 2021 Standard Contractual Clauses**, supported by technical safeguards (encryption in transit and at rest, least-privilege access, region-bounded backups) and a documented Transfer Impact Assessment (Annex C).

- **Data subject rights** under Articles 12–22 are honoured within the statutory thirty-day window. Self-service controls exist for agent and event deletion; account-level deletion is handled by a documented procedure at `team@voight.xyz`.

- **No special categories of data** (Article 9) and **no automated decision-making producing legal effects** (Article 22) are part of the Voight service.

The remainder of this document expands on each of these statements, with references to the relevant articles of the Regulation.

\newpage

# 2. Identity of the Controller

## 2.1 Legal Identity

| Field | Value |
| :--- | :--- |
| Trading name | Voight |
| Legal form | Corporation |
| Country of incorporation | United States of America |
| Main establishment for GDPR | Spain |
| Place of effective management | Spain (founders) and the United Kingdom (founders) |
| Service URLs | `voight.xyz`, `api.voight.xyz`, `docs.voight.xyz` |
| Software identifiers | `@voightxyz/sdk` (npm), `bitfrost` (PyPI), `Voightxyz/*` (GitHub) |

For the purposes of Regulation (EU) 2016/679, Voight maintains a **main establishment in Spain**, where the founding team carries out the activities that constitute the effective and real exercise of its data-controlling activities under Article 4(16) GDPR. The European Data Protection Board has confirmed in its *Guidelines 3/2018 on the territorial scope of the GDPR* that such an arrangement constitutes establishment, even without a registered branch.

Because Voight is established within the Union, it is **not required** to designate a representative under Article 27 GDPR.

## 2.2 Lead Supervisory Authority

| Field | Value |
| :--- | :--- |
| Authority | Agencia Española de Protección de Datos (AEPD) |
| Address | C/ Jorge Juan, 6, 28001, Madrid, Spain |
| Website | [www.aepd.es](https://www.aepd.es) |
| Complaints portal | [sedeagpd.gob.es](https://sedeagpd.gob.es) |

Data subjects in any Member State may also lodge a complaint with their local supervisory authority pursuant to Article 77 GDPR.

## 2.3 Privacy Contact

| Channel | Value |
| :--- | :--- |
| Privacy email | `team@voight.xyz` |
| Postal | available on request from the email above |
| Response window | 30 days (Article 12(3)) — extendable by 60 days for complex requests |

Voight has determined that it is **not required** to designate a Data Protection Officer under Article 37 GDPR. Voight does not engage in large-scale processing of special category data (Article 9), large-scale systematic monitoring of public areas, or any other activity that triggers the mandatory DPO threshold. Privacy responsibilities are exercised by the founding team and tracked in a dedicated privacy register.

\newpage

# 3. Scope of Processing

## 3.1 The Voight Platform — In One Diagram

```
     ┌──────────────────────────────┐
     │  Customer application (the   │
     │  data controller of the      │
     │  end-user data it generates) │
     └──────────────┬───────────────┘
                    │ Voight SDK (npm or PyPI)
                    │ — privacy filters run locally before any
                    │   payload leaves the customer process
                    ▼
     ┌──────────────────────────────┐
     │   api.voight.xyz (ingest)    │
     │   Railway (US-West region)   │
     │   TLS 1.3, vk_ API key       │
     └──────────────┬───────────────┘
                    │ Postgres (Prisma ORM)
                    ▼
     ┌──────────────────────────────┐
     │   Encrypted storage at rest  │
     │   Backups in same region     │
     └──────────────┬───────────────┘
                    │
                    ▼
     ┌──────────────────────────────┐
     │   voight.xyz (dashboard)     │
     │   Vercel — auth via Privy    │
     │   Customer sees own data     │
     └──────────────────────────────┘
```

The Voight platform consists of:

1. An **SDK** (`@voightxyz/sdk` on npm; `bitfrost` on PyPI) that customers install in their own applications. The SDK captures telemetry — model name, token counts, latency, tool calls — and runs three local privacy filters before any payload leaves the customer process (see §8).

2. An **ingest API** at `api.voight.xyz` that authenticates the call with a Voight key (`vk_…`) and writes events into a Postgres database hosted on Railway.

3. A **dashboard** at `voight.xyz` that allows the customer (and only the customer) to view their own events. Authentication is brokered by **Privy**, an identity provider that returns a signed session token bound to the user's Privy DID.

## 3.2 Voight as Controller — Account Data

For the account data of its direct customers, Voight is the **controller**. The personal data we process in this capacity is the minimum necessary to deliver the service the customer has contracted for.

| Category | Examples | Source | Retention |
| :--- | :--- | :--- | :--- |
| Identifiers | Privy DID, optional email, optional wallet, optional handle | Provided at sign-in via Privy | For the life of the account |
| Plan & billing | Plan tier, trial dates, Stripe customer ID (when billing is enabled) | Provided by the user; Stripe | For the life of the account |
| Technical telemetry | API keys (hashed), request timestamps, IP addresses in transient logs | Generated by use of the platform | 90 days for logs |
| Support correspondence | Messages sent to `team@voight.xyz` | Provided by the user | 2 years from last contact |

## 3.3 Voight as Processor — Customer Telemetry

For the telemetry that flows through the SDK, the customer is the **controller** and Voight acts as **processor**. We process this data only on documented instructions from the customer, set out in the Voight Data Processing Agreement (DPA), which the customer accepts when they create a Voight account.

The categories of personal data that *can* appear in customer telemetry are entirely under the customer's control. Voight provides three privacy levels (Minimal, Standard, Full — see §8) that the customer selects per agent. The SDK runs the chosen filter **locally** before any payload leaves the customer process, so the data that reaches Voight is already minimised.

Typical telemetry fields, after Standard scrubbing, include:

- Model identifier (e.g., `claude-haiku-4-5`)
- Token counts (input, output, cached)
- Duration in milliseconds
- Tool names invoked (without arguments by default)
- Cost in USD
- A redacted reasoning trace where applicable

Voight does **not** instruct customers to send special category data and Voight's terms of service prohibit it.

\newpage

# 4. Lawful Basis

Voight relies on a **single lawful basis** for the processing it controls: **Article 6(1)(b) GDPR — performance of a contract**.

When a user creates a Voight account and accepts the Terms of Service, a contract is formed between that user and Voight. The processing described in §3.2 is necessary to perform that contract: we cannot deliver a hosted observability dashboard, retain the user's events for the agreed retention window, or honour their access and erasure requests without processing the data listed above.

We have deliberately chosen **not** to rely on:

- **Consent** (Article 6(1)(a)) — to avoid consent fatigue and because no part of the service is "optional add-on processing" that would justify a separate consent.
- **Legitimate interest** (Article 6(1)(f)) — to avoid the documentation burden of a Legitimate Interest Assessment and the resulting uncertainty for data subjects.

This narrow basis means that Voight does **not** profile its users, does **not** target advertising, and does **not** sell or share data with third parties for those purposes. The lawful basis is the same for free, trial, and paid tiers.

For customer telemetry processed under §3.3, the lawful basis is determined by the customer in their role as controller of the end-user data they generate. Voight, as processor, relies on the lawful basis that the customer has documented in its own privacy notice.

\newpage

# 5. Purposes of Processing

Voight processes personal data for the following purposes, each linked to the lawful basis above.

| # | Purpose | Categories of data | Retention |
| :-: | :--- | :--- | :--- |
| 1 | Account creation and authentication | Privy DID, email, wallet | Life of account |
| 2 | Service delivery (ingestion, storage, dashboard) | Event payloads, API keys (hashed) | Tier-based retention §7 |
| 3 | Billing (when active) | Stripe IDs, plan, billing email | Life of account + 7 years (legal) |
| 4 | Customer support | Email correspondence | 2 years from last contact |
| 5 | Security and abuse prevention | Request logs, IP, rate-limit counters | 90 days |
| 6 | Compliance with legal obligations | The minimum necessary to respond to a binding request | As required by law |

Voight does **not** process personal data for marketing communications, behavioural advertising, profile enrichment, or sale to third parties.

\newpage

# 6. Data Subject Rights

Voight honours the following rights under Articles 12–22 of the GDPR. Requests can be made by emailing `team@voight.xyz` from the address associated with the account, or by using the in-app controls where indicated. We respond within 30 days (Article 12(3)).

| # | Right | How to exercise it with Voight |
| :-: | :--- | :--- |
| 1 | **Information** (Arts. 13–14) | This document plus the public Privacy Notice at `voight.xyz` |
| 2 | **Access** (Art. 15) | Login to the dashboard exposes all stored events; a full export of account-level data is available on request |
| 3 | **Rectification** (Art. 16) | Editable in the dashboard settings; corrections to immutable fields are made on request |
| 4 | **Erasure** / "right to be forgotten" (Art. 17) | **Agent-level**: delete an agent in the dashboard to cascade-delete its events. **Account-level**: email `team@voight.xyz`. Account-level deletion is performed within 30 days and includes backups within an additional 30 days |
| 5 | **Restriction** (Art. 18) | Available on request; the account is suspended without deletion while the request is processed |
| 6 | **Portability** (Art. 20) | Account data and events are exported in JSON via the `/api/me/export` endpoint |
| 7 | **Objection** (Art. 21) | Not applicable to contract-based processing, but objection to specific processing (e.g., support emails) is honoured on request |
| 8 | **Automated decision-making** (Art. 22) | **Not applicable.** Voight does not subject data subjects to decisions producing legal or similarly significant effects based solely on automated processing |
| 9 | **Withdrawal of consent** (Art. 7(3)) | Not applicable, as Voight does not rely on consent |
| 10 | **Lodging a complaint** (Art. 77) | With the AEPD or any local supervisory authority |

A self-service "Delete my account" control in the dashboard is on the roadmap for the v1.0 product release. Until that ships, the email-based procedure described above is the documented mechanism and is fully compliant with Article 12(2): the controller must facilitate the exercise of data subject rights, not necessarily expose every right as a one-click control.

\newpage

# 7. Data Retention

Voight follows the principle of storage limitation (Article 5(1)(e)). Personal data is retained only for as long as necessary for the purposes for which it was collected.

## 7.1 Telemetry Event Retention

| Plan | Event retention |
| :--- | :--- |
| Free | 7 days |
| Pro | 90 days |
| Enterprise | 1 year (custom terms available) |

After the retention window expires, events are hard-deleted from the primary database and removed from backups within the next backup rotation cycle (≤ 30 days).

## 7.2 Account Data Retention

| Data | Retention |
| :--- | :--- |
| Account profile (DID, email) | Life of account |
| Billing records | Life of account + 7 years (Spanish tax law, Article 30 Código de Comercio) |
| Support correspondence | 2 years from last contact, then deleted |
| Server logs (request, IP, rate-limit) | 90 days, then deleted by log rotation |
| Backups | 30 days rolling, then overwritten |

## 7.3 Erasure Mechanics

When a deletion request is honoured:

1. The primary database row is hard-deleted (not soft-deleted).
2. Cascade rules in the Postgres schema delete dependent rows (agents, events, sessions, API keys).
3. Backups are not edited in place — they age out of the 30-day rolling window and are then overwritten.
4. Voight retains a tombstone record of the deletion itself (timestamp, request identifier, no personal data) for audit purposes.

\newpage

# 8. Security Measures (Article 32)

Voight implements technical and organisational measures appropriate to the risk, in line with Article 32 GDPR.

## 8.1 Privacy by Design — Three-Level Local Filter

The Voight SDK ships with three privacy levels. The chosen level is enforced **locally**, inside the customer's own process, before any payload reaches Voight infrastructure.

| Level | Behaviour |
| :--- | :--- |
| **Minimal** | Free-text content fields are dropped entirely. Only structural metadata (tool names, token counts, durations, identifiers) is sent. |
| **Standard** (default) | Free-text fields are kept but passed through `scrubPii()` first. Thirteen regular expressions plus a Luhn-validated credit-card check identify common secrets and personal identifiers and replace them with tagged tokens (`[REDACTED-API-KEY]`, `[REDACTED-EMAIL]`, …). The list is published at `docs.voight.xyz/privacy/pii-patterns`. |
| **Full** | The customer has assumed responsibility for upstream scrubbing. No SDK-side filtering. Reserved for environments where the customer's own pipeline has already removed personal data. |

This local-first design satisfies Article 25 (data protection by design and by default) and reduces the personal data Voight ever sees in the first place.

## 8.2 Encryption in Transit

All endpoints exposed by Voight require **TLS 1.3**. TLS 1.2 is permitted only for negotiation fallback with legacy clients; older protocols are rejected. Certificates are issued by Let's Encrypt via the hosting provider and rotated automatically.

Internal traffic between the API service and the database runs over Railway's private network. Postgres connections are protected by TLS and authenticated with a credential rotated on schedule.

## 8.3 Encryption at Rest

Postgres storage volumes on Railway are encrypted at rest using AES-256. Backups are encrypted with the same algorithm and stored in the same region as the primary database. Customer secrets (API keys, third-party tokens) are stored hashed; the plaintext value is shown to the customer once at creation and never again.

## 8.4 Authentication and Access Control

| Surface | Mechanism |
| :--- | :--- |
| End-user authentication | Privy DID — email magic link, wallet signature, or social provider. Voight does not store passwords. |
| Server-to-server (SDK → API) | Bearer Voight key (`vk_…`), 256 bits of entropy, hashed at rest, revocable per agent |
| Internal infrastructure | SSO with two-factor authentication for the founding team, signed audit log |
| Database direct access | Restricted to the founding team; access requires a short-lived credential and is logged |

The principle of least privilege is applied throughout. No third party — including Voight's sub-processors — has standing access to customer personal data outside of the strict scope of the service each one provides.

## 8.5 Logging and Monitoring

Voight maintains application and access logs sufficient to reconstruct security-relevant events. Logs are retained for 90 days and reviewed routinely. Personal data is excluded from logs wherever practical; where structured identifiers must appear (e.g., user ID for an authenticated request), the value is the opaque Privy DID, not a name or email.

## 8.6 Vulnerability Management

Voight's dependencies are monitored continuously through GitHub's Dependabot. Critical vulnerabilities are remediated within 7 days; high within 30; medium within 90. The SDK is published with provenance attestations (npm `--provenance`) so customers can verify the integrity of the artifact they install.

## 8.7 Personnel

All people with access to Voight production systems are bound by confidentiality obligations and receive privacy and security guidance at onboarding. The founding team operates under the discipline summarised in this document.

\newpage

# 9. Sub-processors (Article 28)

Voight engages a small number of sub-processors to deliver the service. Each one has been selected for its compliance posture, has signed a written contract that imposes Article 28 obligations (or has published one that we incorporate by reference), and is subject to the technical and organisational measures described in §8.

| # | Sub-processor | Service provided | Location | Compliance posture | DPA |
| :-: | :--- | :--- | :--- | :--- | :--- |
| 1 | **Vercel, Inc.** | Hosting of the dashboard and marketing site (`voight.xyz`) | Global edge, primary region United States | SOC 2 Type II, GDPR-aligned DPA | [vercel.com/legal/dpa](https://vercel.com/legal/dpa) |
| 2 | **Railway Corp.** | Hosting of the API and Postgres database, including backups | United States (US-West) | SOC 2 Type II, GDPR-aligned DPA | [railway.com/legal/dpa](https://railway.com/legal/dpa) |
| 3 | **Privy.io** | End-user authentication and identity management | United States | SOC 2 Type II, GDPR-aligned DPA | [privy.io/legal/dpa](https://privy.io/legal/dpa) |

When Voight intends to engage a new sub-processor or replace an existing one, the new entry is added to this list and customers are notified at least 30 days in advance through the changelog at `docs.voight.xyz/changelog`. Customers retain the right to object to a new sub-processor under the terms of the Voight DPA.

## 9.1 Sub-processors Planned (Not Yet Engaged)

The following are part of the published roadmap and are not currently in the processing chain. They are listed here for transparency; data is not shared with them today.

| Sub-processor | Service | When |
| :--- | :--- | :--- |
| **Stripe, Inc.** | Subscription billing | When paid tiers are activated |
| **Helius / Solana RPC providers** | Optional on-chain event anchoring | When the on-chain registry ships |

This document will be re-issued with a new version number when any of these become active.

\newpage

# 10. International Data Transfers (Articles 44–49)

## 10.1 Where Personal Data Goes

Personal data processed by Voight is stored in **Railway's US-West region (California, United States)**. Voight is a US-incorporated entity whose founders operate from Spain and the United Kingdom; in the ordinary course of business, personal data may therefore be accessed from those locations.

The United States is, in the assessment of the European Court of Justice (Case C-311/18 — *Schrems II*), a third country whose laws do not by themselves offer a level of protection essentially equivalent to that of the Union. Transfers to the United States therefore require an additional transfer tool under Chapter V of the GDPR.

## 10.2 Transfer Mechanism — 2021 Standard Contractual Clauses

Voight relies on the **Standard Contractual Clauses adopted by the European Commission on 4 June 2021 (Commission Implementing Decision (EU) 2021/914)** as the transfer tool for all personal data transferred from the European Economic Area to the United States.

The applicable modules are:

- **Module 2 (Controller to Processor)** — when Voight acts as processor of customer telemetry on behalf of an EU-established controller (the customer).
- **Module 4 (Processor to Controller)** — when telemetry is returned to a customer outside the Union.

Customers receive a copy of the executed SCCs as part of the Voight Data Processing Agreement at account creation. A copy of the DPA is available for review on request from `team@voight.xyz`.

## 10.3 Supplementary Measures

In line with the EDPB *Recommendations 01/2020 on supplementary measures*, Voight has implemented the following measures, which together render the SCCs effective in practice:

1. **Encryption in transit and at rest** — described in §8.2 and §8.3. Keys are managed by the infrastructure providers under their certified controls.
2. **Pseudonymisation by design** — the platform identifies end users by an opaque Privy DID, not by name. Telemetry payloads are scrubbed at source before transfer.
3. **Strict access control** — production data is accessible only to a narrow set of identified individuals operating under written confidentiality obligations.
4. **Transparency on government access requests** — Voight commits to challenging any third-country government access request that is overbroad, unlawful under the requesting country's own law, or inconsistent with the GDPR. We have received zero such requests to date.
5. **Region-bounded backups** — backups never leave the primary processing region.

A full Transfer Impact Assessment (TIA), prepared in accordance with EDPB *Recommendations 01/2020*, is provided as **Annex C** of this document.

## 10.4 Other Transfers

No personal data is transferred to a third country other than the United States. The only sub-processors engaged today (§9) are all US entities, and all are covered by the same SCC-based framework.

\newpage

# 11. Personal Data Breach Procedure (Articles 33–34)

Voight maintains a written incident-response procedure. In the event of a personal data breach:

| Step | Time-frame | Action |
| :--: | :--- | :--- |
| 1 | T+0 | The on-call founder declares the incident, opens an internal channel, and freezes the affected component if continued operation increases risk. |
| 2 | T+1 hour | Initial impact assessment: which data categories, how many data subjects, what is the level of risk to rights and freedoms. |
| 3 | T+24 hours | If reportable, the AEPD is notified through `sedeagpd.gob.es`. The notification follows the template in Article 33(3) and is updated as facts develop. |
| 4 | T+72 hours | Final notification to the AEPD, no later than 72 hours after Voight becomes aware of the breach (Article 33(1)). |
| 5 | T+72 hours / "without undue delay" | If the breach is likely to result in a high risk to data subjects, affected individuals are notified directly in clear and plain language (Article 34). |
| 6 | T+7 days | Internal post-incident review. Root cause, lessons learned, and corrective actions are recorded in a register and applied. |

Voight has not experienced a notifiable personal data breach as of the issue date of this document. The breach register is maintained as required by Article 33(5).

\newpage

# 12. Cookies and the ePrivacy Directive

The dashboard at `voight.xyz` sets the **minimum** cookies necessary to deliver the service:

| Cookie | Purpose | Type | Duration |
| :--- | :--- | :--- | :--- |
| `voight_handle` | Display the authenticated user's handle in the navigation bar | Strictly necessary | Session |
| Privy iframe cookies | Authentication session (set by `auth.privy.io`) | Strictly necessary | Per Privy's own policy |

Under Article 5(3) of Directive 2002/58/EC (the ePrivacy Directive) and the corresponding national transpositions (in Spain, *Ley 34/2002 de Servicios de la Sociedad de la Información*, Article 22(2)), strictly necessary cookies do not require prior consent. Voight therefore does not display a cookie banner.

Voight does **not** use analytics cookies, marketing cookies, advertising pixels, fingerprinting techniques, or session-replay tools. No third-party tracking is loaded on `voight.xyz` or `docs.voight.xyz`.

\newpage

# 13. Children's Data (Article 8)

The Voight service is offered for use by professionals — engineers, founders, operators, and the companies they represent. The Terms of Service require users to be at least **16 years old**, which is the age of digital consent set out in Article 8(1) GDPR (Member States may set a lower age down to 13; Spain has retained 14 in *LOPDGDD* Article 7, but Voight applies the higher 16 floor by default for all jurisdictions).

If Voight becomes aware that an account belongs to a person below this threshold, the account is suspended and the data deleted in line with §7.

\newpage

# 14. Records of Processing Activities (Article 30)

Voight maintains a written Record of Processing Activities ("RoPA") in line with Article 30(1) for processing carried out as controller, and Article 30(2) for processing carried out as processor.

A condensed view of the RoPA is reproduced below; the full register is held internally and made available to the AEPD or any other competent supervisory authority on request.

| # | Activity | Role | Categories of data | Categories of subjects | Recipients | Transfers | Retention | Security ref. |
| :-: | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Account sign-in | Controller | Privy DID, email, wallet | Voight customers | Privy | US (SCCs) | Life of account | §8 |
| 2 | Telemetry ingest | Processor | Telemetry payloads | Customer end users | Railway | US (SCCs) | 7d / 90d / 1y | §8 |
| 3 | Telemetry display | Processor | Telemetry payloads | Customer end users | Vercel | US (SCCs) | As stored | §8 |
| 4 | Support email | Controller | Email content | Customer correspondents | None | None | 2 years | §8 |
| 5 | Billing (planned) | Controller | Stripe IDs, billing email | Voight customers | Stripe | US (SCCs) | 7 years | §8 |

\newpage

# 15. Governance and Accountability

| Field | Value |
| :--- | :--- |
| Privacy contact | `team@voight.xyz` |
| Supervisory authority | AEPD (Spain) — `www.aepd.es` |
| Data Protection Officer | Not required under Article 37; founding team holds privacy responsibility |
| EU Representative | Not required under Article 27 (establishment in Spain) |
| Document review cycle | Every six months and following any material change to the platform, sub-processors, or applicable law |
| Document store | Versioned in the public docs repository under `voight-docs/trust/_pdf-sources/` |

Voight commits to keeping this document current. Material changes — new sub-processor, new region, new lawful basis, change of supervisory authority — are reflected in a new version within 30 days of taking effect, and customers are notified through the changelog.

\newpage

# Annex A — Sub-processor Register

This annex is the single source of truth for the sub-processors Voight engages today. It restates and expands on §9.

## A.1 Active Sub-processors

### A.1.1 Vercel, Inc.

| Field | Value |
| :--- | :--- |
| Service provided | Hosting of `voight.xyz`, `docs.voight.xyz`, and edge functions |
| Personal data processed | Authenticated session identifiers, IP addresses (transient), customer-uploaded content on the dashboard |
| Region of processing | Global edge with primary region in the United States |
| Compliance posture | SOC 2 Type II; ISO 27001; published GDPR DPA with 2021 SCCs |
| DPA | [vercel.com/legal/dpa](https://vercel.com/legal/dpa) |
| Sub-processor list | [vercel.com/legal/subprocessors](https://vercel.com/legal/subprocessors) |
| Onward transfer | Vercel may engage its own sub-processors (e.g., AWS for compute). Voight assumes responsibility for the full chain. |

### A.1.2 Railway Corp.

| Field | Value |
| :--- | :--- |
| Service provided | Hosting of the API (`api.voight.xyz`) and the Postgres database, including backups |
| Personal data processed | All telemetry payloads, account records, server logs |
| Region of processing | United States — US-West (California) |
| Compliance posture | SOC 2 Type II; published GDPR DPA with 2021 SCCs |
| DPA | [railway.com/legal/dpa](https://railway.com/legal/dpa) |
| Sub-processor list | Available via Railway support |
| Onward transfer | Railway uses GCP as its infrastructure backbone, covered by GCP's own GDPR commitments |

### A.1.3 Privy.io

| Field | Value |
| :--- | :--- |
| Service provided | Authentication (magic link email, social, wallet) and identity issuance (DID) |
| Personal data processed | Email address (where used), wallet address (where used), social provider identifier |
| Region of processing | United States |
| Compliance posture | SOC 2 Type II; published GDPR DPA with 2021 SCCs |
| DPA | [privy.io/legal/dpa](https://privy.io/legal/dpa) |
| Sub-processor list | Published on the Privy trust page |
| Onward transfer | Privy uses AWS US-East and its own communication providers, covered by Privy's DPA |

## A.2 Planned Sub-processors

Not active today; listed for transparency.

| Provider | Service | Expected go-live | Personal data |
| :--- | :--- | :--- | :--- |
| Stripe, Inc. | Subscription billing | When paid tiers are activated | Billing email, payment metadata (Stripe holds card data, not Voight) |
| Helius / Solana RPC | Optional on-chain event anchoring | When the on-chain registry ships | Public wallet address (where the customer opts in) |

\newpage

# Annex B — Categories of Personal Data — Catalogue

This annex provides a complete catalogue of personal data fields stored by Voight, grouped by the data store in which they live. It is intended to make Article 30 audits and access requests straightforward.

## B.1 In `voight` Postgres database

| Table | Field | Type | Origin | Why it exists |
| :--- | :--- | :--- | :--- | :--- |
| `User` | `id` | cuid | Voight | Primary key |
| `User` | `privyId` | Privy DID | Privy at first sign-in | Authentication |
| `User` | `email` | string (optional) | User or Privy | Identification and communication |
| `User` | `wallet` | string (optional) | User or Privy | Web3 identity (optional) |
| `User` | `handle` | string (optional) | User | Display name |
| `User` | `plan`, `planStartedAt`, `trialEndsAt` | enum, dates | Voight billing logic | Plan enforcement |
| `User` | `stripeCustomerId`, `stripeSubscriptionId` | string (when billing is active) | Stripe | Billing |
| `Agent` | … | various | User input | Agent metadata; no personal data of end users |
| `Event` | `payload` | JSON | Customer SDK | Telemetry (post-scrubbing) |
| `ApiKey` | `hash` | sha-256 | Voight | Authenticated ingest |

## B.2 In transient logs

| Source | Fields | Retention |
| :--- | :--- | :--- |
| API access logs | Timestamp, method, path, status, latency, IP, user ID (where authenticated) | 90 days |
| Application logs | Timestamp, level, structured event, no payload bodies | 90 days |
| Audit log | Timestamp, actor, action, target | 1 year |

## B.3 At sub-processors

See Annex A. Each sub-processor holds only the categories of data that are functionally required for the service it provides; nothing more.

\newpage

# Annex C — Transfer Impact Assessment (Summary)

This annex summarises the Transfer Impact Assessment Voight has conducted for the transfer of personal data from the European Economic Area to the United States, in line with the EDPB *Recommendations 01/2020*.

## C.1 Description of the Transfer

| Field | Value |
| :--- | :--- |
| Exporter | Voight, established in Spain (Article 4(16) GDPR) |
| Importer | Voight, incorporated in the United States; sub-processors Vercel, Railway, Privy |
| Categories of data | As catalogued in Annex B |
| Categories of subjects | Voight customers and (through telemetry) their end users |
| Purpose | Provision of the Voight observability service |
| Transfer tool | Module 2 / Module 4 of the 2021 SCCs |

## C.2 Assessment of the Legal Regime of the Third Country

The relevant US legal provisions are Section 702 of the Foreign Intelligence Surveillance Act (FISA 702) and Executive Order 12333. The European Court of Justice has found these provisions to fall short of the requirements of Article 47 of the Charter of Fundamental Rights.

However, Voight assesses that:

1. **Personal data processed by Voight is not of a kind ordinarily of interest to US national-security agencies.** The telemetry is operational metadata about LLM applications (model name, token counts, latency), not communications content, location data, or special category data.
2. **The volume of EU data subjects processed is modest** — Voight is in its first year of operation.
3. **Voight, as the importer, is not a US "electronic communication service provider" within the meaning of FISA 702(b)(4).** Voight's service is observability for the customer's own applications, not the carriage or storage of third-party communications.

## C.3 Supplementary Measures

The technical, contractual, and organisational measures listed in §10.3 mitigate the residual risk to a level Voight assesses as low.

## C.4 Conclusion

Voight concludes that the SCCs, together with the supplementary measures described, provide a level of protection essentially equivalent to that guaranteed within the European Union. The transfer is therefore lawful under Article 46 GDPR.

This assessment will be reviewed at the next document review cycle, or sooner if there is a material change to the US legal regime, to the nature of the data transferred, or to Voight's role.

\newpage

# Annex D — Document Version History

| Version | Date | Change | Author |
| :--- | :--- | :--- | :--- |
| 1.0 | 2026-05-26 | Initial publication. | Voight — Privacy Office |

\newpage

# Contact

For any question, request, or feedback related to this document or to the way Voight handles personal data:

**Voight — Privacy Office**

`team@voight.xyz`

[voight.xyz/trust](https://voight.xyz/trust) · [docs.voight.xyz/trust](https://docs.voight.xyz/trust)

---

*This document is published by Voight and made available under the same terms as the Voight documentation. The legally binding agreement between Voight and a customer is the Voight Terms of Service and the Voight Data Processing Agreement.*
