---
title: "NIST AI Risk Management Framework"
subtitle: "Voight Alignment (AI RMF 1.0)"
author: "Voight"
date: "June 2026"
subject: "AI Risk Management"
keywords: [NIST, AI RMF, AI Risk Management, Voight, Observability, Trustworthy AI]
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
header-left: "Voight — NIST AI RMF"
header-right: "v1.0 · June 2026"
footer-left: "Voight Inc. — Confidential"
footer-right: "Page \\thepage\\ of \\pageref{LastPage}"
listings-no-page-break: true
caption-justification: centering
---

\newpage

# Document Control

| Field | Value |
| :--- | :--- |
| Document Title | NIST AI Risk Management Framework — Voight Alignment |
| Document Version | 1.0 |
| Framework Tracked | NIST AI RMF 1.0 (NIST AI 100-1) + Generative AI Profile (NIST-AI-600-1) |
| Status | Published |
| Issue Date | June 3, 2026 |
| Owner | Voight — Security Office |
| Approver | Founding Team |
| Classification | Public |
| Next Review | December 3, 2026 |

This document describes how Voight ("Voight", "we", "us", "our") relates to the NIST Artificial Intelligence Risk Management Framework (AI RMF 1.0, NIST AI 100-1, January 2023) and its companion Generative AI Profile (NIST-AI-600-1, July 2024). It is written for AI risk managers, security reviewers, and procurement teams evaluating Voight, and for Voight customers who use the platform as part of their own AI RMF implementation.

The AI RMF is a voluntary framework. This document records voluntary alignment; it is not a certification by, or endorsement from, NIST.

\newpage

# 1. Executive Summary

The NIST AI Risk Management Framework is the leading voluntary framework for managing the risks of artificial intelligence systems. It organises AI risk management into four functions — **Govern, Map, Measure, and Manage** — and defines a set of trustworthiness characteristics that an AI system should exhibit: valid and reliable, safe, secure and resilient, accountable and transparent, explainable and interpretable, privacy-enhanced, and fair with harmful bias managed.

Voight relates to this framework from two angles, and this document addresses both honestly.

**Part 1 — How Voight supports your AI RMF.** Voight is an observability platform purpose-built to capture, store, and present telemetry about AI systems in production. Within the four functions, Voight maps most naturally and most strongly to **Measure** — the function concerned with analysing and tracking AI risk over time using metrics. Voight also contributes operational evidence to **Map** (it tells you what your AI system actually does in production) and to **Manage** (it provides the alerts, traces, and records used to respond to incidents). Voight contributes least to **Govern**, which is an organisational discipline rather than a technical one; there, Voight supplies evidence, not the governance itself. Part 1 maps each function in turn.

**Part 2 — Voight's own AI governance.** Today, Voight does not operate an AI system within its own product; it is the platform that observes its customers' AI systems. Part 2 records that fact, the platform-security baseline that underpins it, and a forward commitment for the AI-powered features on Voight's roadmap.

Two honest framing points run through the document:

1. **Voight is a Measure-function tool first.** Its centre of gravity is measurement and tracking. It supports Map and Manage with operational evidence, and it informs — but does not constitute — Govern.

2. **Observability is evidence, not governance.** Voight produces the data and the audit trail that an AI RMF programme runs on. It does not set your risk tolerance, write your policies, or make your risk-treatment decisions. Those remain with your organisation.

A function-by-function coverage summary appears in §7, and a consolidated statement of what Voight does *not* do appears in §8.

\newpage

# 2. The NIST AI RMF in Brief

The AI RMF Core is organised into four functions, each broken into categories. The categories below are summarised from NIST AI 100-1.

**GOVERN** — cultivate a culture of AI risk management across the organisation.

- Govern 1: Policies, processes, and procedures for managing AI risk are in place.
- Govern 2: Accountability structures empower and train the right teams.
- Govern 3: Diversity, equity, inclusion, and accessibility inform risk decisions.
- Govern 4: Organisational culture emphasises critical thinking and a safety-first approach.
- Govern 5: Mechanisms for engaging external AI actors are established.
- Govern 6: Policies address third-party software, data, and supply-chain risk.

**MAP** — establish the context and identify the risks of a specific AI system.

- Map 1: Context — purpose, deployment setting, and goals — is established.
- Map 2: The AI system's tasks and methods are categorised.
- Map 3: Capabilities, usage targets, benefits, and costs are understood.
- Map 4: Risks and benefits are mapped across all components, including third-party.
- Map 5: Impacts to individuals, groups, organisations, and society are characterised.

**MEASURE** — analyse, assess, and track AI risks using quantitative and qualitative methods.

- Measure 1: Appropriate methods and metrics are identified and applied.
- Measure 2: AI systems are evaluated for trustworthy characteristics.
- Measure 3: Mechanisms track identified risks over time during deployment.
- Measure 4: The efficacy of measurement is gathered and assessed from stakeholders.

**MANAGE** — allocate resources to treat the risks that have been mapped and measured.

- Manage 1: Risks are prioritised and responded to based on Map and Measure.
- Manage 2: Strategies to maximise benefit and minimise harm are documented.
- Manage 3: Third-party risks and benefits are regularly monitored.
- Manage 4: Treatment, response, recovery, and communication plans are documented.

The authoritative definitions are maintained by NIST at `airc.nist.gov`. This document summarises each function and focuses on Voight's relationship to it.

\newpage

# 3. Scope and Framing

## 3.1 Two Perspectives

This document separates two questions that are easily conflated:

- **"Does Voight help me run my AI RMF programme?"** — addressed in Part 1 (§4–§5).
- **"Does Voight govern its own AI risk?"** — addressed in Part 2 (§6).

A reader evaluating Voight as a tool for their own AI RMF cares about Part 1. A reader evaluating Voight as a vendor cares about Part 2. Keeping them apart avoids overstating Voight's own exposure and understating its value.

## 3.2 Where Voight Sits in the Four Functions

Voight is an observability platform. It captures telemetry about AI calls — model, tokens, latency, tool calls, cost, outcomes, and, subject to the customer's privacy settings, prompt and completion content. This shapes its role across the framework:

- **Measure** is Voight's home function. Measurement and tracking of AI risk over time is, almost exactly, what an observability platform does.
- **Map** is supported: Voight tells you what your AI system *actually* does in production — which models, which tools, which costs — the empirical ground truth that the Map function calls for.
- **Manage** is supported: Voight's alerts, traces, and records are the operational substrate for responding to and recovering from AI incidents.
- **Govern** is informed, not implemented: Voight supplies the evidence and audit trail that governance relies on, but the policies, accountability structures, and risk-tolerance decisions are organisational and remain with the customer.

Throughout Part 1, "Voight supports" should be read in this sense: Voight supplies measurement, operational evidence, and audit trails — the data layer an AI RMF programme runs on, not the programme itself.

\newpage

# 4. Part 1 — How Voight Supports the Four Functions

## 4.1 GOVERN — Informed by Voight

**The function.** Govern establishes the organisational culture, policies, accountability, and oversight that the other three functions operate within. It is a management discipline, not a technical control.

**How Voight helps.** Voight does not write your AI policies or define your accountability structures — but it produces the evidence that makes governance real rather than aspirational:

- **Govern 1 (policies in place).** Voight's per-event `privacyLevel` stamp and immutable event records give a policy like "we scrub PII from AI telemetry" a verifiable audit trail, rather than an unenforced statement.
- **Govern 4 (safety-first culture).** Continuous visibility into production AI behaviour — cost, errors, anomalous tool use — supports the critical-thinking, monitor-everything posture the function calls for.
- **Govern 6 (third-party and supply-chain policy).** Voight's per-event model and provider attribution gives governance an accurate, live inventory of which third-party models the organisation actually depends on.

**Limits.** Govern is owned by your organisation. Voight informs it with evidence; it does not constitute governance, set risk tolerance, or assign accountability.

## 4.2 MAP — Supported by Voight

**The function.** Map establishes the context of an AI system and identifies its risks: what it is for, what it does, what it depends on, and whom it affects.

**How Voight helps.** Map is often run on *intended* design; Voight grounds it in *actual* production behaviour:

- **Map 2 (tasks and methods categorised).** Voight records which models and methods each agent actually invokes, so the system categorisation reflects reality, not just the design document.
- **Map 3 (capabilities, benefits, costs understood).** Voight measures real cost and token consumption per model and per agent — the empirical "cost" side of Map 3.
- **Map 4 (risks across components, including third-party).** Per-event provider attribution surfaces every third-party model in the request path, including ones introduced after the original mapping.

**Limits.** Voight supplies the operational facts; characterising societal and individual impact (Map 5) and deciding which risks matter remain analytical tasks your team performs.

## 4.3 MEASURE — Voight's Home Function

**The function.** Measure analyses, assesses, benchmarks, and tracks AI risk over time using quantitative and qualitative methods. This is, almost by definition, what an observability platform does.

**How Voight helps.** This is Voight's strongest alignment in the entire framework:

- **Measure 1 (methods and metrics applied).** Voight provides concrete, continuously collected metrics for every AI call: token counts (input, output, cache reads, cache creations), cost in USD, latency, outcome, and tool-call frequency and success rate.
- **Measure 2 (trustworthy characteristics evaluated).** Voight contributes direct signal to several trustworthiness characteristics: *privacy-enhanced* (local PII scrubbing with a `privacyLevel` audit stamp), *secure and resilient* (error and anomaly visibility), and *accountable and transparent* (full trace reconstruction via `withTrace`).
- **Measure 3 (track risks over time during deployment).** This subcategory is the heart of observability. Voight tracks identified risks continuously in production — cost trends, error rates, tool-usage drift, per-user consumption — with prior-window deltas and alerting when a metric departs from baseline.
- **Measure 4 (efficacy of measurement assessed).** Voight's dashboards and exports give stakeholders the artefacts they need to assess whether the measurement programme is working.

**Limits.** Voight measures the operational and security characteristics of AI calls. It does not, on its own, evaluate every trustworthiness characteristic — fairness and harmful-bias measurement, for example, require ground-truth datasets and evaluation tooling at the application layer. Voight supplies the runtime metrics; bias and fairness evaluation is a complementary discipline.

## 4.4 MANAGE — Supported by Voight

**The function.** Manage allocates resources to treat the risks that Map and Measure have surfaced: prioritising them, responding to incidents, and documenting residual risk.

**How Voight helps.**

- **Manage 1 (prioritise and respond).** Voight's alerts — cost spike, event surge, error rate, orphan spike — convert measured risk into a timely signal that drives response, and its severity context helps prioritise.
- **Manage 2 (documented response plans).** When an incident occurs, the full trace record (`withTrace`) is the evidence base for response and for the post-incident write-up.
- **Manage 3 (third-party risk monitored regularly).** Continuous per-event provider attribution means third-party model risk is monitored continuously, not just at onboarding.
- **Manage 4 (response, recovery, communication documented).** Voight's records and exports support the documentation and communication this subcategory requires.

**Limits.** Voight surfaces and evidences risk; it does not itself treat risk. The decision to throttle a model, roll back a deployment, or accept a residual risk is an action your team takes — Voight tells you, quickly, that the action is needed.

\newpage

# 5. The Generative AI Profile (NIST-AI-600-1)

In July 2024, NIST published a companion to the AI RMF: the **Generative AI Profile** (NIST-AI-600-1), which identifies risks unique to or amplified by generative AI and proposes actions to manage them. Because Voight is built specifically to observe generative-AI applications, several of these risks fall squarely in its measurement remit.

Selected GenAI Profile risks and Voight's contribution:

| GenAI Profile risk area | How Voight contributes |
| :--- | :--- |
| Information integrity / confabulation | Voight surfaces error rates and (via `log()` in `withTrace`) precursors such as "retrieval returned zero results"; factuality evaluation remains application-level |
| Data privacy | Local three-level PII scrubbing before any telemetry leaves the customer process; `privacyLevel` audit stamp |
| Information security | Full trace forensics for prompt-injection and output-handling incidents; error and anomaly alerting |
| Value chain and component integration | Per-event model and provider attribution gives a live inventory of the GenAI supply chain |
| Excessive resource consumption (environmental / cost) | Token and cost tracking with per-user attribution and spike alerts |

The GenAI Profile reinforces the same conclusion as the core framework: Voight's contribution is concentrated in measurement, monitoring, and the production of evidence, and is strongest where a risk has a measurable runtime signature.

\newpage

# 6. Part 2 — Voight's Own AI Governance

## 6.1 Does Voight Operate an AI System Today?

No. As of the issue date, Voight does not run a large language model or other AI system within its own production product. Voight ingests telemetry generated by *the customer's* AI systems and presents it. The "AI Apps" section of the product is named for the customer applications it observes, not for any AI operated by Voight.

Consequently, the AI RMF functions as applied to *Voight's own AI* have no production subject yet. What Voight governs today is a conventional web platform.

## 6.2 Platform Governance Baseline

| Control | Implementation |
| :--- | :--- |
| Transport security | TLS 1.3 on all public endpoints |
| Storage encryption | AES-256 at rest; secrets stored hashed |
| Authentication | Privy-brokered identity for users; hashed, revocable `vk_` keys for ingest |
| Access control | Least-privilege; production data access restricted and logged |
| Supply chain | Dependabot monitoring; npm packages published with provenance attestations |
| Logging and audit | 90-day retention; immutable event records with per-event privacy stamps |

These controls, documented in full in Voight's GDPR Compliance Documentation, are the governance baseline on which any future AI feature will be built.

## 6.3 Planned AI Features and Forward Commitment

Voight has AI-powered features on its roadmap, including **Smart Trace** (LLM-assisted trace explanation), **Prompt Scorer** (automated prompt quality and risk scoring), and **Debug Agent** (an agent that helps diagnose trace failures).

When these ship, Voight will itself operate AI systems and will fall within the AI RMF as a deployer. Voight commits:

> When any AI-powered feature reaches production, Voight will apply the AI RMF to that feature — establishing its context (Map), measuring its trustworthiness characteristics with the same telemetry we offer customers (Measure), and documenting its risk treatment and response plans (Manage) — and will re-version this document to record the assessment before the feature is generally available.

This mirrors the forward-commitment model Voight uses for planned sub-processors in its GDPR documentation: declare the change before it happens, and update the public record when it does.

\newpage

# 7. Coverage Summary

| Function | Voight role | Strength | Primary mechanism |
| :--- | :--- | :---: | :--- |
| GOVERN | Informs | Supporting | Audit trail, privacy stamps, model inventory as evidence |
| MAP | Supports | Moderate–Strong | Real production behaviour: models, tools, costs |
| MEASURE | **Implements (core)** | **Strongest** | Metrics, tracking over time, alerting, trace capture |
| MANAGE | Supports | Strong | Alerts, trace forensics, continuous third-party monitoring |

The shape of Voight's alignment is deliberate and honest: an observability platform is a **Measure** instrument that radiates outward into Map and Manage, and informs Govern with evidence. It is not, and does not claim to be, a governance programme.

\newpage

# 8. What Voight Does Not Do

In the interest of an honest record, Voight explicitly does **not** provide the following:

- **Governance itself.** Voight does not write policies, set risk tolerance, assign accountability, or make risk-treatment decisions (GOVERN, MANAGE). It supplies evidence for these; it does not perform them.
- **Bias and fairness evaluation.** Voight measures operational and security characteristics. It does not, on its own, evaluate fairness or detect harmful bias, which require ground-truth datasets and dedicated evaluation tooling (MEASURE 2).
- **Impact assessment.** Voight does not characterise societal or individual impact (MAP 5); that is an analytical task for your team.
- **Inline prevention or risk treatment.** Voight observes and alerts; it does not block, throttle, or roll back. Treatment actions are yours to take (MANAGE).
- **Factuality evaluation.** Voight does not assess whether a generative output is true (GenAI Profile information integrity).

Stating these boundaries is deliberate. An observability platform that claimed to deliver the whole AI RMF would be misrepresenting both the framework and itself.

\newpage

# 9. Governance and References

| Field | Value |
| :--- | :--- |
| Framework | NIST AI RMF 1.0 (NIST AI 100-1) |
| Companion | Generative AI Profile (NIST-AI-600-1) |
| Authoritative source | `airc.nist.gov` · `nvlpubs.nist.gov/nistpubs/ai/nist.ai.100-1.pdf` |
| Security contact | `team@voight.xyz` |
| Related documents | GDPR (`docs.voight.xyz/trust/gdpr`) · OWASP LLM Top 10 (`docs.voight.xyz/trust/owasp-llm`) |
| Review cycle | Every six months, and on publication of a new AI RMF version |

Voight commits to re-versioning this document when NIST publishes a new version of the AI RMF, and when any Voight AI-powered feature (§6.3) reaches production.

\newpage

# Annex A — Function-to-Capability Mapping

A reverse index: each Voight capability and the AI RMF categories it contributes to.

| Voight capability | Categories supported |
| :--- | :--- |
| Metrics: tokens, cost, latency, outcome | Measure 1, Measure 3, Map 3 |
| Tracking over time with baseline deltas | Measure 3, Manage 1 |
| Alerts: cost spike, event surge, error rate, orphan spike | Measure 3, Manage 1, Manage 4 |
| Full trace capture (`withTrace`) | Measure 2, Manage 2, Manage 4 |
| Three-level local PII scrubbing + `privacyLevel` stamp | Measure 2 (privacy), Govern 1 |
| Per-event model/provider attribution | Map 2, Map 4, Manage 3, Govern 6 |
| Per-user spend attribution | Measure 3, Map 3 |
| Immutable event records | Govern 1, Manage 4 |
| npm provenance + Dependabot (own supply chain) | Govern 6 |

\newpage

# Annex B — Trustworthiness Characteristics

The AI RMF defines seven characteristics of trustworthy AI. Voight's contribution to each:

| Characteristic | Voight contribution |
| :--- | :--- |
| Valid and reliable | Error-rate and outcome tracking surface reliability regressions |
| Safe | Anomaly and cost-spike alerting flag unsafe runtime behaviour |
| Secure and resilient | Trace forensics + alerting for injection and output-handling incidents |
| Accountable and transparent | Full trace reconstruction and immutable records provide an audit trail |
| Explainable and interpretable | Supporting only — Voight shows *what* happened, not model internals |
| Privacy-enhanced | Local three-level PII scrubbing before transmission; `privacyLevel` stamp |
| Fair, with harmful bias managed | Not covered — requires application-level evaluation tooling |

\newpage

# Annex C — Document Version History

| Version | Date | Change | Author |
| :--- | :--- | :--- | :--- |
| 1.0 | 2026-06-03 | Initial publication against AI RMF 1.0 + GenAI Profile. | Voight — Security Office |

\newpage

# Contact

For any question about this document or about how Voight supports AI risk management:

**Voight — Security Office**

`team@voight.xyz`

[voight.xyz/trust](https://voight.xyz/trust) · [docs.voight.xyz/trust](https://docs.voight.xyz/trust)

---

*This document is published by Voight and made available under the same terms as the Voight documentation. It describes Voight's voluntary alignment with the NIST AI Risk Management Framework and is not a certification by, or endorsement from, the National Institute of Standards and Technology.*
