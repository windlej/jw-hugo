---
title: "SIEM Platforms Compared: Kibana vs Perch vs Splunk From an MSP Seat"
date: 2026-03-18
description: "Managing security operations across 40+ organizations gave me hands-on time with multiple SIEM platforms. Here's what actually matters when you're the one writing detection rules at 11pm."
categories: ["Security"]
tags: ["siem", "kibana", "perch", "splunk", "security", "msp"]
draft: true
---

Most SIEM comparisons are written by vendors or analysts who've seen the demos. This one is written by someone who's used these platforms in production — ingesting real logs, tuning real alerts, and investigating real incidents across dozens of client environments. Here's what actually matters.

## The Three Platforms

I've had meaningful production time with:

- **Kibana (ELK Stack)** — primary SIEM at my current MSP for security operations across municipal government clients
- **Perch Security** — co-managed SIEM platform purpose-built for MSPs, used across 40+ client organizations
- **Splunk** — exposure through client environments and hands-on study; included here for completeness against the standard that everyone measures against

---

## Kibana (ELK Stack)

Kibana is the visualization layer on top of Elasticsearch and Logstash — the "K" in ELK. When MSPs or in-house teams build a SIEM on ELK, Kibana is the interface where analysts actually work.

**What it does well:**

The query language (KQL for basic filtering, Lucene for complex queries) is reasonably approachable once you've spent time with it. Dashboards are fully customizable — you can build exactly the views your clients need, not whatever a vendor decided was important. If you have the engineering resources to tune it, the result is a powerful tool.

The data pipeline is flexible. You can ingest almost anything with the right Logstash or Beats configuration. For municipal government clients with legacy systems logging in non-standard formats, that flexibility matters.

**What it doesn't do well:**

Out of the box, Kibana is a visualization tool, not a detection platform. Building meaningful detection requires you to write the rules, build the dashboards, tune the thresholds, and own the alert logic yourself. That's fine if you have a dedicated security engineer. In an MSP where one person is managing security operations for 15 clients simultaneously, it's a real resource problem.

Alert correlation is also not native in the way it is in commercial SIEMs. You can get there with Watcher/Alerting, but it requires investment. Splunk and Microsoft Sentinel both handle correlation more naturally out of the box.

**Bottom line for MSPs:** High ceiling, high floor of effort. Best fit for teams that have the engineering depth to build and maintain it, or environments where customization requirements are complex enough to justify the overhead.

---

## Perch Security

Perch is a co-managed SIEM built specifically for MSPs. It ingests network metadata (via a sensor on-prem), endpoint logs, and cloud log sources, and surfaces alerts through a shared SOC model — their analysts plus yours.

**What it does well:**

The deployment model is genuinely MSP-friendly. You drop a sensor on the client's network, it starts ingesting data, and within hours you have visibility. Compare that to standing up an ELK stack from scratch.

The co-managed SOC element is a real differentiator. Perch analysts review alerts and escalate the ones that matter, which means MSP technicians aren't drowning in raw alert volume. For teams without dedicated security staff, that filtering layer is the difference between SIEM being useful and SIEM being noise.

Network visibility is a particular strength. The sensor watches east-west traffic, DNS queries, and connection metadata — threat hunting on network behavior, not just log events.

**What it doesn't do well:**

The customization ceiling is lower than ELK. You work within Perch's detection framework, not your own. If you have a specific threat detection use case that doesn't fit the platform's built-in rules, your options are limited.

The co-managed model also means you're partially dependent on Perch analysts for escalation quality. The consistency of that experience varies.

**Bottom line for MSPs:** Best fit for MSPs that need security monitoring coverage without the engineering overhead to run a full SIEM internally. Solid network visibility, good escalation workflow, limited customization.

---

## Splunk

Splunk is the enterprise SIEM standard. The SPL query language is powerful, the detection capabilities are mature, and the ecosystem of apps and integrations is enormous.

**What it does well:**

SPL (Search Processing Language) is genuinely excellent for complex log analysis. Once you learn it, you can slice event data in ways that would be cumbersome in KQL or Lucene. The Splunk ES (Enterprise Security) layer adds structured incident management on top of the raw search capability.

The community content is substantial. The Splunk Security Essentials app ships hundreds of pre-built detection rules mapped to MITRE ATT&CK. If you want to get detection coverage quickly, the content library is a real advantage.

**What it doesn't do well:**

Cost. Splunk's licensing model has historically been ingest-volume-based, which makes it expensive at scale and particularly punishing when log volumes spike during incidents (exactly when you most need your SIEM to be ingesting everything). The shift toward entity-based licensing has improved this, but enterprise Splunk deployments are still significant budget line items.

**Bottom line:** If budget isn't a constraint and you need a mature, well-documented enterprise SIEM, Splunk is hard to argue with. For MSPs and smaller security teams, the cost structure is often prohibitive.

---

## The Honest Comparison

| | Kibana | Perch | Splunk |
|---|---|---|---|
| **Setup time** | Days–weeks | Hours | Days |
| **Cost** | Low (infra cost) | Mid (subscription) | High |
| **Customization** | Very high | Low | High |
| **Detection out-of-box** | Low | Medium | High (with ES) |
| **MSP deployment model** | DIY | Purpose-built | Enterprise |
| **Query language** | KQL/Lucene | Limited | SPL |
| **Best for** | Engineering-heavy teams | MSP coverage model | Enterprise SOC |

---

## What I'd Use Now

If I were building a security operations capability from scratch at an MSP today, I'd look seriously at **Microsoft Sentinel** before any of the three above — especially if the client base is heavily Microsoft 365. The free E5 developer sandbox, native integration with Defender and Entra ID logs, KQL similarity to familiar tooling, and SOAR capabilities are a compelling combination.

That's a post for another day. The short version: the SIEM landscape has shifted, and the right answer in 2026 is probably different than it was in 2023.
