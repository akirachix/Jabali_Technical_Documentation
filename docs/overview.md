# Overview

Welcome to the **Rejesha Green** technical documentation. This overview covers what the product is, the problem it solves, who it's for, and what makes it unique.

## Product Definition

**Rejesha Green** is a digital forest-management platform designed to support Community Forest Associations (CFAs), CFA members, KFS officials, forest rangers, and conservation organizations. It enables users to replace manual, paper-based forest-management processes with a centralized digital system, providing them with streamlined member registration, permit requests, illegal-activity reporting, conservation planning, and tree-restoration monitoring.

Members must be communities within the legal **5-kilometre boundary** adjacent to the forest.

The platform uses:

- **Mobile application** for CFA officials registering CFA members
- **USSD services** for members using feature phones or smartphones to request permits and report incidents
- **SMS notifications and reminders** for CFA members
- **Mobile money payments via M-Pesa** for registration and permit fees

---

**What the Product Does**

Rejesha Green digitizes the manual process of member registration for Community Forest Associations. The current manual process is tiresome and time-consuming; Rejesha Green is designed to ease the work. Registered CFA members can request forest resources, report illegal activities, and engage in conservation activities to enhance forest restoration.

Product Goal

The main goal of Rejesha Green is to **digitize the registration of Community Forest Association members** to help in the restoration of forests.

Other goals include:

- Improve communication between CFA officials and members
- Make forest-resource permit requests faster and more transparent
- Enable faster reporting of illegal forest activities
- Improve coordination of tree planting and other conservation activities
- Track planted trees and their survival rates
- Provide KFS officials with timely reports for decision-making
- Improve accountability for membership and permit payments
- Support increased participation by forest-adjacent households

---

## Problem Statement

Before Rejesha Green, slow, manual, and paper-dependent operational systems was:

- **Time-consuming** — managing everything by hand takes too much time; physical travel and extensive paperwork cause months of registration delays
- **Fragmented** — no digital coordination tools — conservation activities managed via word-of-mouth, resource extractions tracked in messy, unverified paper log books
- **Error-prone** — manual record-keeping easily leads to lost records or mistakes
- **Inaccessible** — members waste too much time traveling to the office for registration, permits, and updates; KFS officials receive illegal reports too late

These challenges led to land degradation and desertification — 75 billion tonnes of fertile soil and 12 hectares lost annually. There was no unified solution that addressed a centralized, digital management system that streamlines member registration and improves communication to empower CFAs in their co-management duties.

---

**How the Product Solves the Problem**

Rejesha Green solves the problem by making the registration method easier and faster, enabling more members to be registered. More members means more hands helping in the restoration of damaged and degraded forests and land.

---

## Target Users

Rejesha Green is built for:

| User Type                    | Role                                                   | Pain Points Addressed                                                                                      |
| ---------------------------- | ------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------- |
| CFA Officials                | Forest association administrators using the mobile app | Managing everything by hand takes too much time and easily leads to lost records or mistakes               |
| CFA Members                  | Forest-adjacent community members using USSD/SMS       | Wastes too much time traveling to the office for registration, permits, and updates                        |
| KFS Officials                | Kenya Forest Service officers using the web dashboard  | Receives illegal reports late and is unable to arrest the victim on time                                   |
| NGOs & Conservation Partners | External organizations supporting restoration          | Lack of approved, timely reports to understand restoration progress and identify partnership opportunities |

**CFA Officials**

CFA officials use the **mobile application** to:

- Register new members
- Verify member information and eligibility
- Manage member records
- Create tree-planting and conservation activities
- Send activity notifications and reminders
- Record attendance and activity results
- Record planted trees and locations
- Update tree-survival information
- View membership, payment, permit, and activity reports

**CFA Members**

CFA members use **USSD and SMS services** to:

- Receive their membership identification number
- Receive notifications and reminders
- Request permits for forest resources
- Make payments through M-Pesa
- Receive permit confirmations by SMS
- Report illegal forest activities
- Receive updates about CFA activities

**KFS Officials**

KFS officials use the **web dashboard** to:

- View CFA membership information
- Monitor forest activities
- Review permit and resource-extraction reports
- View illegal-activity alerts
- Identify areas requiring ranger intervention
- Monitor tree-planting and tree-survival progress
- Review restoration reports

**NGOs and Conservation Partners**

NGOs can use approved reports to:

- Understand restoration progress
- Support CFA activities
- Identify opportunities for conservation partnerships

---

## Key Features

What makes Rejesha Green stand out:

**Feature 1: Member Onboarding**

CFA officials enter member details through the mobile app; the system verifies eligibility, records M-Pesa payment, creates a membership ID, and sends confirmation by SMS

**Feature 2: Membership Management**

Centralized database storing member profiles, membership status, payment history, and CFA information

**Feature 3: Forest-Resource Permits**

Members request permits via USSD, select resources (firewood, grass, medicinal plants, bamboo, honey), pay through M-Pesa, and receive permit numbers by SMS

**Feature 4: Illegal-Activity Reporting**

Members report incidents via USSD; reports are forwarded to KFS officials to support faster ranger deployment

**Feature 5: Activity Planning & Mobilization**

CFA officials create events (tree planting, patrols, clean-ups, nursery activities, meetings); members receive SMS invitations and reminders; attendance and results are recorded

**Feature 6: Tree & Restoration Monitoring**

Officials record trees planted, location, date, surviving/dead counts, and restoration progress over time

**Feature 7: Payments & Revenue Tracking**

M-Pesa integration for membership fees, renewals, and permit fees; payment records stored in financial reports

**Feature 8: Dashboards & Reports**

Web dashboard showing total members, revenue, permit rates, extraction volumes, illegal reports, event attendance, trees planted, and survival rates

### Technical Highlights

- **Mobile App (CFA Officials)** — Android app for member registration, activity creation, and tree monitoring
- **USSD Services** — Feature-phone and smartphone access for permit requests and incident reporting — no internet required
- **SMS Notifications** — Automated reminders, confirmations, and activity invitations via SMS
- **M-Pesa Integration** — Mobile money payments for registration fees and permit fees
- **Web Dashboard (KFS)** — Real-time monitoring of membership, permits, illegal alerts, and restoration progress
- **Centralized Database** — Single source of truth for all CFA records, payments, and activity data

---

## Informational Website

For more information about Rejesha Green, visit our official information website:
[Visit the Rejesha Green Information Website](https://rejeshagreen-vert.vercel.app/)
The website provides additional information about the platform, its purpose, services, and impact on forest communities.

## Workflow Overview

At a high level, Rejesha Green operates through **5 core workflows**:

_1. Member Registration_

CFA official opens app → enters member details → confirms eligibility → member accepts rules → M-Pesa payment → confirmed → membership number generated → confirmation SMS sent

_2. Resource Permit_

Member dials USSD → selects resource → system checks availability → M-Pesa payment → permit number generated → SMS sent

_3. Illegal Reporting_

Member opens USSD → selects incident → enters location/details → system records → KFS receives alert → ranger patrol assigned → response recorded

_4. Activity Management_

CFA official creates activity → members receive SMS invitation → reminders sent → attendance recorded → results recorded → report generated

_5. Restoration Monitoring_

Official records planting → enters location/number → later records surviving/dead → survival rate calculated → dashboard report

### Data Flow

```
User (USSD/App) ──▶ API Gateway ──▶ Backend Services ──▶ Database
         │                                              │
         └────────────◀──── SMS Response ◀───────────────┘
```

---

## Quick Links

- [Architecture](./architecture.md)
- [Backend](./backend.md)
- [Frontend](./frontend.md)
- [Security](./security.md)
- [Deployment](./deployment.md)

---
