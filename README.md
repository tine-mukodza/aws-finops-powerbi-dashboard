# AWS Cloud Cost Optimization (FinOps Dashboard & Case Study)

This project analyzes **AWS Cloud Costs for October 2025** using Power BI.  
It applies **FinOps principles** including cost visibility, cost allocation, rightsizing, and optimization tracking.  
The dashboard includes **KPIs, DAX measures, visuals, and actionable optimization insights**.

---

##  Project Overview

This project is a two-page AWS Cloud Cost Optimization dashboard built in Power BI using October 2025 billing data. It applies FinOps principles such as cost visibility, rightsizing analysis, savings plan evaluation, environment-level cost allocation, and anomaly detection. The dashboard includes custom DAX measures, KPI cards, donut charts, trend visuals, and optimization insights designed for real-world FinOps workflows.

The FinOps dashboard uncovers:
- Total AWS spend across services, regions, pricing models, and usage types  
- High-cost drivers contributing to overall cloud cost  
- Rightsizing and Savings Plan optimization opportunities  
- Daily anomalies and unusual spend patterns  
- Estimated savings if shifting from **On-Demand to Savings Plans**

The report is split into **two pages**:

---

## **Page 1 - Executive Cost Summary**
**File:** `page1_summary.png`

![Page 1 Screenshot](page1_summary.png)

### Key Features
- Total AWS Spend  
- Average & Maximum Daily Cost  
- Number of Active Services  
- Regions in Use  
- Production Cost %  
- Average Cost per Service  
- Cost trend over time  
- Cost distribution by Pricing Model  
- Spend by Environment (Prod, Staging, Development)  
- Top AWS Services by Cost  
- Spend by Region  
- Spend by Usage Type  

---

## **Page 2 - Optimization Insights**
**File:** `page2_insights.png`

![Page 2 Screenshot](page2_insights.png)

### Optimization KPIs
- **Estimated Savings (On-Demand → SP)**  
- Rightsizing %  
- Daily Cost Standard Deviation (StDev)  
- Optimization summary & insights  

### Deep-Dive Visuals
- Cost Drivers by Service  
- Cost Drivers by Region  
- Cost by UsageType  
- Daily anomaly detection signals  
- Cost by Tag Environment  
- Cost by Pricing Model  

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
## Cost Drivers

Largest spend comes from AWS Glue, Redshift, RDS, and EC2.

US-East-1 accounts for most total cost.

TimedStorage-GB, DataTransfer-Out, and Requests dominate usage-based charges.

OnDemand pricing contributes to approximately 72% of all spend.

## Optimization Opportunities

Converting OnDemand workloads to Savings Plans yields an estimated ~30% cost reduction.

Rightsizing analysis indicates 22% optimization potential.

Non-Production environments (Staging/Dev) show unnecessary spend and can be optimized further.

## Anomaly Detection

Several daily cost spikes exceed 2× the standard deviation above the baseline.

These may indicate one-off workloads, inefficient ETL pipelines, or unexpected data transfer activity.

## Overall Estimated Savings

~$10.9K/month in potential savings through:

~Savings Plans

~Rightsizing

~Eliminating waste in Staging/Dev

~Reducing data-transfer inefficiencies 







