# Maxim Markelow — CV

[← Back to profile](README.md)

**Engineering Manager — Security & .NET Platform**

I build engineering teams and the platforms they run on. At Mindbox, a B2B customer data platform, I first ran the internal .NET platform tribe: I cut the monolith's time-to-market from 12 to ~4 hours and moved the whole company from GitHub to GitLab. Then I took over security and became its functional owner. I treat security as an engineering discipline: controls, detection and access are all code. Before Mindbox I spent a decade in .NET, going from intern to team lead, and grew a product team from one developer to six.

✉️ [markelow.dev@gmail.com](mailto:markelow.dev@gmail.com) · 💼 [LinkedIn](https://www.linkedin.com/in/maxim-markelow-a24573123/)

---

## About

- **Platform first, then security.** I came to security from developer platform work, so I build controls into the delivery path (pipelines, templates, IDP) rather than on top of it.
- **Non-blocking by default.** The mandate I work under is "security must not slow delivery". In practice this means self-service with structured justification and asynchronous audit instead of approval gates, with delivery speed kept as a health metric of the security team itself.
- **Hands-on manager.** I was a playing coach for most of my career. I still design architecture, review ADRs and write the first version of tools when that's the fastest way to set direction.
- **AI in the loop, not in charge.** My team uses AI agents for triage, questionnaires, access reviews and mass refactorings, with guardrails for everyone else using them.

---

## Selected outcomes

| Area | Result |
|---|---|
| Delivery speed | Average monolith time-to-market **12h → ~4h**; failed production rollouts **50% → 18%**; p95 deploy time **3h → 1h** |
| Developer platform | Company-wide **GitHub → GitLab** migration; **111 of 111** services deployable by click via Backstage IDP |
| Detection & response | In-house SIEM + SOAR with auto-blocking; **90% of critical alerts handled within 30 min** |
| Data protection | Own PII discovery scanner across Kafka, MS SQL and Postgres, replacing a foreign vendor |
| Team | eNPS **13 → 50** after a hiring wave; zero attrition across several half-years; engineers promoted to lead roles in other tribes |

---

## Things I built

### Delivery pipeline turnaround
The CDP monolith took ~12 hours on average to go from merge to production, and half of production rollouts failed. We covered the pipeline with quality metrics first, then worked on the worst stages. Average TTM dropped to ~5 hours within a half-year and later to ~4 hours. Failed rollouts fell from 50% to 18%, post-deploy test failures from 12.5% to ~5%, and p95 deploy time from 3 hours to 1 hour. TTM stayed a health metric for the team after it moved into security, so security work was never allowed to slow delivery again.

### GitHub → GitLab migration
I led the company-wide move of all private code, issues and CI from GitHub to GitLab. It included unified pipelines for C# libraries (52 repositories) and microservices, an Artifactory rollout for dependency caching and resilience to external registry outages, and the move to GitLab Premium. GitHub was switched off; public repositories stay there and are mirrored.

### Internal Developer Platform
The goal was to stop product developers from writing infrastructure code. We deployed Backstage and added 111 services, each deployable by click into a new environment. Most of them are described declaratively up to production-ready state, and changes ship through the declaration without direct production access. New services are created from a template with Postgres, Kafka, S3, Redis, DragonFly, ClickHouse, RabbitMQ and imgproxy provisioned out of the box. The service catalog is enriched with ownership and docs-as-code.

### Detection & response platform
A SIEM on cross-cluster OpenSearch with detection-as-code, built in-house after a managed cloud offering was rejected on budget. Log sources cover product events, Linux/Windows hosts, cloud audit trails, Vault, Teleport, MS SQL, YugabyteDB and Postgres. On top of it sits an in-house SOAR. It automatically blocks suspicious users and terminates sessions in the product, Linux, the cloud, Vault, MS SQL and YugabyteDB, and every automated action has a mandatory revert and a TTL. An on-call rotation holds a reaction SLO of 30 minutes for 90% of critical alerts. Runtime detection runs with Falco (eBPF) on every Kubernetes cluster. The platform was later re-architected to cut hardware costs by ~₽320K/month while ingesting more logs.

### PII discovery (DSPM)
I built our own scanner for personal data and secrets, replacing a foreign vendor after a risk-storming session surfaced blockers that later proved real. It covers Kafka, MS SQL and Postgres. It produces a PII map with a criticality score per store, and that score drives the hardening backlog handed to owning teams, starting with dynamic credentials for the most sensitive Kafka clusters.

### Governed AI-built apps for non-engineers
I set up the process and platform that let non-engineering staff ship AI-built internal apps safely. They work in an isolated GitLab space with their own runners and no access to developer secrets, and they can't touch production code without engineer approval. Apps run behind VPN on a self-hosted PaaS with data kept in-country.

---

## Experience

### Mindbox — Engineering Manager
*June 2024 – present* 
*B2B SaaS customer data platform · 500+ employees · ~250 engineers*

**Framework tribe (internal .NET platform), 2024–2025.** I joined as the dedicated EM of the .NET platform tribe.
- Led the GitHub → GitLab migration, the delivery pipeline turnaround and the IDP (see above).
- Brought operational toil down and kept it flat, reaching zero defects caused by release management.
- Built a paid internship that shipped 10 of 10 workflow presets now used daily by account managers.
- Used AI agents for mass, repetitive refactorings across services and turned it into a shared practice.

**SecOps tribe, 2025 – present.** Security started as a second lane inside Framework. I split it into its own tribe, then merged the .NET platform team back into it to get enough hands. I am the functional owner of security, accountable for SecOps, DevSecOps and AppSec, and I report to the CTO. The tribe has 12 people: PM, architect, SecOps lead, information security officer, SRE and 7 engineers.
- **Operations.** Turned security from a set of one-off projects into a service: on-call for SIEM alerts, incident response including customer communication, a ticketed intake for security requests, and a consultation process.
- **Detection & response.** SIEM, SOAR and runtime detection (see above). Code exfiltration detection via GitLab webhooks. Led response to a 2026 npm supply-chain compromise using a phased IR runbook.
- **Identity & access.** M2M authorization with key rotation (see above). Audited and rolled out a role model for cloud IAM, took over Authentik (SSO/OIDC), moved CI off static tokens for Vault and Artifactory, and moved GitLab to scoped service accounts. Designed the vision for a new product role model that replaces ~200 loosely related permissions.
- **Supply chain & AppSec.** Deployed DefectDojo and rolled out Gitleaks and Trivy across repositories after the commercial scanner failed in our setup. Ran a SAST evaluation across 12 tools on ~40 criteria and chose Opengrep as the self-hosted baseline. Replaced a proprietary attack-surface management tool.
- **Product security.** Shipped IP allowlisting for customer-facing APIs (integrations, bulk API, delta sharing) for enterprise plans, adopted by 8+ customers. Delivered WAF and GOST TLS support that unblocked enterprise deals and a banking integration.
- **Compliance.**  The ISO 27001 audit was passed with no critical or high findings.
- **AI in security operations.** Automated triage of leaked secrets and vulnerable dependencies, answers to customer security questionnaires, and review of IAM access requests. Built an agent skill that guides on-call through PII-leak investigations.
- **People.** Onboarded a SecOps lead, grew an SRE inside the team, and introduced co-mission-leads as a repeatable growth path. Two engineers were promoted into lead roles in other tribes. I am the bar raiser for all .NET hiring company-wide and redesigned the interview framework around a competency library.

### SIIS Ltd — Team Lead

*Oct 2018 – Jun 2024 · 5 yrs 9 mos*
*[Survey Studio](https://surveystudio.ru/): platform for market research and survey operations*

Playing coach. I grew the team from 1 backend developer to 5 developers + QA and owned everything from customer requirements and architecture to processes and mentoring.

- **Platform modernisation.** Migrated from .NET Framework 4.5 to .NET Core 3, from LINQ to SQL to Entity Framework, and from MS SQL to PostgreSQL.
- **Monolith to microservices.** Split the monolith into services.
- **Product merger.** Merged two products into one with cross-tenant interaction.
- **"Uber for call centres."** A marketplace that matches survey requests with call centres.
- **Online panel.** Built the online respondent panel.
- **Scale.** Designed storage and web applications for ~1,000 RPM and tens of terabytes of data.
- **Performance.** Optimised the system end to end, from queries and stored procedures to hot paths.
- **Analytics.** Built a dashboard builder and custom analytics.
- **Open source.** Authored the libraries that grew into [Curiosus Dev](https://github.com/curiosus-dev) (see below).

### SCOUT Group — .NET Developer → Team Lead

*Nov 2014 – Oct 2018 · 4 yrs*
*[SCOUT](https://scout-gps.ru/): Telematics and fleet management*

- **Team Lead** (Mar 2018 – Oct 2018): led project teams, worked with customers, wrote specs, took part in tender preparation, and migrated the Journey Management System to a REST API with an Angular front end.
- **Middle .NET Developer** (Dec 2016 – Mar 2018): built an automated dispatcher plugin that solves the travelling salesman problem for commercial fleet routing. Developed the Journey Management System (planned vs actual trips, live location and violation tracking, reporting, notifications) and an internal set of corporate libraries.
- **Junior .NET Developer** (Sep 2015 – Dec 2016): worked on product features, reports and analytics.
- **Intern** (Nov 2014 – Sep 2015): built a parser for tachograph DDD files and driver working-time reports.

---

## Open source

Author and maintainer of [**Curiosus Dev**](https://github.com/curiosus-dev), pragmatic .NET libraries born from real projects:

| Project | What it does |
|---|---|
| [Curiosus.Migrations](https://github.com/curiosus-dev/Curiosus.Migrations) | Database migrations with SQL scripts and C# code: downgrades, long-running migrations, policies |
| [Curiosus.Utils](https://github.com/curiosus-dev/Curiosus.Utils) | Building blocks for .NET services: configuration, hosting, data access, email and SMS, notifications |
| [Curiosus.TelegramBot](https://github.com/curiosus-dev/Curiosus.TelegramBot) | Infrastructure for Telegram bots: command dispatching, multi-step state, persistent update queue |

---

## Stack

**Languages:** C# / .NET (ASP.NET Core, EF Core, GraphQL), TypeScript

**Platform:** GitLab CI, Kubernetes, Backstage, JFrog Artifactory, Octopus Deploy, Yandex Cloud, Docker, Grafana

**Security:** OpenSearch, custom SOAR, Falco, DefectDojo, Trivy, Gitleaks, Opengrep, Renovate, Authentik, HashiCorp Vault, Teleport, OWASP ASVS, MITRE ATT&CK, ISO 27001

**Data:** PostgreSQL, Kafka, Redis, RabbitMQ

---

## Education

**ITMO University**, Saint Petersburg
- M.Sc., Intelligent Information Systems — 2016–2018 (GPA 4.9 / 5)
- B.Sc., Software Engineering — 2012–2016 (GPA 4.7 / 5)

## Languages

Russian (native) · English B2
