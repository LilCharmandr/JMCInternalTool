# JMC Internal Dashboards Platform
## Comprehensive Planning & Architecture Document

**Version:** 1.0  
**Date:** February 13, 2026  
**Classification:** Internal — Confidential  
**Prepared for:** JMC Leadership & Operations Team

---

# Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Strategic Objectives](#2-strategic-objectives)
3. [Full Module Breakdown with Functional Requirements](#3-full-module-breakdown-with-functional-requirements)
4. [User Roles & Permissions](#4-user-roles--permissions)
5. [Technical Architecture Recommendations](#5-technical-architecture-recommendations)
6. [Phased Implementation Plan](#6-phased-implementation-plan)
7. [Reporting & Dashboard Visualizations](#7-reporting--dashboard-visualizations)

---

# 1. Executive Summary

## 1.1 Purpose of the Platform

The JMC Internal Dashboards Platform is a centralized operational management system designed to unify all tracking, reporting, compliance, and financial oversight activities across every JMC program and camp into a single, authoritative platform. It replaces the current patchwork of Google Sheets, exported HTML tables, one-off trackers, and disconnected spreadsheets with an integrated dashboard system that provides real-time visibility, automated workflows, and role-based access control.

## 1.2 Current Operational Challenges

Today, JMC operations are managed through dozens of independent spreadsheets and manual processes:

| Challenge | Impact |
|---|---|
| **Fragmented data** — Compliance checklists, insurance policies, vendor contracts, program trackers, and training records live in separate Google Sheets with no relational links. | Leadership lacks a single source of truth. Answering cross-camp questions requires manually opening and comparing multiple files. |
| **No real-time visibility** — Static HTML exports of spreadsheets (e.g., `Compliance Checklist.html`, `Insurance.html`, `Vendor Contracts - Mosaic.html`) provide snapshots but are stale the moment they're exported. | Decision-making is delayed. Compliance gaps go undetected until manual audits. |
| **Error-prone formulas** — The current compliance checklist shows `#VALUE!` and `#REF!` errors in camp name, location, and date columns, indicating broken references as sheets grow. | Data integrity cannot be trusted. Staff waste time troubleshooting formulas instead of managing operations. |
| **No workflow automation** — Status tracking (e.g., "Needed" badges for YPT, Background Checks, CPR) requires manual updates with no automated reminders, escalations, or deadline triggers. | Items slip through the cracks. Compliance deadlines are missed. |
| **No role-based access** — Everyone with the sheet link has the same access. There is no differentiation between a Super Admin viewing financial data and a camp team member updating their own compliance status. | Sensitive financial and personnel data is exposed to all users. No audit trail exists for who changed what. |
| **Camp-specific requirements are hard to manage** — State-specific compliance items (Mandated Reporter for Georgia, Fingerprinting for Florida) appear as columns with "N/A" for non-applicable camps, cluttering the view. | Camp teams are confused by irrelevant fields. Conditional logic is not enforceable in flat spreadsheets. |
| **No integration with iUSA** — Participant management data (applications, waivers, health forms) lives in the iUSA system with no connection to the internal tracking tools. | Double data entry. Participant status must be manually reconciled across systems. |

## 1.3 Vision for Centralized Tracking

The JMC Internal Dashboards Platform will serve as the **operational command center** for all JMC programs. Every stakeholder — from executive leadership to individual camp teams — will access a single platform with views tailored to their role and responsibilities.

**Core Design Principles:**

- **Single source of truth** — One record per entity (person, camp, vendor, policy), linked across modules.
- **Real-time dashboards** — Live status indicators, progress bars, and alerts replace static snapshots.
- **Workflow-driven operations** — Defined processes with stages, approvals, escalations, and automated notifications.
- **Role-based access control** — Each user sees only the data and actions relevant to their role and camp(s).
- **Audit trail** — Every data change is logged with user, timestamp, and prior value.
- **Mobile accessibility** — Core dashboards and approval workflows are accessible from mobile devices during field operations.

## 1.4 Expected Impact

| Stakeholder | Impact |
|---|---|
| **Executive Leadership** | At-a-glance dashboards for cross-camp compliance, financial health, incident trends, and enrollment status. No more requesting reports — the data is live. |
| **Camp Teams** | Simplified views focused on their camp's tasks, deadlines, and compliance status. Automated reminders eliminate manual follow-ups. |
| **Finance** | Real-time budget vs. actual tracking per camp. Vendor payment status, reconciliation checklists, and 1099/W9 management in one place. |
| **Compliance** | Heatmap dashboards by camp, state, and role. Automated alerts for expiring certifications. Audit-ready documentation at all times. |
| **Operations** | Unified tracking for transportation, sites, insurance, swag, and vendor management. Contract expiration alerts and renewal workflows. |

## 1.5 Integration Goals

- **iUSA Integration** — Bidirectional sync for participant applications, waivers, health forms, and enrollment status. The platform will either consume iUSA APIs or implement a scheduled data import/export pipeline to ensure participant records are current without manual reconciliation.
- **Google Forms** — Intake integration for incident reports and escalation submissions (read-only ingestion from form responses).
- **Google Drive** — Document linking for invoices, confirmation PDFs, COIs, and policy documents (already partially in use).
- **Email / Notification Systems** — Automated alerts via email, and optionally Slack or Teams, for deadline reminders, approval requests, and escalation notifications.

## 1.6 Long-Term Scalability Objectives

- Support growth from the current ~12 camps to 25+ programs without schema redesign.
- Enable year-over-year data comparison and historical trend analysis.
- Provide a foundation for eventual external-facing portals (e.g., participant status lookup for parents).
- Support future modules (e.g., alumni engagement CRM, advanced analytics) without platform migration.
- Maintain sub-second dashboard load times with up to 100 concurrent users.

---

# 2. Strategic Objectives

Each objective below is defined with measurable key results (KRs) to enable tracking of platform success.

## 2.1 Increased Compliance Visibility

**Objective:** Every compliance requirement across all camps is tracked in real time with automated status indicators and alerts.

| Key Result | Metric | Target |
|---|---|---|
| KR1: Compliance dashboard accuracy | % of compliance items with current, verified status | 100% within 30 days of go-live |
| KR2: Time to detect compliance gaps | Hours from gap occurrence to alert | < 24 hours (automated) |
| KR3: State-specific compliance coverage | % of state-specific requirements modeled (FL fingerprinting, GA mandated reporter) | 100% |

## 2.2 Real-Time Financial Clarity Per Camp

**Objective:** Finance leadership can view budget vs. actual, outstanding payments, and vendor compliance for any camp at any time.

| Key Result | Metric | Target |
|---|---|---|
| KR1: Budget tracking latency | Days between expense and dashboard reflection | < 2 business days |
| KR2: Vendor payment visibility | % of vendors with complete W9/1099 status tracked | 100% |
| KR3: Financial reconciliation time | Hours to complete monthly bank reconciliation per camp | 50% reduction from baseline |

## 2.3 Reduced Administrative Burden

**Objective:** Eliminate redundant manual data entry, formula maintenance, and status-check communications.

| Key Result | Metric | Target |
|---|---|---|
| KR1: Duplicate data entry | Number of fields requiring entry in multiple systems | Zero (single entry, relational linking) |
| KR2: Manual status requests | Volume of "what's the status of X?" emails/messages per week | 80% reduction |
| KR3: Spreadsheet maintenance time | Hours per week spent fixing formulas, reconciling sheets | 90% reduction |

## 2.4 Improved Incident Tracking and Escalation Response

**Objective:** Incidents are captured, classified, assigned, and resolved through a defined workflow with full audit trail.

| Key Result | Metric | Target |
|---|---|---|
| KR1: Incident capture completeness | % of incidents captured through formal intake | 100% |
| KR2: Escalation response time | Time from severity-classified intake to assignment | < 1 hour (Severity 1), < 4 hours (Severity 2) |
| KR3: Audit trail completeness | % of incidents with full status history | 100% |

## 2.5 Standardized Training Compliance Tracking

**Objective:** All training requirements (YPT, CPR, Active Shooter, Safeguard from Abuse, etc.) are tracked per person with expiration alerts.

| Key Result | Metric | Target |
|---|---|---|
| KR1: Training tracking coverage | % of required trainings with digital tracking | 100% |
| KR2: Expiration alert lead time | Days before expiration that alerts fire | 30, 14, and 7 days |
| KR3: Pre-camp compliance readiness | % of staff fully compliant 7 days before camp start | > 95% |

## 2.6 Centralized Document Repository

**Objective:** All operational documents (policies, contracts, COIs, invoices, waivers) are linked to their parent records and accessible with appropriate permissions.

| Key Result | Metric | Target |
|---|---|---|
| KR1: Document coverage | % of records with linked supporting documents | > 90% |
| KR2: Document findability | Average time to locate a specific document | < 30 seconds |
| KR3: Version control | % of documents with current version clearly identified | 100% |

---

# 3. Full Module Breakdown with Functional Requirements

---

## Module A: Quality of Life (QOL)

### Core Purpose
Track measurable indicators of participant and staff well-being across all JMC programs. QOL encompasses the holistic experience — from physical comfort and safety to emotional support, meaningful engagement, and sense of community. This module provides leadership with a structured framework to assess, compare, and improve program quality year over year.

### QOL Definition and Measurable Indicators

Quality of Life within JMC programs is measured across five domains:

| QOL Domain | Indicators Tracked |
|---|---|
| **Physical Well-Being** | Meals quality rating, sleeping arrangements adequacy, facility cleanliness score, temperature/weather preparedness |
| **Safety & Security** | Incident count per camp, staff-to-participant ratio, emergency drill completion, first aid accessibility |
| **Emotional & Social** | Participant satisfaction score (from evaluations), homesickness incidents, conflict resolution cases, mentorship engagement |
| **Program Engagement** | Session attendance rates, activity participation %, facilitator effectiveness ratings, content relevance scores |
| **Operational Quality** | Transportation punctuality, schedule adherence, communication responsiveness, supply availability |

### Required Data Fields
- Camp name, year, session
- QOL domain and sub-indicator
- Measurement method (survey, observation, incident count)
- Score / value (numeric scale 1–5, count, or percentage)
- Data collection date
- Collected by (staff name/role)
- Benchmarks (prior year comparison)
- Notes / qualitative observations

### Workflows and Status Tracking
1. **Pre-Camp Setup** → QOL indicators configured per camp → *Status: Configured*
2. **During Camp** → Data collected daily/per-session → *Status: In Progress*
3. **Post-Camp** → Aggregated and reviewed by camp leadership → *Status: Under Review*
4. **Final** → Approved and published to dashboards → *Status: Complete*

### Dashboard Visualizations
- QOL score radar chart per camp (5 domains)
- Year-over-year QOL trend line per camp
- Cross-camp QOL comparison bar chart
- Red/yellow/green indicator cards for each domain

### Automation Triggers
- Auto-generate QOL data collection forms 14 days before camp start
- Alert camp leads when any domain score drops below threshold (< 3.0)
- Auto-populate comparison data from prior year

### Reporting Outputs
- QOL Summary Report per camp per year
- Cross-camp QOL Benchmarking Report
- Year-over-year QOL Improvement Report

### User Access Levels
| Role | Access |
|---|---|
| JMC Super Admin | Full read/write across all camps |
| JMC Admin | Full read across all camps, write for assigned camps |
| Camp Team | Read/write for own camp only |

### Integration Dependencies
- **Evaluations Module (H)** — Participant and staff survey scores feed into QOL calculations
- **Safety & Security Module (B)** — Incident counts feed physical well-being and safety domains

---

## Module B: Safety & Security

### Core Purpose
Manage all safety infrastructure including site inspections, risk escalation workflows, security staff training, external vendor coordination, and incident reporting. Ensure every camp operates within defined safety protocols with documented evidence.

### Required Data Fields

**Site Inspection Checklist:**
- Camp name, site location
- Inspection date, inspector name
- Checklist category (Fire Safety, Structural, Electrical, Water Safety, ADA Compliance, Grounds)
- Item description, status (Pass / Fail / N/A / Needs Follow-Up)
- Photo/document attachment
- Remediation due date, assigned to, remediation status

**Risk Management:**
- Risk ID, description, category (Health, Weather, Security, Infrastructure, Program)
- Likelihood (1–5), Impact (1–5), Risk Score (calculated)
- Mitigation plan, owner, status
- Escalation trigger conditions

**Onsite Staff Security Training:**
- Staff name, camp, role
- Training module (Emergency Evacuation, Lockdown Procedures, First Response, Communication Protocol)
- Completion date, expiration date, certificate link
- Assessment score (if applicable)

**External Security Vendor Management:**
- Vendor name, company, contract ID
- Camp(s) assigned, service dates
- Contract value, payment status
- Insurance/bonding verification, background check status
- Performance rating, incident log

**Incident Reporting:**
- Incident ID (auto-generated)
- Date, time, location (camp + specific area)
- Reporter name, role
- Incident type (Injury, Behavioral, Weather, Security Breach, Medical, Near-Miss)
- Severity (1-Critical, 2-High, 3-Medium, 4-Low)
- Description, persons involved, witnesses
- Immediate action taken
- Follow-up required (Y/N), follow-up actions, follow-up status
- Resolution summary, resolution date
- Attachments (photos, forms, statements)

### Workflows and Status Tracking

**Incident Reporting Flow:**
1. **Intake** — Submitted via Google Form or direct platform entry → *Status: New*
2. **Triage** — Severity classified, category assigned → *Status: Classified*
3. **Assignment** — Assigned to responsible party → *Status: Assigned*
4. **Investigation** — Details gathered, witnesses interviewed → *Status: Under Investigation*
5. **Resolution** — Actions taken, resolution documented → *Status: Resolved*
6. **Closed** — Final review and audit trail sealed → *Status: Closed*

**Risk Escalation:**
- Risk Score ≥ 15 → Auto-notify Camp Director + JMC Admin
- Risk Score ≥ 20 → Auto-notify JMC Super Admin + trigger emergency protocol flag
- Unresolved risks > 48 hours → Auto-escalate one level

### Dashboard Visualizations
- Site inspection completion heatmap (camp × category)
- Open incidents by severity (donut chart)
- Incident trend line (monthly, by type)
- Security vendor compliance scoreboard
- Staff training completion matrix

### Automation Triggers
- New Google Form incident submission → auto-create incident record
- Severity 1 incident → immediate push notification to Super Admin
- Site inspection item marked "Fail" → auto-create remediation task with 72-hour deadline
- Training expiration 30 days away → auto-email reminder to staff and camp lead
- Security vendor contract expiration 60 days away → auto-alert operations

### Reporting Outputs
- Camp Safety Readiness Report (pre-camp)
- Incident Summary Report (per camp, per period)
- Risk Register with mitigation status
- Security Vendor Performance Report
- Training Compliance Report (by camp, by role)

### User Access Levels
| Role | Access |
|---|---|
| JMC Super Admin | Full read/write; access to all severity levels and audit trails |
| JMC Admin | Full read; write for assigned camps; view all severity levels |
| Camp Team | Read/write for own camp; submit incidents; cannot modify closed records |

### Integration Dependencies
- **Google Forms** — Incident intake ingestion
- **Compliance Module (E)** — Training records shared
- **Sites Module (F)** — Site contact and contract information linked
- **Escalation Tracking Module (T)** — Cross-references escalation workflow

---

## Module C: Finance

### Core Purpose
Provide comprehensive financial management including annual budgeting, bank reconciliation, expense tracking, vendor payments, volunteer reimbursements, and revenue monitoring per camp. Establish a vendor management database with compliance tracking.

### Required Data Fields

**Annual Budget Tracking:**
- Camp name, fiscal year
- Budget category (Facilities, Transportation, Staff, Food, Supplies, Insurance, Marketing, Miscellaneous)
- Budgeted amount, actual amount, variance, % utilized
- Line item description, GL code
- Approval status, approved by, approval date

**Bank Reconciliation Checklist:**
- Camp name, month/period
- Bank statement balance, book balance, adjusted balance
- Outstanding checks (list with amounts)
- Deposits in transit
- Reconciliation status (Not Started / In Progress / Reconciled / Discrepancy Found)
- Reconciled by, reconciliation date
- Supporting document links

**Expense Disbursement:**
- Expense ID, date, camp, category
- Payee, description, amount
- Payment method (Check, ACH, Wire, Credit Card)
- Check/reference number, payment date
- Approval chain (Requester → Camp Lead → Finance → Admin)
- Receipt/invoice attachment
- Status (Pending Approval / Approved / Paid / Rejected)

**Volunteer Reimbursements:**
- Volunteer name, camp, reimbursement type (Travel, Supplies, Food, Other)
- Amount requested, amount approved
- Receipt attachments, approval chain
- Payment method, payment date, status

**Revenue Status:**
- Participant name (linked to People module), camp
- Total fees, amount paid, amount outstanding, payment plan status
- Payment dates and amounts (ledger)
- Subsidy applied (linked to Subsidy module)
- Status (Paid in Full / Partial / Unpaid / Subsidy Pending / Waived)

**Vendor Management Database:**
- Vendor ID, company name, DBA
- Primary contact name, email, phone
- Service provided (description and category)
- W9 status (Not Requested / Requested / Received / Verified)
- W9 received date, document link
- 1099 status (Not Applicable / Pending / Issued)
- 1099 issued date, amount reported
- Vendor status (Active / Inactive / Blacklisted)
- Contract links, payment history summary
- Notes

### Workflows and Status Tracking

**Expense Approval Flow:**
1. **Submission** → Requester enters expense → *Status: Submitted*
2. **Camp Lead Review** → Approved or returned with notes → *Status: Camp Approved / Returned*
3. **Finance Review** → Budget check, documentation verified → *Status: Finance Approved / Held*
4. **Payment Processing** → Payment issued → *Status: Paid*

**Vendor Onboarding Flow:**
1. **Request** → New vendor requested → *Status: Requested*
2. **W9 Collection** → W9 form requested and received → *Status: W9 Received*
3. **Verification** → W9 verified, vendor approved → *Status: Active*
4. **Year-End** → 1099 generated if applicable → *Status: 1099 Issued*

### Dashboard Visualizations
- **Budget vs. Actual** — Stacked bar chart per camp per category; overall rollup view
- **Outstanding Payments** — Table view with aging buckets (0–30, 31–60, 61–90, 90+ days)
- **Vendor Compliance** — Status grid (W9 ✓/✗, 1099 ✓/✗, Contract Current ✓/✗) with % complete
- **Revenue Collection** — Per-camp donut chart (Paid / Partial / Unpaid / Subsidy Pending)
- **Expense Trend** — Monthly spend trend line by category
- **Bank Reconciliation Status** — Monthly status indicators per camp (Green = Reconciled, Yellow = In Progress, Red = Not Started)

### Automation Triggers
- Expense over $500 → auto-route to JMC Admin for additional approval
- Vendor W9 not received 30 days after first payment → alert Finance
- Revenue payment overdue > 30 days → auto-reminder to participant contact
- Bank reconciliation not completed by 15th of following month → alert Finance and Admin
- 1099 threshold approaching → alert Finance to verify vendor totals

### Reporting Outputs
- Annual Budget Report per Camp
- Monthly Financial Summary (all camps)
- Vendor 1099 Report (year-end)
- Outstanding Accounts Receivable Report
- Expense Audit Report (by category, by approver)
- Bank Reconciliation Summary (monthly)

### User Access Levels
| Role | Access |
|---|---|
| JMC Super Admin | Full read/write; all financial data; vendor SSN/TIN visible |
| JMC Admin | Full read; write for assigned camps; vendor SSN/TIN restricted |
| Camp Team | Submit expenses and reimbursements for own camp; view own camp budget summary; no vendor financial details |

### Integration Dependencies
- **People Module (D)** — Participant records linked for revenue tracking
- **Subsidy Module (K)** — Subsidy amounts linked to revenue records
- **Vendor Management** — Shared vendor database with Sites (F), Transportation (J), Swag (Q)

---

## Module D: People Management

### Core Purpose
Centralize all person-related records — participants, NPTs (non-paid team), staff, and alumni — with integrated application tracking, document management, and directory features.

### D.1 Participant Applications

**Required Data Fields:**
- iUSA Application ID, participant name, date of birth, gender
- Camp applied for, session/year
- Application status (Submitted / Under Review / Accepted / Waitlisted / Declined / Withdrawn)
- Waiver status (Not Sent / Sent / Signed / Expired)
- Health form status (Not Submitted / Submitted / Reviewed / Cleared / Flagged)
- Emergency contacts (name, relationship, phone, email)
- Dietary restrictions, allergies, medications
- Special needs / accommodations
- Payment status (linked to Finance Module)
- Subsidy status (linked to Subsidy Module)
- Parent/guardian contact information

**Workflows:**
1. Application submitted (via iUSA) → *Status: Submitted*
2. Application reviewed → *Status: Under Review*
3. Decision made → *Status: Accepted / Waitlisted / Declined*
4. Waivers and health forms collected → *Status: Documents Pending → Documents Complete*
5. Payment confirmed → *Status: Enrolled*
6. Pre-camp readiness check → *Status: Ready*

**Integration Dependencies:**
- **iUSA** — Primary application intake; bidirectional sync for status updates
- **Finance Module (C)** — Payment and revenue tracking
- **Subsidy Module (K)** — Subsidy application and approval status
- **Healthcare Module (L)** — Health form review and clearance

### D.2 NPT (Non-Paid Team) Applications

**Required Data Fields:**
- Applicant name, email, phone, city/state
- Camp applying for, role/position
- Application status pipeline: Launch → Review → Shortlist → Approval → Directory
- Interview notes, interviewer name, interview date
- Reference check status
- Onboarding checklist completion %
- Compliance status (linked to Compliance Module)
- Directory entry (name, role, camp, contact info, photo)

**Workflows:**
1. **Launch** → Application opens → recruitment marketing begins
2. **Review** → Applications screened → *Status: Under Review*
3. **Shortlist** → Top candidates identified → *Status: Shortlisted*
4. **Approval** → Final selection and offer → *Status: Approved*
5. **Directory** → Onboarded and added to team directory → *Status: Active*

### D.3 Staff Applications

**Required Data Fields:**
- Applicant name, email, phone, address
- Position applied for, camp, department
- Application date, source (referral, website, job board)
- Interview tracking:
  - Interview stage (Phone Screen / Round 1 / Round 2 / Final)
  - Interview date, interviewer, notes, rating (1–5)
  - Decision (Advance / Hold / Reject)
- Offer status (Not Offered / Offered / Accepted / Declined)
- Waiver status, health form status
- Background check status (linked to Compliance Module)
- Employment documents (I-9, direct deposit, emergency contact)

**Workflows:**
1. Application received → *Status: New*
2. Phone screen → *Status: Screening*
3. Interview rounds → *Status: Interviewing*
4. Final decision → *Status: Offered / Rejected*
5. Onboarding → *Status: Onboarding*
6. Active → *Status: Active Staff*

### D.4 Alumni Database

**Required Data Fields:**
- Alumni name, email, phone, mailing address
- Camp(s) attended (multi-select)
- Year(s) attended (multi-select)
- Role during participation (Participant / NPT / Staff / Faculty)
- Engagement level (Active / Occasional / Inactive)
- Engagement history (events attended, donations, volunteer activities)
- Last contact date, preferred contact method
- Notes / relationship summary
- Opt-in/opt-out status for communications

**Dashboard Visualizations (People Module):**
- Application pipeline funnel (by camp, by role type)
- Enrollment progress tracker (applications → enrolled, per camp)
- Staff hiring pipeline (stages × count)
- Alumni engagement summary (active vs. inactive, by camp)
- Document completion matrix (waivers, health forms, compliance — by person)

**Automation Triggers:**
- Application received → auto-acknowledge email
- Waiver not signed 14 days after acceptance → auto-reminder
- Health form not submitted 21 days before camp → escalation to camp lead
- Staff interview scheduled → auto-calendar invite
- Alumni last contact > 12 months → flag for re-engagement

### User Access Levels
| Role | Access |
|---|---|
| JMC Super Admin | Full read/write; all camps; all personal data |
| JMC Admin | Full read; write for assigned camps |
| Camp Team | Read/write for own camp participants, NPTs, staff; read-only alumni for own camp |

---

## Module E: Compliance

### Core Purpose
Track all compliance requirements across camps, roles, and states, including certifications, training completions, background checks, and policy acknowledgments. Provide audit-ready dashboards and automated expiration alerts.

### Required Data Fields

**Per-Person Compliance Record:**
- Person name, role (Staff / NPT / Volunteer / Faculty / HCP), camp(s)
- YPT (Youth Protection Training): completion date, expiration date, certificate link, status
- Background Check: provider, submission date, clearance date, status, document link
- Fingerprinting (Florida only): submission date, clearance date, status
- CPR Certification: provider, completion date, expiration date, certificate link
- Mandated Reporter Training (Georgia only): completion date, certificate link
- Safeguard from Abuse: completion date, certificate link
- Active Shooter Training: completion date, certificate link
- Driving Waiver: signed date, document link
- Policy Acknowledgment: policy name, signed date, document link

**Policy Repository:**
- Policy name, version, effective date
- Category (Safety, HR, Financial, Operational, Legal)
- Document link, approval status
- Required acknowledgment roles
- Acknowledgment tracking (who signed, when)

**Waiver Compliance:**
- Waiver type, person name, camp
- Sent date, signed date, expiration date
- Status (Not Sent / Sent / Signed / Expired / Waived)

### Compliance Requirements by State

| Requirement | All States | Georgia Only | Florida Only |
|---|---|---|---|
| YPT | ✓ | ✓ | ✓ |
| Background Check | ✓ | ✓ | ✓ |
| CPR | ✓ | ✓ | ✓ |
| Active Shooter | ✓ | ✓ | ✓ |
| Safeguard from Abuse | ✓ | ✓ | ✓ |
| Mandated Reporter | | ✓ | |
| Fingerprinting | | | ✓ |

### Workflows and Status Tracking
1. **Requirement Assigned** → Person added to camp with role → applicable compliance items auto-generated based on camp state and role → *Status: Required*
2. **In Progress** → Training started or document submitted → *Status: In Progress*
3. **Completed** → Certificate/clearance received and verified → *Status: Compliant*
4. **Expiring** → Within 30 days of expiration → *Status: Expiring Soon*
5. **Expired** → Past expiration date → *Status: Non-Compliant*

### Dashboard Visualizations

**Compliance Heatmap by Camp:**
- Rows: Camps | Columns: Compliance requirements | Cells: % complete (color-coded)

**Compliance by Staff Role:**
- Filter by role type to see compliance completion rates

**Compliance by State:**
- Grouped view showing only applicable requirements per state

**Individual Compliance Card:**
- Per-person view of all requirements with status badges

### Automation Triggers
- Person assigned to camp → auto-generate applicable compliance requirements
- Training completion uploaded → auto-update status + calculate expiration
- 30/14/7 days before expiration → auto-email reminder to person + camp lead
- Expiration reached → auto-set Non-Compliant + alert JMC Admin
- Pre-camp readiness report auto-generated 14 days before camp start
- Non-compliant individual assigned to active camp role → block/flag in system

### Reporting Outputs
- Camp Compliance Readiness Report
- Individual Compliance Transcript
- Compliance Gap Report (all camps, all requirements)
- State-Specific Compliance Report (Georgia, Florida)
- Policy Acknowledgment Status Report
- Expiring Certifications Report (30/60/90 day lookahead)

### User Access Levels
| Role | Access |
|---|---|
| JMC Super Admin | Full read/write; all camps; can modify compliance requirements |
| JMC Admin | Full read; can verify and approve compliance items |
| Camp Team | View compliance status for own camp; can upload own certificates; cannot modify others' records |

### Integration Dependencies
- **People Module (D)** — Person records and camp assignments
- **Safety & Security Module (B)** — Training records shared
- **Healthcare Module (L)** — HCP-specific compliance items

---

## Module F: Sites

### Core Purpose
Manage all camp site relationships including contracts, certificates of insurance (COI), and contact/relationship management for each facility used across JMC programs.

### Required Data Fields
- Site name, address, city, state, zip
- Site type (Residential, Day Camp, Conference Center, Outdoor, School)
- Camp(s) using site, session dates
- Primary contact (name, title, email, phone)
- Secondary contact
- Relationship owner (JMC staff member)
- Relationship status (Prospective / Active / On Hold / Former)
- Contract status (Draft / Sent / Under Negotiation / Signed / Expired)
- Contract start date, end date, auto-renewal clause (Y/N)
- Contract value, payment terms
- Contract document link
- COI status (Not Requested / Requested / Received / Verified / Expired)
- COI expiration date, document link
- Site capacity, amenities, accessibility features
- Notes, historical usage log

### Workflows and Status Tracking
1. **Prospect** → Site identified for potential use → *Status: Prospective*
2. **Negotiation** → Contract in discussion → *Status: Negotiating*
3. **Contracted** → Agreement signed → *Status: Active*
4. **COI Verification** → Insurance certificate obtained → *Status: COI Verified*
5. **Renewal** → Contract approaching expiration → *Status: Renewal Pending*

### Dashboard Visualizations
- Site map (geographic view of all active sites)
- Contract status board (by camp, by status)
- COI expiration timeline
- Site utilization summary (camps per site per year)

### Automation Triggers
- Contract expiration 90/60/30 days → alert relationship owner
- COI expiration 60/30 days → auto-email site contact requesting renewal
- New camp session created → prompt for site assignment and contract verification

### Reporting Outputs
- Active Sites Summary
- Contract Renewal Calendar
- COI Status Report
- Site Cost Analysis (per camp, per year)

### User Access Levels
| Role | Access |
|---|---|
| JMC Super Admin / Admin | Full read/write |
| Camp Team | Read for own camp's sites; can update contact notes |

### Integration Dependencies
- **Insurance Module (I)** — COI tracking shared
- **Finance Module (C)** — Contract values and payments
- **Safety & Security Module (B)** — Site inspection records linked

---

## Module G: Marketing

### Core Purpose
Manage marketing campaign planning, execution tracking, and launch coordination across all JMC programs.

### Required Data Fields
- Campaign name, camp(s), target audience
- Campaign type (Email, Social Media, Print, Digital Ad, Event, Website)
- Launch date, end date
- Status (Planning / Content Creation / Review / Approved / Live / Completed)
- Checklist items (content written, design complete, approved by leadership, links tested, scheduled, launched)
- Checklist item status, assigned to, due date
- Budget allocated, actual spend
- Performance metrics (if applicable): reach, clicks, conversions, registrations
- Notes / creative assets links

### Workflows and Status Tracking
1. **Planning** → Campaign defined and scheduled → *Status: Planning*
2. **Content Creation** → Assets being developed → *Status: In Production*
3. **Review** → Submitted for approval → *Status: Under Review*
4. **Approved** → Ready for launch → *Status: Approved*
5. **Live** → Campaign active → *Status: Live*
6. **Completed** → Campaign ended, results logged → *Status: Completed*

### Dashboard Visualizations
- Launch calendar (Gantt/timeline view of all campaigns)
- Campaign status board (Kanban-style)
- Marketing budget vs. actual per camp
- Campaign performance summary (if metrics tracked)

### Automation Triggers
- Campaign launch date 7 days away + checklist incomplete → alert assigned team
- Campaign approved → auto-schedule launch notification
- Campaign completed → auto-prompt for performance data entry

### Reporting Outputs
- Marketing Calendar Report
- Campaign Performance Report
- Marketing Spend Report per Camp

### User Access Levels
| Role | Access |
|---|---|
| JMC Super Admin / Admin | Full read/write |
| Camp Team | Read/write for own camp campaigns |

---

## Module H: Evaluations

### Core Purpose
Manage all survey and evaluation processes across the participant lifecycle — pre-camp, post-camp, and 100-day follow-up — for participants, staff, facilitators, and parents. Aggregate results into dashboards by camp.

### Required Data Fields
- Evaluation type: Participant Survey, Staff Survey, Facilitator Survey, Parent Survey
- Timing: Pre-Camp, Post-Camp, 100-Day Follow-Up
- Camp name, session, year
- Distribution date, due date, close date
- Response count, total distributed, response rate
- Question categories (Experience, Safety, Content, Facilities, Leadership, Recommendation)
- Average scores per category (1–5 scale)
- Net Promoter Score (NPS) if applicable
- Open-ended response summaries
- Status (Draft / Distributed / Collecting / Closed / Analyzed)

### Workflows and Status Tracking
1. **Setup** → Survey configured and scheduled → *Status: Draft*
2. **Distribution** → Sent to recipients → *Status: Distributed*
3. **Collection** → Responses coming in → *Status: Collecting*
4. **Closed** → Deadline passed → *Status: Closed*
5. **Analysis** → Results reviewed and summarized → *Status: Analyzed*

### Dashboard Visualizations
- Response rate gauge (per survey, per camp)
- Average scores by category (radar chart per camp)
- Cross-camp comparison (bar chart)
- Year-over-year trend (line chart)
- NPS score display per camp
- 100-day follow-up participation rate

### Automation Triggers
- Camp end date → auto-trigger post-camp survey distribution (3 days after)
- 100 days after camp → auto-trigger follow-up survey
- Response rate < 50% at 7 days before close → reminder email to non-respondents
- Survey closed → auto-generate summary report

### Reporting Outputs
- Post-Camp Evaluation Summary (per camp)
- Cross-Camp Evaluation Comparison Report
- Year-over-Year Evaluation Trends
- 100-Day Impact Report
- Parent Satisfaction Summary

### User Access Levels
| Role | Access |
|---|---|
| JMC Super Admin / Admin | Full read/write; all camps |
| Camp Team | Read results for own camp; manage survey distribution for own camp |

### Integration Dependencies
- **QOL Module (A)** — Survey scores feed QOL indicators
- **People Module (D)** — Participant and staff lists for survey distribution

---

## Module I: Insurance

### Core Purpose
Track all insurance policies, certificates of insurance (COI) per camp site, high-risk activity coverage, and policy registry for the organization.

### Required Data Fields

**Policy Registry:**
- Year, policy name/carrier (e.g., "Chubb"), policy number
- Account number, policy period (start date – end date)
- Policy type (General Liability, Property, Workers Comp, D&O, Umbrella, Auto, Cyber)
- Policy amount / coverage limit
- Premium amount, billing date, paid date
- Payment confirmation link, invoice link
- Renewal status (Current / Renewal Pending / Lapsed)
- Broker contact name, email, phone

**COI Tracking Per Site:**
- Site name (linked to Sites Module), camp(s)
- COI holder name, policy number
- Coverage dates, expiration date
- Additional insured requirements met (Y/N)
- COI document link
- Status (Requested / Received / Verified / Expired)

**High-Risk Activity Tracking:**
- Activity name (e.g., swimming, ropes course, canoeing)
- Camp, site, date(s)
- Covered by policy (Y/N), policy reference
- Additional rider required (Y/N), rider status
- Waivers collected (linked to People/Compliance modules)
- Safety plan document link

### Dashboard Visualizations
- Policy timeline (Gantt view of all policies with renewal dates)
- COI status grid (site × camp, color-coded)
- Coverage gap alerts (any camp/activity without verified coverage)
- Premium payment status (paid vs. outstanding)
- High-risk activity coverage matrix

### Automation Triggers
- Policy expiration 90/60/30 days → alert JMC Admin + broker
- COI expiration 60/30 days → auto-request renewal from site contact
- High-risk activity added to camp without coverage → block or flag
- Payment due date approaching → alert Finance

### Reporting Outputs
- Annual Insurance Summary
- COI Compliance Report (by site, by camp)
- High-Risk Activity Coverage Audit
- Premium Payment Schedule

### User Access Levels
| Role | Access |
|---|---|
| JMC Super Admin | Full read/write |
| JMC Admin | Full read; write for assigned areas |
| Camp Team | Read COI status for own camp's sites |

### Integration Dependencies
- **Sites Module (F)** — Site records linked for COI tracking
- **Finance Module (C)** — Premium payments and budget allocation
- **Safety & Security Module (B)** — High-risk activity coordination

---

## Module J: Transportation

### Core Purpose
Manage all transportation logistics including bus contracts, flight bookings, car rentals, and volunteer driver waiver tracking across all camps.

### Required Data Fields

**Bus Contracts:**
- Bus company name, contract ID, camp(s)
- Route (pickup location → drop-off location)
- Service dates, times
- Number of buses, capacity per bus
- Contract value, payment status
- Insurance verification status
- Driver background check status
- Contract document link

**Flights (Corporate Codes):**
- Airline, corporate code / account number
- Traveler name, camp, role
- Origin, destination, departure date, return date
- Booking reference, ticket cost
- Payment method, reimbursement status (if applicable)
- Status (Booked / Confirmed / Changed / Cancelled)

**Car Rentals (Corporate Codes):**
- Rental company, corporate code / account number
- Renter name, camp, role
- Pickup location, return location, rental dates
- Vehicle class, daily rate, estimated total
- Confirmation number
- Payment method, reimbursement status
- Status (Reserved / Active / Returned / Cancelled)

**Volunteer Car Driver Waivers:**
- Driver name, camp
- Vehicle info (make, model, year, license plate)
- Insurance verification (policy number, carrier, coverage limits)
- Driver's license verification (state, number, expiration)
- Driving waiver signed date, document link
- Background check status
- Approved to drive (Y/N), approved by, date
- Status (Pending / Approved / Denied / Expired)

### Dashboard Visualizations
- Transportation overview by camp (bus, flight, rental counts)
- Upcoming departures timeline
- Waiver completion status (% approved drivers)
- Transportation spend by camp and type
- Contract status board

### Automation Triggers
- Bus contract not signed 30 days before camp → escalation alert
- Volunteer driver waiver not complete 14 days before camp → alert camp lead
- Driver's license expiring within 60 days → flag and alert
- Flight/rental booking confirmation not received 7 days after request → follow-up alert

### Reporting Outputs
- Transportation Cost Summary per Camp
- Volunteer Driver Compliance Report
- Bus Contract Status Report
- Travel Itinerary Summary

### User Access Levels
| Role | Access |
|---|---|
| JMC Super Admin / Admin | Full read/write |
| Camp Team | Read/write for own camp; submit travel requests |

### Integration Dependencies
- **Compliance Module (E)** — Driving waiver and background check status
- **Finance Module (C)** — Transportation expenses and contract payments
- **People Module (D)** — Traveler records linked

---

## Module K: Subsidy Tracking

### Core Purpose
Track all subsidy applications, approvals, rejections, and disbursements across camps, with breakdowns for camp fees vs. travel costs.

### Required Data Fields

**Master Subsidy Tracker:**
- Applicant name (linked to People Module), camp, session
- Application date, application ID
- Subsidy type: Camp Fees / Travel / Both
- Amount requested (camp fees), amount requested (travel)
- Amount approved (camp fees), amount approved (travel)
- Approval status: Pending / Approved / Partially Approved / Rejected / Withdrawn
- Approved by, approval date
- Rejection reason (if applicable)
- Disbursement status: Not Disbursed / Disbursed / Partial
- Disbursement date, method, reference number
- Notes

**Travel Tracker:**
- Applicant name, camp
- Travel type (Flight, Bus, Car, Other)
- Origin, destination
- Estimated cost, approved amount, actual cost
- Receipt link, reimbursement status

### Dashboard Visualizations
- Subsidy allocation overview (total requested vs. approved vs. disbursed)
- Approval rate by camp (bar chart)
- Camp fees vs. travel subsidy split (stacked bar)
- Pending applications count with aging
- Budget utilization for subsidy fund

### Automation Triggers
- New application received → auto-acknowledge + assign reviewer
- Application pending > 14 days → escalation to JMC Admin
- Subsidy approved → auto-update participant's financial record in Finance module
- Subsidy fund utilization > 80% → alert Finance team

### Reporting Outputs
- Subsidy Allocation Report by Camp
- Subsidy Budget Utilization Report
- Applicant Subsidy Ledger
- Camp Fees vs. Travel Subsidy Analysis

### User Access Levels
| Role | Access |
|---|---|
| JMC Super Admin | Full read/write; approve/reject authority |
| JMC Admin | Read; can recommend; limited write |
| Camp Team | View subsidy status for own camp's participants; submit applications |

### Integration Dependencies
- **People Module (D)** — Applicant records
- **Finance Module (C)** — Revenue adjustments and disbursement tracking
- **Transportation Module (J)** — Travel cost validation

---

## Module L: Healthcare Management

### Core Purpose
Manage all healthcare-related operations including Healthcare Professional (HCP) tracking, health form review, pre-camp training, onboarding, inventory, and expense management.

### Required Data Fields

**HCP Tracking:**
- HCP name, credentials (MD, RN, NP, PA, EMT, etc.)
- License number, state of licensure, expiration date
- Camp(s) assigned, session dates
- Availability status (Confirmed / Tentative / Unavailable)
- Contact info (email, phone, emergency contact)
- Travel arrangements (linked to Transportation Module)

**Health Form Review:**
- Participant/staff name (linked to People Module)
- Health form submission date, review date
- Reviewer (HCP name)
- Status (Not Submitted / Submitted / Under Review / Cleared / Flagged / Requires Follow-Up)
- Flag reason, follow-up actions, follow-up status
- Allergies, medications, conditions (summary fields)
- Accommodation requirements

**Pre-Camp Healthcare Training:**
- Training module name, facilitator
- Training date, delivery method (In-Person, Virtual, Self-Paced)
- Attendees list, completion status per attendee
- Materials link, assessment score (if applicable)

**HCP Onboarding:**
- Onboarding checklist items (license verification, orientation, site walkthrough, medical kit check, communication protocol review)
- Item status, completion date
- Onboarding overall status (Not Started / In Progress / Complete)

**Healthcare Inventory:**
- Item name, category (First Aid, Medication, Equipment, PPE)
- Camp, location (storage area)
- Quantity on hand, minimum required, reorder level
- Expiration date (if applicable)
- Last audit date, audited by

**HCP Travel & Expenses:**
- HCP name, camp
- Travel arrangements (linked to Transportation Module)
- Expense type, amount, receipt link
- Reimbursement status, payment date

**HCP Expectations / Terms of Reference (TOR):**
- Document version, effective date
- Acknowledged by (HCP name), acknowledgment date
- Document link

### Dashboard Visualizations
- HCP assignment matrix (camp × HCP, with status)
- Health form review progress (% cleared per camp)
- Inventory status alerts (items below minimum)
- HCP onboarding completion tracker
- Healthcare readiness scorecard per camp

### Automation Triggers
- Health form submitted → auto-notify assigned HCP for review
- Health form flagged → auto-alert camp lead + HCP
- HCP license expiring within 90 days → alert
- Inventory item below minimum → auto-reorder alert
- Pre-camp training incomplete 14 days before camp → escalation

### Reporting Outputs
- Healthcare Readiness Report per Camp
- Health Form Review Summary
- HCP Assignment and Availability Report
- Healthcare Inventory Audit Report
- HCP Expense Summary

### User Access Levels
| Role | Access |
|---|---|
| JMC Super Admin | Full read/write; access to all health data |
| JMC Admin | Read; manage HCP assignments |
| Camp Team | View health form status for own camp; no access to medical details |
| HCP (special role) | Read/write health forms and medical details for assigned camp |

### Integration Dependencies
- **People Module (D)** — Health form submission linked to participant/staff records
- **Compliance Module (E)** — HCP credentials and training
- **Transportation Module (J)** — HCP travel arrangements
- **Finance Module (C)** — HCP expense reimbursements

---

## Module M: Corporate Accounts

### Core Purpose
Manage organizational corporate accounts including discount codes, subscription services, and storage facility arrangements.

### Required Data Fields

**Discount Code Management:**
- Vendor/service name, code type (Promo, Corporate, Partnership)
- Code value, usage limits, expiration date
- Applicable camps/programs
- Status (Active / Expired / Revoked)
- Usage log (who used, when, for what)

**Subscription Management:**
- Service name, provider, account ID
- Subscription type (Software, SaaS, Media, Communication, Other)
- Monthly/annual cost, billing cycle, next billing date
- Account owner, login credentials location (reference to secure vault — not stored in platform)
- Auto-renewal (Y/N), cancellation deadline
- Status (Active / Cancelled / Pending Renewal)

**Storage Facility Management:**
- Facility name, address, unit number
- Access contacts, access hours
- Lease start, lease end, monthly cost
- Contents inventory summary
- Status (Active / Closed)

### Dashboard Visualizations
- Active subscriptions list with upcoming renewals
- Corporate discount codes (active vs. expiring)
- Storage facility overview with costs
- Total recurring cost summary

### Automation Triggers
- Subscription renewal 30 days away → alert account owner
- Discount code expiring in 14 days → alert admin
- Storage lease renewal 60 days → alert operations

### User Access Levels
| Role | Access |
|---|---|
| JMC Super Admin / Admin | Full read/write |
| Camp Team | Read discount codes applicable to their camp; no subscription/storage access |

---

## Module N: ITREB Educators / Faculty

### Core Purpose
Track ITREB educator and faculty members including onboarding, training compliance, travel/expense management, and scheduling.

### Required Data Fields
- Faculty name, title, credentials, institution/affiliation
- Email, phone, mailing address
- Camp(s) assigned, session(s), role (Lead Educator, Assistant, Guest Speaker)
- Onboarding status (Not Started / In Progress / Complete)
- Onboarding checklist items and completion dates
- Training modules completed, dates, certificates
- Compliance status (linked to Compliance Module)
- Travel arrangements (linked to Transportation Module)
- Expense submissions (linked to Finance Module)
- Teaching schedule (camp, date, time, session, topic)
- Availability calendar
- Performance evaluation notes (from Evaluations Module)
- TOR signed (Y/N), document link

### Dashboard Visualizations
- Faculty assignment board (camp × faculty member)
- Onboarding completion tracker
- Training compliance matrix
- Schedule calendar view
- Expense summary per faculty member

### Automation Triggers
- Faculty assigned to camp → auto-generate onboarding checklist
- Training incomplete 21 days before camp → alert
- Schedule conflict detected → flag and alert

### User Access Levels
| Role | Access |
|---|---|
| JMC Super Admin / Admin | Full read/write |
| Camp Team | View assigned faculty for own camp; view schedule |

### Integration Dependencies
- **Compliance Module (E)**, **Transportation Module (J)**, **Finance Module (C)**, **Evaluations Module (H)**

---

## Module O: Annual Calendar

### Core Purpose
Centralized calendar of all JMC dates including camp sessions, training events, and meetings.

### Required Data Fields
- Event name, type (Camp Session, Training, Meeting, Deadline, Holiday)
- Start date, end date
- Camp(s) associated, location
- Organizer, attendees/audience
- Description, agenda link
- Status (Tentative / Confirmed / Cancelled / Completed)
- Recurrence (if applicable)

### Dashboard Visualizations
- Full-year calendar view (month/quarter/year)
- Timeline view by camp
- Upcoming events list (30-day lookahead)
- Conflict detector (overlapping events for same camp/staff)

### Automation Triggers
- Event 30 days away → reminder to organizer for preparation checklist
- Camp session date confirmed → auto-populate related modules (compliance deadlines, survey schedules, etc.)

### User Access Levels
| Role | Access |
|---|---|
| JMC Super Admin / Admin | Full read/write |
| Camp Team | Read all; write for own camp events |

---

## Module P: AJPF (Donations)

### Core Purpose
Track donation activity related to JMC programs through the Al Jubilee Philanthropic Fund or similar channels.

### Required Data Fields
- Donor name (or Anonymous), contact info
- Donation date, amount, method (Online, Check, Wire, In-Kind)
- Designated camp/program (if restricted)
- Unrestricted/restricted flag
- Receipt issued (Y/N), receipt number
- Acknowledgment sent (Y/N), date
- Tax year
- Notes

### Dashboard Visualizations
- Total donations by period (bar chart)
- Donations by camp/program (pie chart)
- Restricted vs. unrestricted funds
- Donor acknowledgment status

### Automation Triggers
- Donation received → auto-generate acknowledgment letter
- Donation receipt not issued within 48 hours → alert

### User Access Levels
| Role | Access |
|---|---|
| JMC Super Admin | Full read/write |
| JMC Admin | Read; limited write |
| Camp Team | No access (unless specifically granted) |

---

## Module Q: Swag / Vendor Management

### Core Purpose
Track swag inventory, vendor contracts, and distribution across camps.

### Required Data Fields

**Inventory:**
- Item name, SKU/ID, category (Apparel, Accessories, Stationery, Bags, Other)
- Vendor, unit cost, quantity ordered, quantity received, quantity distributed
- Storage location
- Camp(s) designated, distribution method

**Vendor Contracts:**
- Vendor name (linked to Finance Module vendor database)
- Contract ID, contract dates, value
- Items supplied, lead time
- Payment terms, payment status

**Distribution Tracking:**
- Camp, event, date
- Item, quantity distributed
- Distributed by, distribution method
- Remaining inventory after distribution

### Dashboard Visualizations
- Inventory levels by item (with reorder alerts)
- Distribution summary by camp
- Vendor performance (on-time delivery, quality rating)
- Swag budget vs. actual

### User Access Levels
| Role | Access |
|---|---|
| JMC Super Admin / Admin | Full read/write |
| Camp Team | View inventory for own camp; log distributions |

---

## Module R: Trainings & National Meetings

### Core Purpose
Track all training events and national meetings including logistics, costs, and attendance.

### Required Data Fields
- Event name, type (Training / National Meeting / Regional Meeting / Workshop)
- Location (venue, city, state)
- Start date, end date
- Organizer, facilitator(s)
- Number of expected attendees, actual attendees
- Attendee list (names, roles, camps)
- Total cost, cost breakdown (venue, travel, food, materials, AV)
- Budget approved (Y/N), approved amount
- Status (Planning / Confirmed / In Progress / Completed / Cancelled)
- Materials/agenda link, post-event report link

### Dashboard Visualizations
- Training calendar
- Cost per event / cost per attendee
- Attendance tracking (expected vs. actual)
- Year-over-year training investment trend

### User Access Levels
| Role | Access |
|---|---|
| JMC Super Admin / Admin | Full read/write |
| Camp Team | View scheduled trainings; RSVP |

---

## Module S: Content Repository

### Core Purpose
Manage the lifecycle of program content from vision through final publication, including training materials.

### Required Data Fields
- Content title, type (Curriculum, Training Material, Activity Guide, Policy Document, Presentation)
- Camp(s), program area
- Author, reviewer(s), approver
- Current stage: Vision → Outline → Draft → Review → Final
- Stage history with dates and editors
- Version number, change log
- File link (current version), archive links (prior versions)
- Tags/categories for search
- Status (Active / Archived / Deprecated)

### Workflows and Status Tracking
1. **Vision** → Content concept defined → *Status: Vision*
2. **Outline** → Structure documented → *Status: Outline*
3. **Draft** → Content written → *Status: Draft*
4. **Review** → Submitted for review → *Status: Under Review*
5. **Final** → Approved and published → *Status: Final*

### Dashboard Visualizations
- Content pipeline (Kanban board by stage)
- Content by camp/program
- Review queue (items awaiting review)
- Recently published content

### Automation Triggers
- Content in "Review" stage > 7 days → reminder to reviewer
- Content marked "Final" → auto-notify relevant camp teams
- Deprecated content accessed → alert author/admin

### User Access Levels
| Role | Access |
|---|---|
| JMC Super Admin / Admin | Full read/write; approve content |
| Camp Team | Read final content; submit drafts for own camp |

---

## Module T: Escalation Tracking System

### Core Purpose
Provide a structured, auditable system for capturing, classifying, assigning, and resolving escalated issues across all JMC operations.

### Required Data Fields
- Escalation ID (auto-generated)
- Intake source (Google Form / Direct Entry / Email)
- Submission date, time
- Reporter name, role, camp
- Category (Safety, Behavioral, Medical, Compliance, Financial, Operational, Legal, HR)
- Subject / title
- Detailed description
- Persons involved
- Severity classification:
  - **Severity 1 — Critical:** Immediate threat to safety, legal exposure, or organizational reputation
  - **Severity 2 — High:** Significant operational impact requiring same-day response
  - **Severity 3 — Medium:** Important issue requiring resolution within 48 hours
  - **Severity 4 — Low:** Minor issue for tracking and scheduled resolution
- Assigned to (name, role)
- Assignment date, expected resolution date
- Status: Intake → Classified → Assigned → In Progress → Pending Review → Resolved → Closed
- Resolution summary, resolution date
- Follow-up required (Y/N), follow-up actions, follow-up date
- Attachments (documents, photos, statements)
- Audit trail (every status change logged with user, timestamp, notes)

### Workflows and Status Tracking
1. **Intake** → Received via Google Form or direct entry → *Status: New*
2. **Classification** → Severity and category assigned by reviewer → *Status: Classified*
3. **Assignment** → Routed to appropriate handler → *Status: Assigned*
4. **Investigation/Action** → Handler works on resolution → *Status: In Progress*
5. **Pending Review** → Resolution proposed, awaiting confirmation → *Status: Pending Review*
6. **Resolved** → Issue resolved and documented → *Status: Resolved*
7. **Closed** → Final review, audit trail sealed → *Status: Closed*

### Dashboard Visualizations
- Open escalations by severity (bar chart)
- Escalation trend by category (line chart, monthly)
- Average resolution time by severity (gauge chart)
- Escalation heatmap by camp
- Overdue escalations list

### Automation Triggers
- Google Form submission → auto-create escalation record
- Severity 1 → immediate push notification to Super Admin + call alert
- Severity 2 → notification to JMC Admin within 15 minutes
- Escalation unassigned > 2 hours → auto-escalate to next level
- Expected resolution date passed → auto-alert handler + manager
- Resolution entered → auto-prompt for closure review

### Reporting Outputs
- Escalation Summary Report (by period, by camp, by category)
- Resolution Time Analysis
- Open vs. Closed Trend Report
- Severity Distribution Report
- Audit Trail Report (for specific escalation)

### User Access Levels
| Role | Access |
|---|---|
| JMC Super Admin | Full read/write; access all escalations; seal audit trails |
| JMC Admin | Read all; write/manage assigned escalations; cannot modify closed records |
| Camp Team | Submit escalations; view own camp escalations; read-only on resolution details |

### Integration Dependencies
- **Google Forms** — Intake ingestion
- **Safety & Security Module (B)** — Cross-reference incident reports
- **Compliance Module (E)** — Compliance-related escalations linked
- **People Module (D)** — Person records for involved parties

---

## Module U: SSN Tracking

### Status: DESIGN DEFERRED

> **This module will NOT be designed until security and legal requirements are fully clarified.**

**Rationale:** Social Security Numbers are classified as Personally Identifiable Information (PII) under federal and state privacy laws. Storing, transmitting, or displaying SSNs imposes regulatory requirements including:
- Encryption at rest and in transit (AES-256 minimum)
- Access logging and audit trail requirements
- Data minimization and retention policies
- Breach notification obligations (varies by state)
- Potential compliance with SOC 2, PCI DSS, or NIST frameworks

**Next Steps:**
1. Legal review of SSN collection necessity and retention requirements
2. Security architecture review for PII handling
3. Data Protection Impact Assessment (DPIA)
4. Design to proceed only after legal and security sign-off

---

# 4. User Roles & Permissions

## 4.1 Role Definitions

| Role | Description |
|---|---|
| **JMC Super Admin** | Full platform access across all modules, all camps, and all data types. Can configure system settings, manage users, and access sensitive/financial data. Equivalent to system owner. |
| **JMC Admin** | Cross-camp operational access. Can view all camps and write to assigned areas. Cannot modify system configuration or access SSN/TIN data. |
| **Camp Team — Olympia** | Full access to Olympia data across all modules. Read-only for cross-camp dashboards. |
| **Camp Team — Mosaic** | Full access to Mosaic data across all modules. Read-only for cross-camp dashboards. |
| **Camp Team — Al Ummah** | Full access to Al Ummah data across all modules. Read-only for cross-camp dashboards. |
| **Camp Team — Al Ilm** | Full access to Al Ilm data across all modules. Read-only for cross-camp dashboards. |
| **Camp Team — CPOI** | Full access to CPOI data across all modules. Read-only for cross-camp dashboards. |
| **Camp Team — Roots** | Full access to Roots data across all modules. Read-only for cross-camp dashboards. |
| **Camp Team — Embark** | Full access to Embark data across all modules. Read-only for cross-camp dashboards. |
| **Camp Team — Changemakers** | Full access to Changemakers data across all modules. Read-only for cross-camp dashboards. |
| **Camp Team — Khidma** | Full access to Khidma data across all modules. Read-only for cross-camp dashboards. |
| **Camp Team — Retreat** | Full access to Retreat data across all modules. Read-only for cross-camp dashboards. |

## 4.2 Permission Matrix

### Legend
- **F** = Full Access (Read + Write + Delete)
- **RW** = Read + Write (no delete)
- **R** = Read Only
- **RC** = Read Own Camp Only
- **RWC** = Read/Write Own Camp Only
- **—** = No Access
- **S** = Sensitive (requires additional authentication)

| Module | Super Admin | JMC Admin | Camp Team |
|---|---|---|---|
| **A. Quality of Life** | F | RW | RWC |
| **B. Safety & Security** | F | RW | RWC |
| **C. Finance — Budget** | F + S | R | RC (summary only) |
| **C. Finance — Expenses** | F | RW | RWC (submit only) |
| **C. Finance — Vendor DB** | F + S | R (no SSN/TIN) | — |
| **C. Finance — Revenue** | F + S | R | RC (own camp totals) |
| **D. People — Participants** | F | RW | RWC |
| **D. People — NPT** | F | RW | RWC |
| **D. People — Staff** | F | RW | RWC |
| **D. People — Alumni** | F | RW | RC |
| **E. Compliance** | F | RW | RWC (upload own certs) |
| **F. Sites** | F | RW | RC |
| **G. Marketing** | F | RW | RWC |
| **H. Evaluations** | F | RW | RWC (results only) |
| **I. Insurance** | F | R | RC (COI status only) |
| **J. Transportation** | F | RW | RWC |
| **K. Subsidy** | F + S | R | RC |
| **L. Healthcare** | F + S | R | RC (status only, no medical details) |
| **M. Corporate Accounts** | F | RW | R (discount codes only) |
| **N. Faculty** | F | RW | RC |
| **O. Calendar** | F | RW | RWC |
| **P. AJPF** | F + S | R | — |
| **Q. Swag** | F | RW | RWC (distribution log) |
| **R. Trainings/Meetings** | F | RW | R |
| **S. Content** | F | RW | RWC (submit drafts) |
| **T. Escalation** | F | RW (assigned) | RWC (submit + view own) |
| **U. SSN Tracking** | Deferred | Deferred | Deferred |

## 4.3 Sensitive Data Access Controls

| Data Type | Who Can Access | Additional Controls |
|---|---|---|
| Vendor SSN/TIN | Super Admin only | Masked display (last 4 only), full view requires MFA step-up |
| Participant health details | Super Admin + HCP role | Encrypted at rest, access logged |
| Financial actuals | Super Admin + Finance Admin | View restricted by module permission |
| Subsidy applicant details | Super Admin + designated reviewer | PII masked in aggregate reports |
| Donation records | Super Admin only | Donor names masked in camp-level views |

## 4.4 Compliance Visibility by Role

| Role | Compliance Visibility |
|---|---|
| Super Admin | All camps, all requirements, all persons — full heatmap |
| JMC Admin | All camps aggregate view; detail view for assigned camps |
| Camp Team | Own camp compliance status; own personal compliance items |

## 4.5 Financial Visibility by Role

| Role | Financial Visibility |
|---|---|
| Super Admin | All camps, all financial modules, vendor details, revenue details |
| JMC Admin | Budget summary across camps; detailed view for assigned camps; no vendor SSN/TIN |
| Camp Team | Own camp budget summary; own expense submissions; no cross-camp financial data |

---

# 5. Technical Architecture Recommendations

## 5.1 Platform Options Assessment

| Platform | Strengths | Weaknesses | Fit for JMC |
|---|---|---|---|
| **Custom Build (React/Next.js + PostgreSQL)** | Full control, unlimited customization, no per-seat licensing, optimal for complex relational data and custom workflows | Higher upfront development cost, requires dev team for maintenance | **Best Long-Term Fit** — Given 20+ modules with complex relational data, role-based access, and integration requirements |
| **Airtable** | Fast to prototype, relational structure, good views, automations | Row limits on lower plans, limited RBAC, no true PII security, costly at scale, limited custom dashboards | **Good for prototyping Phase 1** — but will hit limits by Phase 2 |
| **Monday.com** | Great visual boards, automations, dashboards | Weak relational data modeling, limited RBAC granularity, expensive per-seat | **Too limited** for this scope |
| **Notion** | Excellent for content/wiki, databases are flexible | No real RBAC, weak automation, no native reporting dashboards, not suitable for sensitive data | **Not recommended** for operational platform |
| **Salesforce** | Enterprise-grade RBAC, robust reporting, extensive integrations | Very expensive, steep learning curve, over-engineered for this use case, customization is complex | **Overkill** for current team size; consider only if JMC scales to 50+ users |
| **Retool / Appsmith + PostgreSQL** | Rapid internal tool development, connects to any database, good RBAC, custom dashboards | Requires technical setup, per-seat pricing, dependent on platform provider | **Strong contender** — balances speed and customization |

### Recommendation

**Primary: Custom Build using Next.js + PostgreSQL + Prisma ORM**

This provides:
- Full control over data model, UI, and business logic
- Proper RBAC with encrypted sensitive data storage
- Integration flexibility (iUSA API, Google Forms API, Google Drive API)
- No per-seat licensing costs
- Scales to any number of modules and users
- Professional-grade audit logging

**Alternative (Faster Time-to-Market): Retool + PostgreSQL Backend**

If development speed is prioritized over full customization, Retool can build internal dashboards rapidly on top of a PostgreSQL database, with built-in RBAC and audit logging.

## 5.2 Recommended Database Structure

### Core Entity-Relationship Overview

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│    Camps      │────<│  Camp_People  │>────│   People     │
│               │     │  (junction)   │     │              │
│ camp_id (PK)  │     │ camp_id (FK)  │     │ person_id(PK)│
│ name          │     │ person_id(FK) │     │ name         │
│ location      │     │ role          │     │ email        │
│ state         │     │ year          │     │ type (enum)  │
│ type          │     └──────────────┘     │ ...          │
└──────┬───────┘                           └──────┬───────┘
       │                                          │
       │     ┌──────────────┐              ┌──────┴───────┐
       ├────<│   Budgets     │              │  Compliance   │
       │     │ budget_id(PK) │              │  Records      │
       │     │ camp_id (FK)  │              │ record_id(PK) │
       │     │ category      │              │ person_id(FK) │
       │     │ budgeted      │              │ req_type      │
       │     │ actual        │              │ status        │
       │     └──────────────┘              │ expiry_date   │
       │                                    └──────────────┘
       │     ┌──────────────┐
       ├────<│    Sites      │     ┌──────────────┐
       │     │ site_id (PK)  │────<│    COIs       │
       │     │ camp_id (FK)  │     │ coi_id (PK)   │
       │     │ contract_stat │     │ site_id (FK)   │
       │     └──────────────┘     │ status         │
       │                           └──────────────┘
       │     ┌──────────────┐
       ├────<│  Incidents    │     ┌──────────────┐
       │     │ incident_id   │     │  Escalations  │
       │     │ camp_id (FK)  │     │ esc_id (PK)   │
       │     │ severity      │     │ incident_id?  │
       │     │ status        │     │ severity      │
       │     └──────────────┘     │ status        │
       │                           └──────────────┘
       │     ┌──────────────┐
       └────<│   Vendors     │
             │ vendor_id(PK) │
             │ name          │
             │ w9_status     │
             │ status        │
             └──────────────┘
```

### Key Database Principles

1. **Normalized relational schema** — No duplicated data. Camps, People, and Vendors are core entities referenced by all modules via foreign keys.
2. **Temporal data** — All records include `created_at`, `updated_at`, and `created_by`, `updated_by` columns for audit purposes.
3. **Soft deletes** — Records are never hard-deleted; a `deleted_at` timestamp is used for logical deletion with full recoverability.
4. **Enums for status fields** — Consistent status values across modules enforced at the database level.
5. **JSONB for flexible metadata** — Modules with varying field requirements use JSONB columns for extensibility without schema migration.
6. **Row-level security (RLS)** — PostgreSQL RLS policies enforce camp-level data isolation for Camp Team roles.

## 5.3 Automation Approach

| Layer | Technology | Purpose |
|---|---|---|
| **Scheduled Jobs** | Cron / pg_cron / Node.js task scheduler | Daily compliance expiration checks, monthly reconciliation reminders, report generation |
| **Event-Driven** | Database triggers + application event bus | Status change notifications, escalation routing, audit log entries |
| **External Integrations** | API polling + webhooks | Google Forms intake, iUSA sync, email notifications |
| **Notification Delivery** | Email (SendGrid/Postmark) + optional Slack/Teams webhooks | Alert delivery for all automation triggers |

### Automation Priority Queue

| Priority | Automation | Module(s) |
|---|---|---|
| P0 (Critical) | Severity 1 escalation instant notification | T, B |
| P0 | Compliance expiration alerts (30/14/7 day) | E |
| P1 (High) | Google Form → Incident record creation | B, T |
| P1 | Expense approval workflow routing | C |
| P1 | Contract/COI expiration alerts | F, I |
| P2 (Medium) | Survey auto-distribution triggers | H |
| P2 | Budget threshold alerts | C |
| P2 | Subsidy application auto-acknowledgment | K |
| P3 (Standard) | Marketing campaign checklist reminders | G |
| P3 | Alumni re-engagement flags | D |

## 5.4 Integration with iUSA

### Integration Architecture

```
┌─────────────┐         ┌──────────────────┐         ┌─────────────┐
│    iUSA      │ ──API──>│  Integration     │ ──SQL──>│  JMC        │
│   System     │<──API── │  Middleware       │<──SQL── │  Database   │
│              │         │  (Node.js)       │         │ (PostgreSQL)│
└─────────────┘         │                  │         └─────────────┘
                         │  - Data mapping  │
                         │  - Conflict res. │
                         │  - Error handling│
                         │  - Sync logging  │
                         └──────────────────┘
```

**Sync Strategy:**
- **Frequency:** Scheduled sync every 4 hours + on-demand manual sync button
- **Direction:** Bidirectional for participant status; read-only for application data
- **Conflict Resolution:** iUSA is source of truth for application data; JMC platform is source of truth for internal status (compliance, payment)
- **Data Mapped:**
  - Participant name, contact info, application status
  - Waiver submission/completion status
  - Health form submission status
  - Enrollment confirmation

**Fallback:** If iUSA API is unavailable, CSV import/export mechanism available as manual override.

## 5.5 Data Security Standards

| Requirement | Implementation |
|---|---|
| **Encryption at Rest** | AES-256 encryption for database; TDE (Transparent Data Encryption) for PostgreSQL |
| **Encryption in Transit** | TLS 1.3 for all connections (HTTPS, database connections, API calls) |
| **Authentication** | OAuth 2.0 / OpenID Connect; enforce MFA for Super Admin and sensitive module access |
| **Authorization** | Role-Based Access Control (RBAC) with PostgreSQL Row-Level Security |
| **Session Management** | JWT with short expiration (15 min) + refresh tokens; auto-logout after 30 min inactivity |
| **PII Handling** | Sensitive fields (SSN, TIN, health data) encrypted at the application layer with field-level encryption |
| **Password Policy** | Minimum 12 characters, complexity requirements, no reuse of last 10 passwords |
| **Vulnerability Management** | Monthly dependency scanning, quarterly penetration testing |
| **Data Backup** | Daily automated backups, 30-day retention, encrypted backup storage, tested restore procedure quarterly |
| **Data Retention** | 7-year retention for financial records; 5-year for compliance; configurable per module |

## 5.6 Audit Logging

Every data modification is logged in an immutable `audit_log` table:

| Field | Description |
|---|---|
| `log_id` | Auto-incrementing primary key |
| `timestamp` | UTC timestamp of the action |
| `user_id` | User who performed the action |
| `user_role` | Role at time of action |
| `action` | CREATE / UPDATE / DELETE / VIEW (for sensitive data) |
| `module` | Module name (e.g., "Finance", "Compliance") |
| `entity_type` | Table/record type affected |
| `entity_id` | Primary key of affected record |
| `field_changed` | Specific field modified |
| `old_value` | Prior value (encrypted for PII fields) |
| `new_value` | New value (encrypted for PII fields) |
| `ip_address` | Client IP address |
| `session_id` | Session identifier |

**Audit logs are append-only** — no updates or deletions permitted, even by Super Admin.

## 5.7 Scalability Planning

| Dimension | Current Need | 3-Year Target | Design Approach |
|---|---|---|---|
| **Users** | ~30 concurrent | ~100 concurrent | Stateless application servers behind load balancer; horizontal scaling |
| **Camps** | ~12 | ~25+ | Camp as a core entity with no hard-coded references; all queries camp-scoped |
| **Data Volume** | ~10K records | ~100K+ records | Database indexing strategy, query optimization, pagination on all list views |
| **Modules** | 20 initial | 25+ | Modular code architecture; each module is a self-contained feature package |
| **Integrations** | iUSA + Google | Additional CRMs, payment processors | Integration middleware layer with standardized adapter pattern |
| **Reporting** | Standard dashboards | Advanced analytics, ML insights | Data warehouse layer (read replicas) for heavy reporting queries |

---

# 6. Phased Implementation Plan

## Phase 1: Foundation (Months 1–4)
**Modules:** Finance (C), People Management (D), Compliance (E)

### Rationale
These three modules form the operational backbone. Finance provides budget visibility, People centralizes all participant/staff data, and Compliance addresses the most critical risk area. Together they replace the highest-volume spreadsheets and deliver immediate value.

### Milestones

| Month | Milestone | Deliverables |
|---|---|---|
| **Month 1** | Platform foundation | Database schema (core entities: Camps, People, Users), authentication/RBAC system, deployment pipeline, CI/CD setup |
| **Month 1** | Finance — Data model | Budget, expense, vendor, and revenue tables; expense approval workflow |
| **Month 2** | Finance — Dashboards | Budget vs. actual, outstanding payments, vendor compliance dashboards |
| **Month 2** | People — Data model | Participant, NPT, Staff, Alumni tables; application pipeline workflow |
| **Month 2** | People — iUSA integration | Middleware for participant data sync (read-only initial) |
| **Month 3** | Compliance — Data model | Compliance requirements matrix (state-aware); per-person tracking |
| **Month 3** | Compliance — Automation | Expiration alerts, pre-camp readiness calculations |
| **Month 3** | People — Dashboards | Application pipeline, enrollment tracker, document completion matrix |
| **Month 4** | Compliance — Dashboards | Compliance heatmap, camp/state/role views, gap report |
| **Month 4** | Phase 1 UAT & Launch | User acceptance testing with JMC Admin + 2 Camp Teams; training; go-live |

### Dependencies
- iUSA API documentation and credentials (required by Month 2)
- Camp list and compliance requirements matrix finalized (required by Month 1)
- Finance historical data for migration (required by Month 1)

### Risk Mitigation
| Risk | Probability | Impact | Mitigation |
|---|---|---|---|
| iUSA API unavailable or undocumented | Medium | High | Build CSV import as fallback; begin with one-way sync |
| Historical data quality issues | High | Medium | Data cleaning sprint in Month 1; accept 80% coverage initially |
| User adoption resistance | Medium | High | Involve 2 camp leads as design partners from Week 1; iterative feedback |

---

## Phase 2: Operations (Months 5–7)
**Modules:** Safety & Security (B), Sites (F), Insurance (I), Transportation (J)

### Milestones

| Month | Milestone | Deliverables |
|---|---|---|
| **Month 5** | Safety — Incident reporting | Google Form integration, incident workflow, severity classification |
| **Month 5** | Sites — Contract tracking | Site database, contract management, COI tracking |
| **Month 6** | Insurance — Policy registry | Policy tracking, COI per-site, high-risk activity matrix |
| **Month 6** | Transportation — Core | Bus contracts, flight/rental tracking, volunteer driver waivers |
| **Month 7** | Safety — Dashboards | Inspection heatmap, incident trends, training matrix |
| **Month 7** | Phase 2 UAT & Launch | Testing with expanded user base; integration validation |

### Dependencies
- Google Forms incident template finalized (required by Month 5)
- Site and insurance data collected from current spreadsheets (required by Month 5)
- Transportation vendor contracts assembled (required by Month 6)

---

## Phase 3: Programs (Months 8–10)
**Modules:** Healthcare (L), Subsidy (K), Marketing (G), Evaluations (H)

### Milestones

| Month | Milestone | Deliverables |
|---|---|---|
| **Month 8** | Healthcare — HCP management | HCP tracking, health form workflow, onboarding checklist |
| **Month 8** | Subsidy — Tracker | Master subsidy tracker, approval workflow, travel tracker |
| **Month 9** | Marketing — Campaigns | Campaign checklist tracker, launch calendar, status board |
| **Month 9** | Evaluations — Surveys | Survey lifecycle management, distribution automation |
| **Month 10** | Healthcare — Inventory + dashboards | Inventory management, readiness scorecard |
| **Month 10** | Evaluations — Dashboards | Response rates, cross-camp comparison, NPS tracking |
| **Month 10** | Phase 3 UAT & Launch | Testing and launch |

### Dependencies
- HCP data and health form templates (required by Month 8)
- Historical subsidy data (required by Month 8)
- Survey templates and distribution lists (required by Month 9)

---

## Phase 4: Enterprise (Months 11–14)
**Modules:** Corporate Accounts (M), Content Repository (S), Trainings & National Meetings (R), ITREB Faculty (N), Annual Calendar (O), AJPF (P), Swag (Q), Escalation Tracking (T), Advanced Reporting

### Milestones

| Month | Milestone | Deliverables |
|---|---|---|
| **Month 11** | Escalation Tracking | Intake workflow, severity routing, audit trail |
| **Month 11** | Annual Calendar | Centralized calendar with cross-module date integration |
| **Month 11** | QOL Module (A) | QOL indicators, data collection, dashboards |
| **Month 12** | Content Repository | Content lifecycle workflow, version management |
| **Month 12** | Faculty (N) + Trainings (R) | Faculty tracking, training event management |
| **Month 13** | Corporate Accounts + Swag + AJPF | Account management, inventory, donation tracking |
| **Month 14** | Advanced Reporting | Executive dashboard, cross-module analytics, historical trends |
| **Month 14** | Full Platform UAT & Polish | End-to-end testing, performance optimization, documentation |

---

## Implementation Timeline Summary

```
Month:  1    2    3    4    5    6    7    8    9    10   11   12   13   14
        ├────────────────────┤
         PHASE 1: Foundation
         Finance | People | Compliance
                              ├──────────────┤
                               PHASE 2: Operations
                               Safety | Sites | Insurance | Transport
                                                ├──────────────┤
                                                 PHASE 3: Programs
                                                 Healthcare | Subsidy |
                                                 Marketing | Evaluations
                                                                  ├──────────────┤
                                                                   PHASE 4: Enterprise
                                                                   All remaining modules +
                                                                   Advanced Reporting
```

---

# 7. Reporting & Dashboard Visualizations

## 7.1 Executive Summary Dashboard

**Audience:** JMC Super Admin, JMC Admin  
**Purpose:** Single-screen overview of organizational health across all dimensions.

### Components

| Component | Visualization | Data Source |
|---|---|---|
| **Camp Status Overview** | Card grid — one card per camp with overall status indicator (Green/Yellow/Red) | Composite score from Compliance, Finance, People |
| **Enrollment Tracker** | Progress bars — applications → accepted → enrolled, per camp | People Module (D) |
| **Financial Health** | KPI cards — Total Budget, Total Spent, % Utilized, Total Outstanding | Finance Module (C) |
| **Compliance Score** | Gauge chart — organization-wide compliance % | Compliance Module (E) |
| **Open Incidents** | Badge count by severity with trend spark-line | Safety Module (B), Escalation Module (T) |
| **Upcoming Deadlines** | Scrolling list — next 30 days of critical deadlines across all modules | All modules |
| **Camp Readiness** | Checklist matrix — camps × readiness categories (Compliance, Financial, Staffing, Site, Insurance) | Cross-module |

### Layout
```
┌────────────────────────────────────────────────────────────┐
│  JMC OPERATIONS DASHBOARD                    [User] [Date] │
├──────────┬──────────┬──────────┬──────────┬───────────────┤
│  Total   │  Overall │  Open    │  Budget  │  Enrollment   │
│  Camps   │ Compli-  │ Escala-  │  Utiliz- │  Progress     │
│  Active  │  ance %  │  tions   │  ation % │  ████████░ 78%│
│   12     │  87%     │   3      │  62%     │               │
├──────────┴──────────┴──────────┴──────────┴───────────────┤
│                    CAMP STATUS CARDS                        │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐         │
│  │ Olympia │ │ Mosaic  │ │Al Ummah │ │ Al Ilm  │   ...   │
│  │  🟢     │ │  🟡     │ │  🟢     │ │  🟡     │         │
│  └─────────┘ └─────────┘ └─────────┘ └─────────┘         │
├────────────────────────────┬───────────────────────────────┤
│   FINANCIAL OVERVIEW       │   COMPLIANCE HEATMAP          │
│   [Budget vs Actual Chart] │   [Camp × Requirement Grid]   │
│                            │                               │
├────────────────────────────┼───────────────────────────────┤
│   INCIDENT TRENDS          │   UPCOMING DEADLINES          │
│   [Monthly Line Chart]     │   [Scrolling List]            │
│                            │                               │
└────────────────────────────┴───────────────────────────────┘
```

## 7.2 Camp-Level Dashboard

**Audience:** Camp Team, JMC Admin  
**Purpose:** Deep-dive into a single camp's operational status.

### Components
- **Camp Header** — Camp name, location, dates, session status, camp lead
- **Enrollment Summary** — Total participants, accepted, waitlisted, withdrawn; progress bar
- **Staff & NPT Summary** — Total positions, filled, vacancies; hiring pipeline status
- **Compliance Status** — Per-person compliance matrix for this camp
- **Financial Summary** — Budget vs. actual for this camp; outstanding expenses
- **Transportation Status** — Bus contracts, flights, driver waivers for this camp
- **Site & Insurance** — Site contract status, COI status for this camp's site(s)
- **Healthcare Readiness** — HCP assigned, health forms reviewed, inventory status
- **Open Issues** — Active incidents and escalations for this camp
- **Evaluation Results** — Latest survey scores and response rates (post-camp)

## 7.3 Compliance Heatmap

**Audience:** JMC Super Admin, JMC Admin  
**Purpose:** At-a-glance view of compliance gaps across all camps and requirements.

### Structure

**Rows:** Camps (Olympia, Mosaic, Al Ummah, Al Ilm, CPOI, Roots, Embark, Changemakers, Khidma, Retreat)  
**Columns:** Compliance requirements (YPT, Background Check, CPR, Active Shooter, Safeguard from Abuse, Mandated Reporter, Fingerprinting, Driving Waivers, Policy Ack.)  
**Cell Color:**
- 🟢 Green (100% compliant)
- 🟡 Yellow (80–99% compliant)
- 🟠 Orange (50–79% compliant)
- 🔴 Red (< 50% compliant)
- ⬜ Gray (N/A for this camp's state)

**Interactive:** Click any cell to drill down to the list of non-compliant individuals.

### Filters
- By state (show only Georgia camps, Florida camps, etc.)
- By staff role (all, staff only, NPT only, volunteers only)
- By date range (show compliance as of specific date)

## 7.4 Financial Overview Dashboard

**Audience:** JMC Super Admin, Finance Team  
**Purpose:** Organization-wide financial health at a glance.

### Components

| Component | Visualization |
|---|---|
| **Budget vs. Actual** | Grouped bar chart — per camp, with variance indicators |
| **Expense Breakdown** | Stacked bar chart — categories across all camps |
| **Outstanding Payments** | Table with aging buckets (0–30, 31–60, 61–90, 90+ days) |
| **Revenue Collection** | Per-camp donut chart (Paid / Partial / Unpaid / Subsidy Pending) |
| **Vendor Compliance** | Grid showing W9 ✓/✗, 1099 ✓/✗, Active Contract ✓/✗ per vendor |
| **Bank Reconciliation** | Monthly status grid (camp × month, Green/Yellow/Red) |
| **Expense Approval Queue** | List of pending approvals with age and amount |

## 7.5 Incident Trends Dashboard

**Audience:** JMC Super Admin, JMC Admin, Safety Team  
**Purpose:** Identify patterns in safety incidents and escalations.

### Components

| Component | Visualization |
|---|---|
| **Incidents Over Time** | Line chart — monthly incident count, with severity breakdown |
| **Incidents by Type** | Horizontal bar chart — Injury, Behavioral, Medical, Security, Weather, Near-Miss |
| **Incidents by Camp** | Bar chart — total incidents per camp, color-coded by severity |
| **Average Resolution Time** | Gauge chart — by severity level |
| **Open vs. Closed** | Stacked area chart — trend over time |
| **Severity Distribution** | Pie chart — current open incidents by severity |
| **Escalation Response Time** | Box plot — time from intake to assignment, by severity |

## 7.6 Enrollment Tracking Dashboard

**Audience:** JMC Super Admin, JMC Admin, Camp Teams  
**Purpose:** Real-time visibility into participant enrollment pipeline.

### Components

| Component | Visualization |
|---|---|
| **Application Funnel** | Funnel chart — Applied → Reviewed → Accepted → Enrolled → Ready, with drop-off rates |
| **Enrollment by Camp** | Horizontal bar chart — target capacity vs. current enrollment per camp |
| **Enrollment Trend** | Line chart — weekly enrollment count, with prior year comparison |
| **Document Completion** | Matrix — participants × documents (waiver, health form, payment), with completion % |
| **Waitlist Status** | Per-camp count with movement trend |
| **Subsidy Impact** | Subsidy applications vs. approvals, overlay with enrollment conversion |
| **Geographic Distribution** | Map visualization — participant locations (if address data available) |

---

# Appendix A: Glossary

| Term | Definition |
|---|---|
| **JMC** | Jubilee Monuments Corporation — the operating organization |
| **iUSA** | External participant management system used for applications and registration |
| **NPT** | Non-Paid Team — volunteer team members supporting camp operations |
| **HCP** | Healthcare Professional — medical staff assigned to camps |
| **COI** | Certificate of Insurance — proof of insurance coverage for a specific site or activity |
| **YPT** | Youth Protection Training — required safety certification for all adults working with youth |
| **W9** | IRS Form W-9 — used to collect vendor taxpayer identification information |
| **1099** | IRS Form 1099-NEC — issued to vendors paid $600+ in a tax year |
| **RBAC** | Role-Based Access Control — security model where access is determined by user role |
| **RLS** | Row-Level Security — database feature that restricts row access based on user attributes |
| **MFA** | Multi-Factor Authentication — requiring multiple verification methods for login |
| **TOR** | Terms of Reference — document defining expectations and responsibilities for a role |
| **ITREB** | Ismaili Tariqah and Religious Education Board |
| **QOL** | Quality of Life — holistic measure of participant and staff experience |
| **AJPF** | Al Jubilee Philanthropic Fund |
| **PII** | Personally Identifiable Information — data that can identify an individual |
| **UAT** | User Acceptance Testing — end-user validation before go-live |

---

# Appendix B: Module Dependency Map

```
                    ┌──────────┐
                    │  People  │ (D)
                    │  Module  │
                    └────┬─────┘
                         │
          ┌──────────────┼──────────────┐──────────────┐
          │              │              │              │
    ┌─────┴─────┐  ┌─────┴─────┐  ┌────┴──────┐ ┌────┴──────┐
    │ Compliance │  │  Finance  │  │ Healthcare│ │   Subsidy │
    │    (E)     │  │    (C)    │  │    (L)    │ │    (K)    │
    └─────┬─────┘  └─────┬─────┘  └───────────┘ └───────────┘
          │              │
    ┌─────┴─────┐  ┌─────┴─────┐
    │  Safety & │  │  Vendors  │
    │ Security  │  │ (in C)    │
    │   (B)     │  └─────┬─────┘
    └─────┬─────┘        │
          │         ┌────┴─────┐──────────┐
    ┌─────┴─────┐   │  Sites   │ Transport │
    │Escalation │   │   (F)    │    (J)    │
    │   (T)     │   └────┬─────┘──────────┘
    └───────────┘        │
                   ┌─────┴─────┐
                   │ Insurance  │
                   │    (I)     │
                   └───────────┘

  Independent Modules (minimal cross-dependencies):
  ┌───────────┐ ┌───────────┐ ┌───────────┐ ┌───────────┐
  │ Marketing │ │ Calendar  │ │  Content  │ │   AJPF    │
  │   (G)     │ │   (O)     │ │   (S)     │ │   (P)     │
  └───────────┘ └───────────┘ └───────────┘ └───────────┘
  ┌───────────┐ ┌───────────┐ ┌───────────┐
  │Evaluations│ │ Corporate │ │   Swag    │
  │   (H)     │ │   (M)     │ │   (Q)     │
  └───────────┘ └───────────┘ └───────────┘
```

---

*End of Document*
