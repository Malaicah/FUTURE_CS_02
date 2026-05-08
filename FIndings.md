# Phishing Email Detection & Awareness — Findings

**Task 2 | Cybersecurity Internship Program**
**Analyst:** [Nancy Cafti]
**Date:** 7th May 2026
**Dataset:** Real-world documented phishing cases (Norton, NordVPN, Keepnet Labs, MailGuard, IT Governance — 2024–2025)

---

## Table of Contents

- [Overview](#overview)
- [Classification Results](#classification-results)
- [Email-by-Email Findings](#email-by-email-findings)
- [Phishing Indicators Summary](#phishing-indicators-summary)
- [Attack Techniques](#attack-techniques)
- [Key Takeaways](#key-takeaways)
- [Full Report](#full-report)

---

## Overview

This document contains findings from the analysis of **5 real phishing emails** collected from trusted cybersecurity sources. Each email impersonated a well-known brand to steal credentials or financial information from victims.

> **Scope:** Email header analysis, sender domain verification, link inspection, and content review for social engineering tactics.

---

## Classification Results

| # | Brand Impersonated | Attack Type | Classification | Primary Risk |
|---|---|---|---|---|
| 1 | PayPal | Credential harvesting via typosquatted domain | PHISHING | Account & payment fraud |
| 2 | Microsoft Teams | Fake login page — credential theft | PHISHING | Corporate account breach |
| 3 | Apple ID | Account lock scare + payment data theft | PHISHING | Identity & financial theft |
| 4 | Netflix | Billing failure — credit card harvesting | PHISHING | Credit card fraud |
| 5 | IRS | Fake tax refund — social engineering | SUSPICIOUS | Identity theft via SSN |

> **Result: 4 confirmed Phishing · 1 Suspicious · 0 Safe**

---

## Email-by-Email Findings

### 1. Fake PayPal Alert

```
From    : PayPal Support <service@paypa1-secure.com>
Subject : Action Required: Suspicious Activity Detected on Your Account
Link    : http://paypa1-secure.com/verify-account
```

| Indicator | Finding | Severity |
|---|---|---|
| Spoofed domain | `paypa1-secure.com` — number `1` replaces letter `l` | CRITICAL |
| Generic greeting | Says "Dear Customer" — PayPal always uses your registered name | HIGH |
| Urgency language | Threatens permanent account suspension to force a quick click | HIGH |
| Malicious link | Leads to a fake PayPal login page that captures credentials | CRITICAL |

**Technique:** Typosquatting + fear tactics

---

### 2. Fake Microsoft Teams Notification

```
From    : Microsoft Teams <noreply@micros0ft-teams.net>
Subject : You Have a New Message Waiting — Sign In to View
Link    : http://micros0ft-teams.net/signin
```

| Indicator | Finding | Severity |
|---|---|---|
| Typosquatted domain | `micros0ft-teams.net` — zero `0` replaces letter `o` in Microsoft | CRITICAL |
| Wrong domain | Legitimate Teams emails only come from `@microsoft.com` | CRITICAL |
| Mobile exploit | 85% of users view emails on phones where the full domain is hidden | HIGH |
| Credential harvesting | Fake login page sends captured passwords directly to attacker | CRITICAL |

**Technique:** Typosquatting + mobile display name exploit

---

### 3. Fake Apple ID Lock Alert

```
From    : Apple <no-reply@apple-id-security.support>
Subject : Your Apple ID Has Been Locked — Immediate Verification Required
Link    : http://apple-id-security.support/unlock
```

| Indicator | Finding | Severity |
|---|---|---|
| Fake domain | `apple-id-security.support` — Apple only sends from `@apple.com` | CRITICAL |
| `.support` TLD abuse | Cheap alternative TLD used to mimic Apple branding | HIGH |
| Requests card details | Asks for credit card to "verify identity" — Apple never does this | CRITICAL |
| Fear tactic | "Account locked" triggers panic and bypasses rational thinking | HIGH |

**Technique:** Fear tactics + credential and payment data harvesting

---

### 4. Fake Netflix Billing Notice

```
From    : Netflix <billing@netflix-payments.info>
Subject : Your Netflix Subscription Has Been Suspended — Update Billing Now
Link    : http://netflix-payments.info/update-billing
```

| Indicator | Finding | Severity |
|---|---|---|
| Fake domain | `netflix-payments.info` — Netflix only communicates from `@netflix.com` | CRITICAL |
| `.info` TLD abuse | Legitimate subscription services use `.com` — not `.info` | HIGH |
| Artificial deadline | "Within 24 hours" is designed to stop the user from thinking carefully | HIGH |
| Card data theft | Fake page collects full card number, expiry, and CVV | CRITICAL |

**Technique:** Urgency creation + billing data harvesting

---

### 5. Fake IRS Tax Refund Notice

```
From    : Internal Revenue Service <refund@irs-tax-refund.com>
Subject : You Are Eligible for a Tax Refund — Submit Your Details
Link    : http://irs-tax-refund.com/claim-refund
```

| Indicator | Finding | Severity |
|---|---|---|
| Wrong TLD | IRS only operates from `.gov` domains — any `.com` IRS email is fake | CRITICAL |
| No email contact policy | The IRS never initiates contact by email — always by postal mail | HIGH |
| SSN request | Asking for a Social Security Number via email enables full identity theft | CRITICAL |
| Reward bait | Unexpected refund promise lowers the victim's guard | HIGH |

**Classification note:** Marked SUSPICIOUS (not confirmed Phishing) because this exact pattern is also used in corporate security awareness training simulations. In a real-world inbox, treat it as Phishing and delete immediately.

---

## Phishing Indicators Summary

| Indicator | Emails | Severity |
|---|---|---|
| Spoofed / typosquatted domain | 1, 2, 3, 4, 5 | CRITICAL |
| Fake login / credential harvesting page | 1, 2, 3, 4 | CRITICAL |
| Request for payment or financial details | 3, 4, 5 | CRITICAL |
| Urgency / threat language | 1, 3, 4, 5 | HIGH |
| Generic greeting — not personalized | 1, 4, 5 | HIGH |
| Wrong domain extension (`.info`, `.support`, `.com` for `.gov`) | 3, 4, 5 | HIGH |
| Brand logo and style impersonation | 1, 2, 3, 4, 5 | HIGH |
| Mobile display name exploit | 2 | HIGH |

---

## Attack Techniques

| Technique | Description | Seen In |
|---|---|---|
| **Typosquatting** | Domain with one character swapped to mimic a real brand (e.g. `paypa1.com`) | 1, 2 |
| **Brand Impersonation** | Copying logos, colors, and writing style of trusted companies | All |
| **Fear & Urgency** | Language like "account locked" or "24 hours" to stop rational thinking | 1, 3, 4, 5 |
| **Credential Harvesting** | Fake login pages that send captured passwords to the attacker | 1, 2, 3, 4 |
| **Social Engineering** | Exploiting user trust in well-known brands rather than hacking technology | All |
| **Too-Good-To-Be-True** | Promising refunds or rewards to lower the victim's defenses | 5 |

---

## Key Takeaways

- All 5 emails used spoofed domains — **always check the full sender address**, not just the display name
- Fear and urgency were the most common psychological triggers across all emails
- Mobile users are at higher risk because phone email apps often hide the full sender domain
- No advanced technology was needed — these attacks succeed entirely through deception
- The IRS, Apple, PayPal, Microsoft, and Netflix **never ask for credentials or card details via email links**

---

## Full Report

The complete analysis including detailed indicator tables, classification guide, and prevention guidelines is available here:

📄 [`Phishing_Detection_Awareness_Report.docx`](./Phishing_Detection_Awareness_Report.docx)

---

*Task 2 — Phishing Email Detection & Awareness System*
*Sources: Norton · NordVPN · Keepnet Labs · CertifID · MailGuard · IT Governance (2024–2025)*
