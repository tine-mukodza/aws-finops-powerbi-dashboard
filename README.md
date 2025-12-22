### *Cloud Cost Optimization Dashboard | Business Intelligence & FinOpsd*

This project delivers a complete FinOps Cost Intelligence Dashboard analyzing AWS spending for October 2025, built end-to-end in Power BI using FinOps Foundation principles.

It provides:

Cost visibility

- Optimization modeling
- Rightsizing insights
- Tagging health
- Pricing model efficiency
- Daily anomalies & waste signals
  
The dashboard uses curated DAX measures, KPI engineering, allocation logic, and spend modeling (On-Demand → Savings Plans) to identify cost drivers and expose optimization opportunities.

---

##  Project Overview

This FinOps dashboard uncovers:

- Total AWS spend across services, regions, usage types, and pricing models
- Which workloads drive the highest cost
- Where resources are over-provisioned
- Which services should move to Savings Plans/Reserved
- Daily spend anomalies caused by unusual workloads
- Monthly savings opportunities from tuning compute, storage, and data transfer

The solution is organized into two analytical pages, each with a strategic purpose.
---

## **Page 1 - Executive Cost Summary**
**File:** `page1_summary.png`

![Overview Page](overview_page.png)

This page gives management a high-level understanding of cloud spend, drivers, and patterns.
### Key Features
- Total AWS Spend
- Key Features
- Total AWS Spend (Oct 2025)
- Average & Max Daily Cost
- Active Services
- Active Regions
- Production Cost %
- Average Cost per Service
- Daily Spend Trend
- Cost by Pricing Model
- Cost by Environment (Prod/Stage/Dev)
- Top Services by spend
- Top Regions by spend
- Cost by UsageType

---

## **Page 2 - Optimization Insights**
**File:** `page2_insights.png`

![Optimization Insights Page](optimization_insights_page.png)

This page transforms raw billing data into actionable optimization strategies.

### Optimization KPIs
- Estimated Savings (On-Demand → Savings Plans): $10.9K
- Rightsizing Opportunity: 22%
- Daily Cost StdDev: $518.30
- Monthly Spend: $50.12K  

### Cost Driver Deep-Dives
- Cost Drivers by Service
- Spend by ServiceName
- Spend by Region
- Spend by UsageType
- Spend by Tag — Environment
- Spend by Pricing Model
  
##*Waste & Anomaly Detection*

- Daily spend anomalies (spikes > 2× baseline)
- Staging/Development environments showing unnecessary cost
- Over-provisioned compute/storage services
---

##  **Key DAX Measures Used**

```DAX
Total AWS Cost = SUM('aws_billing_daily_oct2025'[TotalCost])

Avg Daily Cost = 
AVERAGEX(
    VALUES('aws_billing_daily_oct2025'[Date]),
    CALCULATE(SUM('aws_billing_daily_oct2025'[TotalCost]))
)

Max Daily Cost = 
MAXX(
    VALUES('aws_billing_daily_oct2025'[Date]),
    CALCULATE(SUM('aws_billing_daily_oct2025'[TotalCost]))
)

Active Services = DISTINCTCOUNT('aws_billing_daily_oct2025'[ServiceName])

Regions Used = DISTINCTCOUNT('aws_billing_daily_oct2025'[Region])

Production Cost % =
DIVIDE(
    CALCULATE(SUM('aws_billing_daily_oct2025'[TotalCost]), 'aws_billing_daily_oct2025'[Tag_Environment] = "Production"),
    SUM('aws_billing_daily_oct2025'[TotalCost])
)

Avg Cost per Service =
DIVIDE([Total AWS Cost], [Active Services])

Estimated Savings (OnDemand_SP) =
[Total AWS Cost] * 0.30   -- Assuming 30% savings potential

Rightsizing % =
DIVIDE([Estimated Savings (OnDemand_SP)], [Total AWS Cost])

Daily Cost StdDev =
STDEVX.S(
    VALUES('aws_billing_daily_oct2025'[Date]),
    CALCULATE(SUM('aws_billing_daily_oct2025'[TotalCost]))
)
```
# Insights Summary (Business + Technical)
## 1.Major Cost Drivers

- Highest spend from AWS Glue, Redshift, RDS, and EC2
- Primary region: US-East-1
- Heavy usage types: TimedStorage-GB, DataTransfer-Out, Requeststs
- 72% of spend is On-Demand → strong optimization opportunity
  
## 2.Optimization Opportunities

- Converting On-Demand to Savings Plans yields ~30% savings
- Rightsize low-utilized compute/storage resources
- Consolidate workloads across regions
- Reduce large DataTransfer-Out workloads causing hidden cost spikes

## 3.Anomaly Detection

- Several daily spikes >2× above baseline

- Likely sources: ETL pipeline inefficiencies, temporary workloads, unplanned data transfer

## 4.Estimated Savings

~$10.9K/month in potential savings through:

~Savings Plans

~Rightsizing

~Eliminating waste in Staging/Dev

~Reducing data-transfer inefficiencies 

## Skills Demonstrated
- Built a multi-page Power BI dashboard with professional KPI layout and UX design
- Engineered custom DAX measures (AVERAGEX, MAXX, DISTINCTCOUNT, STDEVX.S)
- Applied FinOps best practices: savings modeling, rightsizing, tagging, anomaly detection
- Identified cost drivers across services, regions, pricing models
- Modeled savings from On-Demand - Savings Plans transitions
- Interpreted AWS usage patterns (storage, compute, requests, data transfer)
- Delivered a complete BI - FinOps - Optimization lifecycle
- Packaged the project into a structured, professional GitHub repository

---
👨‍💻 Author

Tinevimbo Mukodza
MS Information Systems — Pace University
FinOps & Business Intelligence Analytics Portfolio
GitHub: https://github.com/tinemukodza/finops-analytics-portfolio





