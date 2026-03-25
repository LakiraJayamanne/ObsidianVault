---
Class: CO1109
Topic: Exam Revision — All Lectures
Date: 2026-03-23
Exam: 2026-03-27
Related: Business and Financial Computing
---

# CO1109 Exam Revision

> Exam Friday 27th March. All 9 lectures in scope.

---

## Lecture 1 — Business Fundamentals

### Core Concepts
- **The Economic Problem** — unlimited human wants vs limited resources
- **Factors of Production** — Land, Labour, Capital, Enterprise (combine to create products/wealth)
- **The Financial Cycle** — investors provide funds (loans/stock) → company generates profits/wages → returns to investors

### Types of Business Entity

| Type | Key Feature |
|---|---|
| Sole Trader | One owner, no legal separation between owner and firm |
| Partnership | Multiple owners, dissolves if a partner dies or withdraws |
| Private Limited (Ltd) | Separate legal entity, liability limited to investment, cannot trade shares publicly |
| Public Limited (Plc) | Same as Ltd but can sell shares on a stock exchange |

### Added Value
$$\text{Added Value} = \text{Selling Price} - \text{Cost Price}$$

---

## Lecture 2 — Financial Statements and Analysis

### The Accounting Equation
$$\text{Assets} = \text{Liabilities} + \text{Equity}$$

Rearranges to:
- Assets − Liabilities = Equity
- Assets − Equity = Liabilities

### The Three Key Financial Statements

| Statement | What it shows | Timeframe |
|---|---|---|
| **Statement of Financial Position** (Balance Sheet) | Assets, liabilities, and equity | Point in time (snapshot) |
| **Income Statement** (P&L) | Revenues, costs, and expenses | Accounting period |
| **Statement of Cash Flows** | Cash receipts, disbursements, net change in cash | Accounting period |

- Balance sheet must **always balance** — both sides must be equal
- "Cash is King" — sufficient cash is critical for short-term operations, purchases, and acquisitions

### Financial Ratios

#### Tests of Profitability
$$\text{Gross Profit Margin} = \frac{\text{Gross Profit}}{\text{Sales}} \times 100$$

$$\text{Return on Sales} = \frac{\text{Operating Profit}}{\text{Net Sales}}$$

$$\text{Return on Capital Employed (ROCE)} = \frac{\text{Earnings Before Tax}}{\text{Capital Employed}} \times 100$$

> Capital Employed = Total Assets − Current Liabilities

#### Tests of Financial Health
$$\text{Current Ratio} = \frac{\text{Current Assets}}{\text{Current Liabilities}}$$

$$\text{Inventory Turnover} = \frac{\text{Cost of Sales}}{\text{Average Inventory}}$$

$$\text{Debt Ratio} = \frac{\text{Total Debts}}{\text{Total Assets}}$$

> Current ratio > 1 = company can cover short-term liabilities. Debt ratio closer to 0 = less leveraged.

---

## Lecture 3 — Finance for IT Decision Making

### Methods of Finance
- **Share Capital** — selling ownership stakes
- **Venture Capital** — high-risk investment in exchange for equity
- **Grants** — government funding (no repayment)
- **Leasing** — renting assets instead of buying (avoids large cash outflow)
- **Loans** — borrowed money repaid with interest

### Investment Appraisal — The Three Methods

#### 1. Return on Investment (ROI)
$$\text{ROI} = \frac{\text{Net Benefits}}{\text{Total Costs}} \times 100$$

> Example: Benefit = £200K, Cost = £1M → ROI = (200K / 1M) × 100 = **20%**

#### 2. Payback Period (PB)
$$\text{Payback Period} = \frac{\text{Initial Cost}}{\text{Annual Income/Saving}}$$

> Example: £1M investment, saves £250K/year → PB = 1,000,000 / 250,000 = **4 years**

#### 3. Average Rate of Return (ARR)
1. Total Profit = Total net cash flows − initial outlay
2. Average Annual Profit = Total Profit ÷ number of years
3. ARR = (Average Annual Profit / Initial Outlay) × 100

#### 4. Net Present Value (NPV)
- Accounts for **time value of money** — future money is worth less than today's money
- Higher positive NPV = better project
- Compare two projects → pick the one with the higher NPV

---

## Lecture 4 — Business Information Systems (BIS)

### Definition
A group of interrelated components (input, processing, output, storage, control) that convert **data into information** to support organisational decision-making.

### Strategic Objectives of BIS
- Operational excellence
- New products/services
- Customer/supplier intimacy
- Improved decision-making
- Competitive advantage

### Data Types
| Type | Description |
|---|---|
| Quantitative (Hard) | Statistics, figures, measurable |
| Qualitative (Soft) | Opinions, characteristics, descriptions |

### Information Processing Types
- **Classification** — categorising data
- **Sorting** — ordering data
- **Aggregation** — summarising data
- **Calculation** — performing operations on data
- **Selection** — filtering based on criteria

---

## Lecture 5 — Enterprise IT Architecture

### Technology Laws (know these)
| Law | What it says |
|---|---|
| Moore's Law | Microprocessor power doubles approximately every 2 years |
| Law of Mass Digital Storage | Storage costs fall exponentially; data production doubles annually |
| Metcalfe's Law | Network value = n² (where n = number of nodes) |

**Metcalfe's Law Example:** 10 nodes → value = 100. Add 1 node (n=11) → value = 121.

### IT Infrastructure Components
Hardware, Software, Databases, Networks, Procedures, People

### Architectural Paradigms

| Architecture | Key Characteristic |
|---|---|
| Mainframe | Centralised host does all processing; terminals only display ("dumb" terminals) |
| Client/Server | Distributed — client requests, server provides |
| Fat Client | Business logic on the **client** side |
| Thin Client | Business logic on the **server** side |
| 3-Tier | Adds an Application Server layer between client and DB |
| 4-Tier | Adds a Web Server layer on top of 3-tier |
| Cloud (IaaS) | Infrastructure as a Service — raw compute/storage/networking |
| Cloud (PaaS) | Platform as a Service — environment to build/run apps |
| Cloud (SaaS) | Software as a Service — ready-made software over the internet |

---

## Lecture 6 — Enterprise Applications

### The Big Three Systems

| System | Focus |
|---|---|
| ERP (Enterprise Resource Planning) | Internal processes — production, distribution, finance — one database |
| CRM (Customer Relationship Management) | Marketing, sales, customer interactions |
| SCM (Supply Chain Management) | Flow of materials/information through the supply chain |
| SRM (Supplier Relationship Management) | Sourcing, purchasing, warehousing |

### CRM Types
- **Operational CRM** — front-office processes (sales, marketing, service automation)
- **Analytical CRM** — analysing customer data for predictive insights

### Supply Chain Concepts
- **Bullwhip Effect** — demand information gets distorted as it passes between entities in the supply chain (small customer demand fluctuation → large manufacturer overreaction)
- **Push-Based** — production based on demand forecasts ("make what we predict we'll sell")
- **Pull-Based** — production driven by actual customer orders ("make what we've sold")

---

## Lecture 7 — The IT Organisation

### IT Governance (ITG)
Processes ensuring IT efficiently enables an organisation to achieve its goals and add value.

### Service Level Agreements (SLA)

| Type | Description |
|---|---|
| Customer-based | Agreement with a **specific customer** group |
| Service-based | Agreement for a **specific service** for all customers |
| Multi-level | Tiered — covers multiple parties or service levels |

### ITIL (IT Infrastructure Library)
A framework of **best practices** for managing the entire IT service lifecycle — from strategy and design through to operation and continual improvement.

---

## Lecture 8 — Business Intelligence (BI)

### Definition
Applications that transform raw data into meaningful information for actionable business insights.

### ETL Process
1. **Extract** — gather data from sources
2. **Transform** — standardise, clean, normalise the data
3. **Load** — place into a **Data Warehouse**

### KPIs (Key Performance Indicators)
Measurable targets used to evaluate performance. Must follow **SMART**:
- **S**pecific
- **M**easurable
- **A**chievable
- **R**elevant
- **T**ime-bound

---

## Lecture 9 — Data Analytics

### Types of Variables

| Type | Description | Example |
|---|---|---|
| Categorical | Finite groups | Gender, colour |
| Discrete (Numerical) | Counted, whole numbers | Number of children |
| Continuous (Numerical) | Measured, any value | Height, weight |

### Measures of Central Tendency

**Dataset example: 2, 6, 3, 5, 2, 8, 2, 12**

| Measure | Calculation | Result |
|---|---|---|
| Mean | Sum ÷ count = 40 ÷ 8 | **5** |
| Median | Order set → (2,2,2,3,5,6,8,12) → middle = (3+5)/2 | **4** |
| Mode | Most frequent value | **2** |

### Correlation vs Regression

| | Correlation | Regression |
|---|---|---|
| What it measures | Strength and direction of relationship | How an independent variable affects a dependent one |
| Variables | Interchangeable | Independent → Dependent |
| Output | Value between -1 and +1 | Line of best fit / prediction formula |
| Causation? | Does NOT imply causation | Does NOT imply causation |

**Correlation values:**
- +1 = perfect positive
- -1 = perfect negative
- 0 = no relationship

**Regression example:** y = 5x + 50 (x = hours studied, y = exam score)
→ Every extra hour of study adds 5 marks.

### Other Analytics Techniques
- **A/B Testing** — compare two versions to see which performs better
- **Data Mining** — automatically finding patterns in large databases
- **Classification (Supervised Learning)** — assign objects to pre-defined classes using labelled training data
- **Clustering (Unsupervised Learning)** — group unlabelled data by similarity
- **Outlier Detection** — identify data points that deviate significantly from the norm (used in fraud/threat detection)

---

## Quick-Reference Cheat Sheet

### All Formulas
| Formula | Expression |
|---|---|
| Added Value | Selling Price − Cost Price |
| Gross Profit Margin | (Gross Profit / Sales) × 100 |
| Current Ratio | Current Assets / Current Liabilities |
| Debt Ratio | Total Debts / Total Assets |
| Inventory Turnover | Cost of Sales / Average Inventory |
| Return on Sales | Operating Profit / Net Sales |
| ROCE | (Earnings Before Tax / Capital Employed) × 100 |
| Capital Employed | Total Assets − Current Liabilities |
| ROI | (Net Benefits / Total Costs) × 100 |
| Payback Period | Initial Cost / Annual Saving |
| ARR | (Average Annual Profit / Initial Outlay) × 100 |
| Metcalfe's Law | Value = n² |
| Mean | Sum of values / Count of values |

### Likely Exam Traps
- **Balance sheet vs Income Statement** — balance sheet is a *snapshot* (point in time), income/cash flow are *period* statements
- **Capital Employed** = Total Assets − Current Liabilities (not total assets alone)
- **Current ratio < 1** = danger sign (can't cover short-term debts)
- **Correlation ≠ Causation** — always state this
- **NPV** — higher positive = better, but know *why* (time value of money)
- **Fat vs Thin Client** — fat = logic on client, thin = logic on server (easy to mix up)
- **Push vs Pull supply chain** — push = forecast-driven, pull = order-driven
- **Ltd vs Plc** — Plc can sell shares publicly, Ltd cannot
- **Operational vs Analytical CRM** — front-office vs data analysis
