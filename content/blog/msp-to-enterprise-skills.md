---
title: "MSP to Enterprise: Skills That Transfer and Gaps You Need to Close"
date: 2026-04-01
description: "Four years managing infrastructure for 100+ organizations taught me things I couldn't have learned anywhere else. Here's what transfers to enterprise — and what doesn't."
categories: ["Career"]
tags: ["msp", "career", "enterprise", "transition"]
draft: false
---

Four years in an MSP seat gives you something that's genuinely hard to get in enterprise IT: breadth under pressure. When you're responsible for network infrastructure across 40 different organizations simultaneously — each with different tools, different configurations, and different stakes — you develop a kind of situational awareness that pure deep-dive engineers often don't have.

But it also leaves gaps. Real ones. This post is an honest accounting of both.

## What Actually Transfers

### Blast Radius Thinking

In an MSP, a bad change doesn't just break one environment — it can break a dozen. You develop a reflex for asking "what else does this touch?" before you touch anything. This maps directly to enterprise change management.

Enterprise environments have change control boards and approval processes because the blast radius of a misconfigured firewall policy or a botched AD schema change is enormous. MSP engineers who've lived with high-consequence changes already think this way. It's not a skill you have to learn — it's a survival instinct you've already built.

### Multi-Vendor Fluency

I've managed Cisco Meraki, Fortinet, and Ubiquiti UniFi simultaneously for different clients. I know which platform is better for what use case because I've hit the limits of each one in production. Enterprise engineers who've only ever used one vendor stack frequently struggle when they encounter a different one. MSP engineers are comfortable with the concept of "same problem, different interface."

### Security Operations Breadth

Four years of EDR alerts, SIEM tuning, incident response, and Conditional Access policies across 40+ organizations gave me something most desktop support or infrastructure engineers don't have: genuine security operations experience. I've contained a ransomware infection. I've traced a compromised credential through Kibana logs to an IP in Eastern Europe. I've written Conditional Access policies that blocked the attack vector the next time.

That's not something you get from a textbook. It transfers directly to any enterprise security or infrastructure role.

### Documentation Discipline

MSP ticket management forces you to document in real time — not after the fact. When 15 engineers are working across the same client base, your ticket notes are the handoff. Enterprise teams have the same problem: shifts change, engineers move on, institutional knowledge walks out the door if it's only in someone's head. MSP engineers who've been held accountable to documentation standards bring that discipline with them.

---

## What You'll Need to Build

### Deep Routing Protocol Knowledge

MSP networking is largely management-plane work: configuring firewall policies, setting up VLANs, troubleshooting connectivity. You rarely touch OSPF, BGP, or EIGRP in a meaningful way. Enterprise network engineering lives in the routing table.

**What to do about it:** Get into a lab. GNS3 or EVE-NG, a CCNA course, and deliberate time with multi-area OSPF and basic BGP. The CCNA validates the fundamentals; the CCNP is where you get dangerous with routing protocols.

### Storage Architecture

MSP environments are mostly server administration — you manage Windows Server, not storage infrastructure. Enterprise shops care deeply about storage: iSCSI, NFS, Fibre Channel, vSAN, NetApp ONTAP. You probably haven't touched most of these in production.

**What to do about it:** A TrueNAS VM in your homelab gives you real iSCSI and NFS practice at zero cost. If you can get your hands on a NetApp ONTAP simulator, even better.

### Formal Change Management

MSP change control is often informal: you tell the client what you're doing, maybe get a reply, then do it. Enterprise change management involves change advisory boards, risk assessments, rollback plans, maintenance windows, and communication cascades to multiple stakeholders.

**What to do about it:** Document your homelab changes the way you would in a real change request. Get comfortable writing rollback procedures. If your MSP has any kind of change management process, get involved in it.

### Project Ownership

MSPs are reactive by nature — you respond to tickets. Enterprise infrastructure roles often involve owning multi-month projects: network refreshes, cloud migrations, identity platform deployments. Leading a project from scoping through delivery is a different skill than closing tickets.

**What to do about it:** Find a project at your current job and own it end to end, even if it's small. Document the scope, build a timeline, communicate progress. The skill is in the process, not the scale.

---

## The Actual Honest Assessment

MSP experience is undervalued in enterprise hiring. A resume that says "L2 Helpdesk Technician" will get filtered before a human reads the bullets underneath it. That's the real problem to solve: positioning, not capability.

Your headline should reflect your actual work, not your job title. "Network & Security Engineer | Cisco Meraki · Fortinet · Azure | CCNA In Progress" tells a fundamentally different story than "L2 Helpdesk Technician."

The CCNA closes the credential gap on paper. The homelab gives you something concrete to talk about in interviews. The GitHub portfolio with automation scripts turns "I said I know Python" into "here's the repo."

The skills are there. The framing is the work.
