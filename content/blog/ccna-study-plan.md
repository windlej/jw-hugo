---
title: "My CCNA Study Plan: Resources, Schedule, and How I'm Using Physical Lab Gear"
date: 2026-05-05
description: "What I'm actually doing to prepare for the CCNA 200-301, combining Jeremy's IT Lab, a physical Cisco 3750G, and GNS3. The honest version, not the highlight reel."
categories: ["Networking", "Career"]
tags: ["ccna", "cisco", "study", "homelab", "gns3", "certifications"]
draft: false
---

Target date: June 2026. Here's the actual plan — resources, schedule, lab setup, and where I'm struggling.

## Why the CCNA Matters for Me Specifically

I've been managing Cisco Meraki, Fortinet, and UniFi networks across 40+ client organizations for four years. I can configure a FortiGate firewall policy, troubleshoot a VLAN trunk, set up a site-to-site VPN, and triage a flapping BGP session at 2am. The CCNA doesn't teach me most of this — I'm already doing it.

What it does is close the credential gap. My resume says "L2 Helpdesk Technician." The CCNA says "this person understands networking at a verifiable level." Those are different signals to a hiring manager who gets 200 applications for a network engineer role. The cert completes the story that my experience already tells.

It also fills real gaps. My routing protocol knowledge is mostly practical and shallow — I can get OSPF running, but I haven't deeply understood LSA types, area design, or DR/BDR election. The CCNA forces that depth.

## The Resources

### Primary: Jeremy's IT Lab

[Jeremy's IT Lab on YouTube](https://www.youtube.com/@JeremysITLab) is the best free CCNA content available. The production quality is excellent, the pace is deliberate, and the free Anki flashcard deck that accompanies the course is genuinely useful for retention. I've watched the paid course ($10 on Udemy during a sale) which includes labs — worth it.

What makes Jeremy's stand out: he actually explains *why*, not just *what*. Understanding why Spanning Tree elects a root bridge the way it does is more durable knowledge than memorizing the election criteria.

### Supplementary: Boson ExSim

Practice exams are where most CCNA candidates find out what they actually know. Boson's ExSim is widely considered the closest approximation to real Cisco exam difficulty. I'm running practice exams from week 4 onward — not just at the end. Use them diagnostically, not just as a final check.

### Lab: Physical Gear + GNS3

This is where my situation is a bit unusual. Most CCNA candidates use Packet Tracer exclusively. I have physical gear.

**The Cisco 3750G stack** is direct exam prep for switching topics. VLAN creation, trunk configuration, STP, inter-VLAN routing with SVIs — all of it runs on the same IOS version the exam covers. There's something about console cabling into real hardware and seeing `%LINK-3-UPDOWN: Interface GigabitEthernet1/0/1, changed state to up` in a real terminal that makes the concepts stick differently than a simulation.

**GNS3** handles routing topologies that would require more physical hardware than I have. OSPF multi-area labs, basic BGP peering, route redistribution — all of this runs in GNS3 using IOSv images. I connect GNS3 topologies to my physical 3750G via a Cloud node bridged to my management network, which gives me an integrated virtual+physical lab.

## The Schedule

I'm working a full-time MSP job. This is built around that reality.

**Weeks 1–4:** Course content only. Jeremy's IT Lab, one section per weeknight. No labs yet — just understanding the concepts before touching gear.

**Weeks 5–8:** Parallel. Course content in the morning, lab work in the evening. One GNS3 topology per week corresponding to the week's topic.

**Weeks 9–12:** Lab-heavy. One hour of course review in the morning, two hours of lab work. Start running Boson practice exams at 60% exam difficulty.

**Weeks 13–16:** Practice exam focus. One full practice exam per week under timed conditions. Review every wrong answer until I understand the reason, not just the correct answer.

**Week 17+:** Schedule exam when consistently hitting 85%+ on Boson ExSim at full difficulty.

## Where I'm Actually Struggling

**Subnetting speed.** I can subnet correctly, but not at exam speed. I'm using [subnettingpractice.com](https://subnettingpractice.com) for five minutes every day until it's reflexive.

**Wireless concepts.** My real-world wireless experience is with Meraki and UniFi, which abstract away the RF concepts the CCNA tests. DSSS vs OFDM, non-overlapping channels, BSS vs ESS, WPA3 authentication — these are pure memorization for me because I don't interact with them at the physical layer in production.

**QoS.** Low-priority topic on the exam but worth understanding. I can configure QoS on Meraki through a policy, but I've never touched DSCP marking or queuing mechanisms at the IOS level.

## The Lab Topology I'm Using

I'll do a dedicated post on this with diagrams, but the short version:

- **GNS3:** 3–4 IOS routers for routing protocol labs (OSPF, BGP basics, static routing)
- **Physical 3750G:** All switching labs (VLANs, STP, EtherChannel, inter-VLAN routing)
- **Physical ASA 5516-X:** Firewall and ACL labs (NAT, extended ACLs, basic VPN)
- **Cloud node in GNS3:** Bridges virtual topology to physical lab for integrated scenarios

The integrated setup — where a GNS3 router exchanges OSPF routes with the physical 3750G — is particularly useful for understanding how virtual and physical topologies interact, which is relevant for real production environments and increasingly for cloud networking concepts.

## Tracking Progress

I'm checking off topics in Jeremy's official course checklist and tracking Boson practice exam scores in a spreadsheet. If I'm not consistently hitting 80%+ on a topic in practice exams after studying it, I go back to the material before moving on.

The target is June 2026. I'll post an update when I have a scheduled date, and a proper retrospective after I take the exam.
