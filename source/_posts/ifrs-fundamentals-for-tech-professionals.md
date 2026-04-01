---
title: "IFRS Fundamentals: What Tech Professionals Should Know About International Accounting Standards"
date: 2026-03-31 12:00:00
tags:
  - IFRS
  - accounting
  - auditing
  - finance
  - international-standards
categories:
  - Accounting & Auditing
description: "An accessible overview of International Financial Reporting Standards (IFRS) — written for software engineers and tech professionals who work with financial data."
---

If you build software that touches financial data — invoicing, reporting, ERP integrations, compliance dashboards — you need at least a working understanding of IFRS. These standards determine how companies worldwide record, report, and disclose financial information.

As someone pursuing an M.Sc. in Accounting, Auditing & Tax Applications while working in software engineering, I see both sides: the technical implementation and the regulatory framework. This post bridges that gap.

<!-- more -->

## Key Takeaways

- IFRS is a set of business rules your software must reflect (classification, timing, measurement, disclosure).
- Revenue recognition (IFRS 15) and leases (IFRS 16) commonly impact product data models.
- Auditability isn’t optional: systems need traceability from numbers to source documents.

> **Note:** This post is educational and implementation-oriented. For decisions that affect reporting, always validate interpretations with qualified accounting/audit professionals.

> **Trademark & Copyright Notice:** IFRS Standards are issued by the International Accounting Standards Board (IASB) and are the intellectual property of the [IFRS Foundation](https://www.ifrs.org/). "IFRS," "IAS," "IASB," and "International Financial Reporting Standards" are registered trademarks of the IFRS Foundation. This post is an independent educational overview, not endorsed by or affiliated with the IFRS Foundation, and does not reproduce official standards text. For authoritative guidance, refer to the official standards at [ifrs.org](https://www.ifrs.org/). Nothing in this post constitutes professional accounting, auditing, or financial advice.

## What Is IFRS?

**International Financial Reporting Standards (IFRS)** are a set of accounting standards developed by the International Accounting Standards Board (IASB), headquartered in London. They provide a global framework for how companies prepare and present their financial statements.

Over **140 countries** use IFRS, including the European Union, Turkey, Australia, Canada, and much of Asia, Africa, and South America. The United States primarily uses US GAAP but the SEC permits foreign filers to use IFRS.

### Why Should Engineers Care?

If you're building:
- **ERP systems** — your data models must align with how transactions are classified under IFRS
- **Financial reporting tools** — your output must conform to disclosure requirements
- **Audit software** — you need to understand what auditors are looking for
- **Data pipelines for financial data** — revenue recognition timing, asset classification, and lease treatment all affect when and how numbers appear

Understanding IFRS isn't about becoming an accountant. It's about understanding the **business rules** that your software must enforce.

## The Conceptual Framework

Before diving into specific standards, IFRS has a **Conceptual Framework** that establishes foundational principles:

### Qualitative Characteristics of Useful Financial Information

1. **Relevance** — The information should actually matter for the decisions people are making
2. **Faithful Representation** — It should paint an accurate, unbiased, and reasonably complete picture
3. **Comparability** — Readers should be able to meaningfully compare figures across time periods and between different companies
4. **Verifiability** — Independent experts looking at the same data should be able to reach similar conclusions
5. **Timeliness** — The information needs to be available soon enough to actually influence decisions
6. **Understandability** — It should be presented clearly enough for someone with reasonable business knowledge to follow

### Elements of Financial Statements

| Element | Definition |
|---------|-----------|
| **Asset** | Something the company controls that is expected to bring it value in the future |
| **Liability** | Something the company owes that will likely require spending resources to settle |
| **Equity** | What remains for owners after all debts and obligations are accounted for |
| **Income** | When the company's economic position improves (through revenue or gains) |
| **Expense** | When the company's economic position decreases through its operations |

The fundamental equation: **Assets = Liabilities + Equity**

## Key IFRS Standards Every Professional Should Recognize

### IFRS 15 — Revenue from Contracts with Customers

This is arguably the most impactful standard for software companies. It replaced the older IAS 18 and introduced a **five-step model** for revenue recognition:

1. **Confirm a valid contract exists** with the customer
2. **Determine what distinct deliverables** (performance obligations) the contract includes
3. **Establish the total transaction price**
4. **Distribute that price** across each deliverable
5. **Record revenue** as each deliverable is completed or delivered over time

**Why it matters for tech:** A SaaS company selling a bundle (software license + implementation + support) can't recognize all revenue upfront. Each component is a separate performance obligation with its own recognition timing.

**Example:** A company sells a 12-month software license for $12,000 with a one-time setup fee of $3,000. Under IFRS 15:
- The $3,000 setup fee is recognized when the setup is completed
- The $12,000 license fee is recognized monthly ($1,000/month) over the service period

If your billing system recognizes all $15,000 in month one, your financial statements are wrong.

### IFRS 16 — Leases

IFRS 16 fundamentally changed how leases appear on balance sheets. Previously, operating leases were off-balance-sheet. Now, **nearly all leases** must be recognized as a right-of-use asset and a corresponding lease liability.

**Why it matters for tech:** If you're building financial reporting systems, your data model needs to handle:
- Right-of-use assets
- Lease liabilities with amortization schedules
- Interest expense calculations
- Lease modification scenarios

**Practical impact:** A company leasing office space for 5 years at $10,000/month now shows roughly $540,000 (depending on the discount rate used) as both an asset and liability on its balance sheet. This changes financial ratios like debt-to-equity and return on assets.

### IAS 1 — Presentation of Financial Statements

IAS 1 defines the overall structure of financial statements:

1. **Statement of Financial Position** (Balance Sheet)
2. **Statement of Profit or Loss** (Income Statement)
3. **Statement of Changes in Equity**
4. **Statement of Cash Flows**
5. **Notes** (including accounting policies and explanatory information)

If you're building financial dashboards, these five outputs are the standard deliverables.

### IAS 2 — Inventories

Inventories are measured at the **lower of cost and net realizable value (NRV)**.

Cost formulas allowed:
- **FIFO** (First-In, First-Out) — the oldest inventory items are recorded as sold first
- **Weighted Average Cost** — cost is averaged across all units available

Note: **LIFO** (Last-In, First-Out) is **not permitted** under IFRS, though it is allowed under US GAAP. This is a common difference that matters when building multi-jurisdiction inventory systems.

### IAS 16 — Property, Plant and Equipment (PPE)

PPE assets are initially measured at **cost**, then subsequently measured using either:
- **Cost model** — cost minus accumulated depreciation minus impairment
- **Revaluation model** — fair value at revaluation date minus subsequent depreciation

**Depreciation methods:**
- Straight-line
- Diminishing balance
- Units of production

Your asset management software must support the entity's chosen method and allow for periodic review of useful life estimates.

### IAS 36 — Impairment of Assets

An asset is impaired when its **carrying amount exceeds its recoverable amount**. The recoverable amount is the higher of:
- Fair value less costs of disposal
- Value in use (present value of future cash flows)

Impairment tests are required annually for goodwill and intangible assets with indefinite useful lives.

### IAS 37 — Provisions, Contingent Liabilities and Contingent Assets

| Type | Recognition |
|------|------------|
| **Provision** | Recognized when the company has a current obligation, it is likely that resources will need to be spent, and the amount can be reasonably estimated |
| **Contingent Liability** | Disclosed in notes but not recognized on balance sheet |
| **Contingent Asset** | Disclosed only if probable; never recognized until virtually certain |

## IFRS vs US GAAP: Key Differences

| Area | IFRS | US GAAP |
|------|------|---------|
| Framework | Principles-based | Rules-based |
| Inventory | LIFO not permitted | LIFO permitted |
| Development costs | Capitalized if criteria met (IAS 38) | Expensed as incurred (except software) |
| Revaluation of PPE | Allowed | Not allowed |
| Revenue | IFRS 15 (single model) | ASC 606 (very similar but implementation differences) |
| Lease classification | Single model (IFRS 16) | Two models (ASC 842) |

If you're building software for multinational companies, your system may need to support **both frameworks** simultaneously with different recognition and measurement rules.

## IFRS in Turkey: TMS/TFRS

Turkey adopted IFRS through the **Turkish Accounting Standards (TMS)** and **Turkish Financial Reporting Standards (TFRS)**, which are direct translations of IFRS/IAS standards maintained by the **Public Oversight, Accounting and Auditing Standards Authority (KGK)**.

| IFRS Standard | Turkish Equivalent |
|---------------|-------------------|
| IFRS 15 | TFRS 15 |
| IFRS 16 | TFRS 16 |
| IAS 1 | TMS 1 |
| IAS 2 | TMS 2 |
| IAS 16 | TMS 16 |
| IAS 36 | TMS 36 |

Companies listed on Borsa Istanbul (BIST) are required to prepare their financial statements under TFRS. This is directly relevant to my M.Sc. thesis work on greenwashing detection in BIST Sustainability Index reports — the financial disclosures I analyze are prepared under these standards.

## How This Connects to Software Engineering

When I build systems that handle financial data, IFRS knowledge shapes my design decisions:

1. **Data models** need to accommodate multiple valuation methods (cost vs. revaluation)
2. **Revenue recognition logic** must handle multi-element arrangements and time-based allocation
3. **Reporting modules** must produce all five statement types defined by IAS 1
4. **Audit trails** must support verifiability — every number must be traceable to source documents
5. **Multi-jurisdiction support** may require parallel accounting treatments (IFRS + local GAAP)

Understanding the standard doesn't mean implementing it from scratch. It means knowing what your system needs to support and having informed conversations with accountants, auditors, and business stakeholders.

## Further Reading

- [IFRS Foundation](https://www.ifrs.org/) — Official standards and resources
- [KGK (Turkey)](https://www.kgk.gov.tr/) — Turkish accounting standards authority
- [IAS Plus by Deloitte](https://www.iasplus.com/) — Comprehensive third-party summaries of each standard
- Wiley IFRS (published by Wiley) — Practical interpretation guides

*In upcoming posts, I'll dive deeper into specific standards — particularly IFRS 15 revenue recognition for SaaS companies and how NLP can be applied to detect greenwashing in sustainability reports prepared under TFRS.*

## Related Posts

- {% post_link welcome-to-my-blog Welcome to My Blog (Context & Topics) %}
- {% post_link essential-sap-transaction-codes Essential SAP Transaction Codes (Daily Reference) %}
