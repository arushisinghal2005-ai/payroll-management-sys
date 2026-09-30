\# Daily-Wage Payroll \& Attendance Management System



A standalone, privacy-first Single Page Application (SPA) designed for daily-wage, contractor, and shift-based workforce operations.



The platform eliminates fixed monthly salaries in favor of dynamic earnings calculated strictly from per-worker daily rates, tracked attendance status, overtime hours, bonuses, and debt recoveries. All state is maintained locally in the browser with zero external server dependencies.



\---



\## Key Features



\- \*\*Dynamic Daily Wage Engine\*\*: Real-time gross and net wage calculation based on attendance, overtime hours, and custom deductions:

&#x20; $$\\text{Net Pay} = (\\text{Present Days} \\times \\text{Daily Rate}) + (\\text{OT Hours} \\times \\text{OT Rate}) + \\text{Bonus} - (\\text{Advance Deductions} + \\text{Other Deductions})$$

\- \*\*Historical Rate Snapshots\*\*: Processing a pay run locks historical daily rates, OT rates, attendance counts, and advance deductions. Changes made to worker profiles later will never alter past pay slips.

\- \*\*Interactive Calendar Grid\*\*: Click-to-paint attendance calendar tracking Present (`P`), Absent (`A`), Half Day (`HD`), Leave (`L`), and Holiday (`H`).

\- \*\*FIFO Advance \& Recovery Ledger\*\*: Tracks employee salary advances, enforces automated monthly deduction caps, and automatically balances recoveries against outstanding debt.

\- \*\*Client-Side Privacy\*\*: Runs 100% in the browser using the Web Storage API (`localStorage`). No tracking, no external database, and zero latency.

\- \*\*Reporting \& Data Portability\*\*: Single-click CSV payroll exports, print-formatted payslips, and complete JSON backup/restore pipelines.



\---



\## Technical Architecture \& Design Decisions



\### 1. Zero-Backend State Architecture

The system is built as a self-contained Single Page Application (SPA):

\- \*\*Centralized State\*\*: Global application state is managed in a single store synchronized to browser `localStorage` on every mutation.

\- \*\*Deterministic Re-rendering\*\*: UI updates execute top-down rendering routines bound to UI state slices, eliminating DOM desynchronization.



\### 2. Historical Immutability (Rate-Snapshotting)

In standard payroll databases, recalculating past wages from mutable worker master records corrupts historical runs whenever a worker receives a raise. 

\- When a pay cycle is finalized, an immutable record is generated locking daily rates, OT rates, attendance counts, and advance deductions.

\- Future rate modifications or policy updates only apply forward to open drafts, ensuring ledger integrity.



\### 3. FIFO Debt-Recovery Engine

Worker advances operate via an amortized ledger:

\- Payout deductions are applied across open advances in chronological order (First-In, First-Out).

\- Deductions strictly enforce a debt-ceiling guardrail ($\\text{Deduction} \\le \\text{Outstanding Balance}$), eliminating negative debt states.

\- Supports atomic payroll undo operations, reversing locked runs while rolling back associated ledger recovery records.



\---



\## Tech Stack



\- \*\*Frontend\*\*: Vanilla JavaScript (ES6+), HTML5, Semantic CSS3 (Flexbox/CSS Grid)

\- \*\*Persistence\*\*: Web Storage API (`localStorage`)

\- \*\*Data Export\*\*: Native Blob API (CSV and JSON export streams)

\- \*\*Typography\*\*: IBM Plex Sans, IBM Plex Mono, Fraunces



\---



\## Getting Started



Because the application runs entirely in the browser with no build step or dependencies:



1\. \*\*Clone the repository:\*\*

&#x20;  ```bash

&#x20;  git clone \[https://github.com/](https://github.com/)<your-username>/payroll-management-system.git

&#x20;  cd payroll-management-system

