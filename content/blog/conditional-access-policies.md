---
title: "Entra ID Conditional Access: Real Policies, Real Scenarios, What to Actually Enforce"
date: 2026-02-28
description: "I've built Conditional Access policies for 100+ organizations. Here's the framework I actually use — and the mistakes I've watched organizations make by not having one."
categories: ["Security", "Cloud"]
tags: ["entra-id", "conditional-access", "azure", "mfa", "zero-trust", "microsoft"]
draft: true
---

Conditional Access is one of those features where the gap between "we have it enabled" and "we have it configured correctly" is wide enough that attackers drive through it regularly. I've managed CA policies across 100+ organizations at two MSPs. Here's the framework I've landed on.

## The Foundation: What CA Actually Is

Conditional Access is Entra ID's policy engine. Every sign-in attempt hits it, and the policy evaluates conditions — who is signing in, from where, on what device, to what application — and makes a decision: allow, block, or allow with requirements (MFA, compliant device, etc.).

The mental model I use: CA is a firewall for identity, not for packets. It doesn't replace your network firewall. It controls access at the identity layer, which is increasingly where attacks live.

## The Five Policies Every Organization Needs

### 1. Block Legacy Authentication

Legacy authentication protocols — IMAP, POP3, Exchange ActiveSync, SMTP AUTH, older Office client protocols — don't support modern authentication. They can't satisfy MFA challenges. If you have a CA policy requiring MFA but an attacker authenticates via SMTP AUTH using a harvested credential, the MFA requirement doesn't apply.

Microsoft's own data suggests the majority of password spray attacks use legacy authentication. Blocking it is high impact, low disruption — most modern clients don't use these protocols.

```
Assignments:
  Users: All users
  Cloud apps: All cloud apps
  Conditions → Client apps: Exchange ActiveSync clients, Other clients

Access controls:
  Grant: Block access
```

**Before you enable:** Run it in Report-Only mode for two weeks and review the sign-in logs. You'll find the legacy clients that need to be migrated first.

### 2. Require MFA for All Users

This is table stakes. If a credential is compromised, MFA is the control that keeps the account from being fully taken over.

```
Assignments:
  Users: All users (exclude break-glass accounts)
  Cloud apps: All cloud apps

Access controls:
  Grant: Require multi-factor authentication
```

**The break-glass exception matters.** Break-glass accounts are emergency access accounts excluded from all CA policies. They exist so you can get into the tenant if something goes wrong with your MFA configuration. Every organization needs them. Every organization should have audit alerts on when they're used.

### 3. Require Compliant Device for High-Value Apps

This policy requires that the device accessing Exchange Online and SharePoint is enrolled in Intune and meets compliance requirements (BitLocker, current OS, AV running). It closes the gap where MFA alone isn't enough — a user on a compromised personal device can satisfy MFA and still be a risk.

```
Assignments:
  Users: All users (or target group)
  Cloud apps: Exchange Online, SharePoint Online

Conditions:
  Device platforms: Windows, macOS

Access controls:
  Grant: Require device to be marked as compliant
```

**Start with Report-Only.** This policy will surface devices that are unmanaged. You need to know what you're blocking before you block it.

### 4. Block Sign-Ins from Non-Allowed Countries

If your organization operates in the US and occasionally in Canada, there's no legitimate reason for a sign-in to originate from Romania, Russia, or China. Named locations let you define allowed geographies.

```
Assignments:
  Users: All users
  Cloud apps: All cloud apps
  Conditions → Locations: Any location (exclude named "Allowed Countries")

Access controls:
  Grant: Block access
```

**Named Locations** — create a named location list with the countries your users actually operate in. Include VPN exit countries if your company uses a VPN with fixed exit IPs.

### 5. Sign-In Risk Policy (Requires Entra ID P2)

Entra ID P2 includes sign-in risk evaluation — Microsoft's real-time assessment of whether a sign-in looks suspicious based on threat intelligence, leaked credentials, anonymous IPs, impossible travel, etc.

```
Assignments:
  Users: All users
  Cloud apps: All cloud apps
  Conditions → Sign-in risk: High

Access controls:
  Grant: Block access (or: Require MFA + change password)
```

For Medium risk, requiring MFA with a password change is a reasonable response that doesn't immediately lock users out while still forcing remediation.

---

## Common Mistakes

**Mistake 1: No break-glass account.** Organizations lock themselves out of their own tenant by applying overly broad CA policies without an excluded emergency account. This is the most dangerous configuration mistake.

**Mistake 2: Skipping Report-Only mode.** Every new policy should run in Report-Only for at least two weeks before enforcement. The "what would this block?" question has a real answer in the logs — use it.

**Mistake 3: Excluding too many users "temporarily."** Exclusions for pilot groups are fine. Exclusions that grow indefinitely because someone complains about MFA aren't. Audit your exclusions quarterly.

**Mistake 4: Not monitoring break-glass usage.** If someone signs in with a break-glass account outside of a real emergency, you need to know. Set up an alert (Azure Monitor or Sentinel) on sign-ins from break-glass account UPNs.

**Mistake 5: Treating CA as a set-and-forget control.** The threat landscape changes. Microsoft adds new signal types. Your org acquires new apps. Review CA policies quarterly.

---

## The What-If Tool

Before you make any CA change in production, run it through the **What-If** tool in Entra ID. It lets you simulate a sign-in with specific attributes — user, location, device platform, app — and shows you exactly which policies apply and what decision they reach.

It's in the Entra admin center under Protection → Conditional Access → What If. Use it every time.

---

## Licensing Note

Policies 1–4 require Entra ID P1, which is included in Microsoft 365 Business Premium and Microsoft 365 E3. Policy 5 (risk-based) requires Entra ID P2, included in Microsoft 365 E5 or available as an add-on.

If your clients are on Business Basic or Business Standard, they don't have CA at all — that conversation is worth having proactively.
