# Automated Action and Dependency Governance Workflow

*Transition from manual action tracking to SLA driven automated governance and risk ranked PMO oversight.*

VERSION 1.0.

 

30/09/2026

# 1.     EXECUTIVE SUMMARY SNAPSHOT

Currently, cross-functional actions and dependencies raised in governance meetings are tracked manually in a static action log. Because approval request timestamps are not captured and requests happen informally via email or chat, there is no active Service Level Agreement (SLA) clock. Consequently, stale items remain open for months or years, and the PMO only discovers critical delays reactively during status meetings, resulting in ad-hoc escalations to Executive Sponsors.

# 2.     PROJECT DESCRIPTION

This project introduces an automated governance workflow that captures formal dependency and approval timestamps, enforces a multi-tier SLA escalation engine, automatically flags 90-day stale items, and dynamically ranks the weekly PMO watchlist by calculated risk score. It will capture “Approval Request Date” and “Approver Function” on 100% of dependent actions. With current data it is seen that the approval turnaround time is taking more than 200+ days in some cases. This automation will reduce the average approval turnaround time by automating the “Approver function” notifications and escalations to the “Executive sponsors”. Thus, it will automatically flag 100% of open items untouched for 90-days for mandatory governance review. This will replace manual status checks with an automated weekly PMO watchlist ranked by composite risk score. 

# 3.     PROJECT SCOPE

| **IN SCOPE** | **OUT OF SCOPE** |
| --- | --- |
| Structured action logging with mandatory dependency and approver fields. | Automated resource re allocation without PMO or Executive Sponsor sign off. |
| Automated SLA clock initiation and drift calculation | Restructuring internal departmental processes within individual Approver Functions. |
| Approver Function and Executive Sponsor breach alerts. | Retroactive SLA breach penalties for legacy historical items prior to system cutover. |
| Automated risk score ranking for the weekly PMO watchlist. |  |
| Mandatory capture of “Approval Date” at closure |  |
| 90 day inactivity detection and review flagging. |  |








# 4.     STAKEHOLDER MATRIX (RACI)

| **Role** | **Role in TO-BE process** | **RACI** |
| --- | --- | --- |
| **Action Owner** | - Logs actions - Identifies dependencies and approver functions - Initiates approval requests, and executes tasks. | **R** (Responsible) |
| **Approver Function** | - Reviews dependency requests within the SLA window and records formal approval or rejection decisions. | **R** (Responsible) |
| **PMO** | - Validates process governance - Monitors the risk-ranked weekly watchlist, and reviews 90 day stale flags. | **A / C** (Accountable / Consulted) |
| **Executive Sponsor** | - Receives escalation SLA breach escalations and resolves high priority cross functional bottlenecks. | **A / I** (Accountable / Informed) |

# 5.     PROCESS SUMMARY (AS-IS vs. TO-BE)

# 6.     ‘AS-IS’ TO ‘TO-BE’ MAPPING

| **Callout ID** | **AS-IS pain point description** | **TO-BE automated solution** | **Business impact** |
| --- | --- | --- | --- |
| 1 | Missing request date and dependency metadata | Mandatory logging of dependency flag, Approver Function, and automated “Approval Request Date” capture upon creation. | Establishes absolute accountability and baseline metrics from Day 1. |
| 2 | Informal approval channels | Structured “Review and Approve Action” task assigned directly to the designated Approver Function swimlane. | Eliminates untraceable requests and enforces standardized workflow entry. |
| 3 | No SLA clock | Multi-tier SLA countdown engine with automated non-interrupting boundary timers and a daily **90-Day Stale Item** check. | Drastically reduces average approval turnaround time and enforces data hygiene |
| 4 | Reactive ad hoc escalations | Automated Tier-1 email reminders, Tier-2 Executive Sponsor escalations, and a weekly **Risk-Ranked PMO Watchlist**. | Shifts governance from reactive firefighting to proactive, data-driven oversight. |

# 7. REQUIREMENT TRACEABILITY MATRIX AND UAT-TEST CASES

| **Requirement ID** | **Requirement description** | **Priority** | **Verification method** | **UAT test case ID and scenario** | **Expected test results** |
| --- | --- | --- | --- | --- | --- |
| **FR-01** | System must require a dependency flag (Yes/No). If Yes, Approver Function is mandatory. | Must have | Inspection / Functional test | **UAT-01:** Attempt to save a dependent action without selecting an Approver Function. | System blocks saving and displays a validation error requiring an Approver Function. |
| **FR-02** | System must timestamp “Approval Request Date” and start the SLA clock upon status change. | Must have | System log verification | **UAT-02:** Move a dependent action to *Pending Approval*. Verify timestamp in the Data Store. | “Approval Request Date” is auto populated with the exact UTC timestamp and SLA countdown initiates. |
| **FR-03** | System must calculate elapsed time daily and send an alert at the 1st SLA Breach threshold. | Must Have | Automated notification test | **UAT-03:** Simulate an action exceeding the 1st SLA threshold without approval. | System dispatches an automated notification to the assigned Approver Function within the designated window. |
| **FR-04** | System must trigger a Tier-2 escalation to the Executive Sponsor at the 2nd SLA Breach threshold. | Must Have | Workflow escalation test | **UAT-04:** Simulate an action passing the 2nd SLA breach threshold. | System automatically routes an escalation task to the Executive Sponsor lane and logs the event. |
| **FR-05** | System must calculate composite “Risk Score” and rank the weekly PMO watchlist descending. | Must Have | Report verification | **UAT-05:** Generate the PMO watchlist with multiple active, breached, and escalated items. | Watchlist correctly sorts items by computed risk score (highest risk at the top). |
| **FR-06** | System must capture “Approval Date” at closure and prevent backdating prior to request date. | Must Have | Boundary and date logic test | **UAT-06:** Try to approve an action with an “Approval Date” set prior to “Approval Request Date”. | System rejects the backdated entry and requires a valid current or subsequent timestamp. |
| **FR-07** | System must run daily checks to flag open items where “Last Modofied Date \>= 90 days”. | Must Have | Scheduled job test | **UAT-07:** Run the 90-day stale item batch job against a test record inactive for 91 days. | Record is successfully flagged with “Scale Review Flag = True” on the PMO governance dashboard. |
