# Bank-Transactions-Analytics
A Power BI report for exploring transaction flows, branch performance, customer segments, channels, and transaction risk. The report combines financial performance measures with operational status and anomaly views.

# Bank Transactions Analytics

## Small overview

A Power BI report for monitoring transaction flows, transaction outcomes, branch and channel performance, customer segments, and high-value activity. The analysis uses 8,000 transactions dated in 2024.

![Bank transactions overview](Dashboard%20Screenshots/Home.png)

## Business questions

- How much value comes in and goes out, and how does net flow change over time?
- What share of transactions succeed, fail, or remain pending?
- Which transaction types and branches contribute most to successful net flow?
- Which channels have the most failed transactions, and where are customer service improvements needed?
- How do transaction outcomes vary by customer account, income, credit-score, and tenure bands?
- How can the bank review high-value activity and resolve pending transactions while avoiding unnecessary customer friction?

## Data

The separately provided source workbook, `bank_transactions_analytics.xlsx`, was used to validate the report. It is not currently in the project folder and contains three tables:

- `fact_transactions` — 8,000 records dated January–December 2024, with transaction ID, customer, branch, date, type, channel, signed amount, and status
- `dim_customer` — 600 customer records with age, gender, city, account type, credit score, monthly income, and account-open date
- `dim_branch` — 10 branches with branch name, city, and region

The project folder contains `Bank Transactions Analysis.pbix` and a `Dashboard Screenshots/` folder with exported report pages. The amounts are displayed with a `$` symbol; the currency code is not specified in the supplied files. Customer and financial attributes are present in the separate source workbook, so confirm its origin and whether it is safe to publish before adding that workbook to a public repository.

## Dashboard pages

1. **Home Page** — headline transaction, customer, inflow, outflow, net-flow, success, pending, and failure KPIs, plus monthly net flow.
2. **Overview** — report navigation.
3. **Revenue and transactions performance** — transaction counts by month, average transaction value and net flow by transaction type, and failed/pending rates by type. 
4. **Branch performance** — branch volume and value rankings, failed-transaction rates, transaction counts, and net flow.
5. **Customers** — account-type outcomes, customer and gender comparisons, top customers by value, and successful transaction value by city.
6. **Customers 2** — income, tenure, and credit-score views. 
7. **Channels** — transaction and value share, average transaction value, and failure rate by channel. 
8. **Risk and Anomalies** — high-value activity, pending transactions, failed transactions by customer, failed rates by credit band, and monthly net flow. 

## Detailed key findings

- The source contains **8,000 transactions** for **600 customers** across **10 branches**. It spans **January–December 2024**.
- There are **7,214 successful transactions (90.18%)**, **562 failed (7.03%)**, and **224 pending (2.80%)**. The Home Page rounds these to 90%, 7%, and 3%.
- For successful transactions, signed inflows total about **$5.712M**, outflows about **$4.689M**, and net flow about **$1.023M**. The raw file’s all-status totals are different: about **$6.304M** positive amounts and **$5.203M** negative amounts, netting to **$1.102M**. The report’s headline flow is therefore a successful-status view; label it that way when using it for decisions.
- Monthly successful net flow peaks in **October at about $166,014** and reaches its low in **June at about $21,156**. October also has the highest transaction volume (**719**); March and September are lowest at **635** each.
- Deposits contribute about **$4.373M** of successful net flow. Withdrawals contribute about **-$2.198M**, bill payments **-$676,098**, POS purchases **-$354,142**, and transfers **-$121,690**. The average absolute transaction value is highest for Deposits (**$2.39K**) and Transfers (**$2.04K**), and lowest for POS Purchases (**$312**).
- **Luxor Branch** has the most transactions (**846**) and the lowest branch failure rate (**4.61%**). **Tanta Branch** has the fewest (**763**). **Suez Branch** has the highest branch failure rate (**8.26%**). **Nasr City** has the largest successful net flow (**$204,758**), while **Aswan Branch** has the smallest (**$24,203**).
- The account-type table shows the highest failure rate for **Credit accounts (8.30%)**, followed by Checking (**6.95%**) and Savings (**6.62%**).
- The dashboard shows outflow at **7.59% of income** overall, with **16.77%** for the under-$8K income band and **1.75%** for the $25K+ band. The raw workbook has **18 customers with missing monthly income**
- Channel attribution is blank for **160 transactions (2.0%)** in the raw data. The Channels screenshot assigns this group **7.5% of transaction value**, and shows an average transaction value of about **$1.55K**. This is a disproportionate amount of value for an unclassified channel and merits a data-capture review.
- The raw data identifies **163 transactions (2.04%)** with an absolute amount of at least **$5,000**, totaling about **$1.014M** in absolute value. The screenshot’s high-value count and amount match this threshold. These transactions are mostly Deposits (**96**) and Transfers (**60**), with **7 Withdrawals**.
 
## Advanced recommendations

1. **Improve reliability in branch and ATM transactions.** Raw transaction counts show failure rates of **7.74% for Branch** and **7.65% for ATM**, versus **6.27% for Mobile App**. Review decline and error reasons, ATM availability, and branch processing steps; pilot fixes at selected locations. Where customers are comfortable, guide them toward reliable digital options for routine transactions while keeping branch and ATM access available. Track failure rate, successful completion, repeat attempts, and complaints. The channel chart shows different rates, so verify the operational KPI before setting targets.
2. **Give Suez Branch a focused service-improvement plan.** Suez has the highest branch failure rate (**8.26%**) and Luxor the lowest (**4.61%**). Have the Suez manager examine failed transactions by type, time, system, and reason, then assign an owner to the main cause. Compare its failure and completion rates with the branch's own baseline and Luxor after the change.
3. **Resolve pending transactions promptly.** The report shows **224 pending transactions (2.80%)** and about **$28,961** in signed pending value. Establish an operations queue with age-based escalation, customer updates, and an owner for each case. Prioritize by customer impact and gross amount at risk, not signed net value alone. Measure time to resolution and the share that complete, fail, or are reversed.
4. **Apply proportionate safeguards to high-value activity.** The dataset contains **163 transactions of at least $5,000**, totaling about **$1.014M** in absolute value; 96 are Deposits and 60 are Transfers. Review these against the bank's existing transaction-monitoring rules and use verification or manual review where policy requires it. Track alert accuracy, false positives, review time, and customer friction. High value alone should not be treated as evidence of fraud.
5. **Use the flow pattern in treasury and service planning.** Successful transactions produce about **$5.712M** in inflows and **$4.689M** in outflows, for **$1.023M** net flow. Monthly net flow ranges from about **$21,156 in June** to **$166,014 in October**. Treasury teams can use current, multi-year production data to forecast liquidity needs and plan support coverage for busy periods. Net flow is a cash movement measure, not profit.
6. **Offer voluntary cash-flow support to customers who may benefit.** The dashboard shows a higher outflow-to-income share for the under-$8K income band (**16.77%**) than for the $25K+ band (**1.75%**). After confirming the calculation and missing-income treatment, offer opt-in balance alerts, budgeting tools, or payment scheduling. Do not use this measure alone to restrict accounts or change credit terms.
7. **Make failed-payment recovery easier for customers.** With **562 failed transactions (7.03%)**, provide clear status messages, practical retry guidance, and a straightforward route to support or reversal when appropriate. Monitor repeat failures, time to resolution, and customer complaints to see whether the changes reduce disruption.

## Tools

- Microsoft Power BI Desktop
- Power Query and the Power BI data model
- DAX measures and Power BI visuals
- Microsoft Excel source workbook
