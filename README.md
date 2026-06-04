<img width="1159" height="654" alt="Overview Dashboard" src="https://github.com/user-attachments/assets/89494748-4eeb-4b80-a359-683bd37a0c29" /># PPSHV Expressway Data Analytics & Monitoring System

## Project Overview

This project analyzes Cambodia's **PPSHV Expressway** toll transaction data for 2023 using Power BI Desktop. The dashboard transforms **4.91 million** raw transaction records into actionable business insights across four analytical areas:

- Executive Overview
- Traffic & Operations Analysis
- Data Quality Monitoring
- Revenue Analysis

> **Dataset:** PPSHV Expressway Open Data — Cambodia 2023  
> **Tool:** Power BI Desktop  
> **Records:** 4,910,002 Transactions  
> **Stations:** 8 Toll Stations

---

# Dashboard Preview

## Executive Overview

![Executive Overview](Dashboards/Overview%20Dashboard.png)

## Traffic & Operations

![Traffic & Operations](Dashboards/Traffic%20%26%20Operations.png)

## Data Quality Monitor

![Data Quality Monitor](Dashboards/Data%20Quality.png)

## Revenue Analysis

![Revenue Analysis](Dashboards/Revenue%20Analysis.png)

---

## Business Objectives

This dashboard answers several key business questions:

- How much revenue does the expressway generate?
- Which stations contribute the most revenue?
- When does peak traffic occur?
- What are the average travel times across routes?
- Which stations experience the most system errors?
- How reliable is the license plate recognition system?

---

## Dashboard Pages

| Page | Purpose |
|--------|----------|
| Executive Overview | High-level KPI summary for management |
| Traffic & Operations | Traffic patterns and operational performance |
| Data Quality Monitor | Error tracking and data quality assessment |
| Revenue Analysis | Revenue breakdown and profitability insights |

---

## Key Findings

### Revenue Concentration

- Total Revenue reached **$37.29M**
- Phnom Penh Station generated **$16.02M**
- Phnom Penh and Sihanoukville stations contributed approximately **77%** of total network revenue

### Peak Traffic Period

- Total Trips: **4.91M**
- Peak traffic occurs at **15:00 (3 PM)**
- The busiest hours are:
  - 14:00
  - 15:00
  - 16:00

This suggests the expressway primarily supports intercity travel and logistics rather than traditional commuting patterns.

### Data Quality Monitoring

- Error Rate: **1.05%**
- Total Error Transactions: **51,796**
- Plate Not Found Rate: **0.29%**

Several high-volume stations exhibit higher error rates, creating operational and revenue risks.

---

## Recommendations

### Operations

- Increase staffing between **13:00–17:00**
- Ensure all toll gates remain operational during peak traffic periods

### Maintenance

- Prioritize camera inspections at stations with high error rates
- Reduce error rate below **0.5%**

### Monitoring

- Implement automated alerts when station error rates exceed **2%**

---

## Data Model

The dashboard follows a **Star Schema** design.

```text
          Date_Table
               |
               |
               *
PPSHV_2023_Datasets (Fact Table)
      /      |      \
     /       |       \
 Stations   Gates   Vehicle Data
```

### Fact Table

#### PPSHV_2023_Datasets

Contains:

- Toll Amount
- Entry DateTime
- Exit DateTime
- Entry Station
- Exit Station
- Entry Gate
- Exit Gate
- Vehicle Type
- Error Indicators
- Speeding Indicators

### Dimension Tables

#### Date_Table

- Date
- Month
- Quarter
- Year

#### PPSHV_STATIONS

- Station Information

#### PPSHV_GATES

- Gate Information

---

## Data Preparation

### Power Query Transformations

1. Converted DateTime fields
2. Converted revenue fields to numeric format
3. Filtered records to 2023 only
4. Created Date-only field for relationships
5. Replaced missing vehicle types
6. Cleaned station and gate data

---

## Key DAX Measures

```dax
Total Revenue =
SUM(PPSHV_2023_Datasets[AMOUNT])

Total Trips =
COUNTROWS(PPSHV_2023_Datasets)

Revenue Per Trip =
DIVIDE([Total Revenue], [Total Trips])

Error Rate =
DIVIDE(
    COUNTROWS(
        FILTER(
            PPSHV_2023_Datasets,
            PPSHV_2023_Datasets[IS_WRONG_FORMAT] = 1
        )
    ),
    COUNTROWS(PPSHV_2023_Datasets)
)

Plate Not Found Rate =
DIVIDE(
    COUNTROWS(
        FILTER(
            PPSHV_2023_Datasets,
            PPSHV_2023_Datasets[IS_PLATE_NOT_FOUND] = 1
        )
    ),
    COUNTROWS(PPSHV_2023_Datasets)
)
```

---

## Dashboard Features

### Executive Overview

- Revenue KPIs
- Traffic KPIs
- Monthly Revenue Trend
- Revenue by Station
- Revenue by Vehicle Type

### Traffic & Operations

- Peak Hour Analysis
- Trips by Hour
- Travel Time by Route
- Station Traffic Distribution

### Data Quality Monitor

- Error Tracking
- Plate Recognition Monitoring
- Station Quality Comparison
- Quality Summary Table

### Revenue Analysis

- Revenue Trends
- Revenue by Station
- Revenue by Vehicle Type
- Revenue Efficiency Metrics

---

## Technologies Used

- Power BI Desktop
- Power Query
- DAX
- Data Modeling
- Data Visualization
- Business Intelligence

---

## Repository Structure

```text
PPSHV-PowerBI-Dashboard/
│
├── dashboard/
│   └── PPSHV_Dashboard.pbix
│
├── Dashboard_Screenshots/
│   ├── Overview Dashboard.png
│   ├── Traffic & Operations.png
│   ├── Data Quality.png
│   └── Revenue Analysis.png
│
├── data/
│   ├── PPSHV_2023_Datasets.csv
│   ├── PPSHV_STATIONS.csv
│   └── PPSHV_GATES.csv
│
└── README.md
```

---

## How to Open

1. Install Power BI Desktop
2. Clone the repository

```bash
git clone https://github.com/LizaSROY/PPSHV Cambodia Expressway Data Analytics and Monitoring System.git
```

3. Open:

```text
dashboard/PPSHV_Dashboard.pbix
```

4. Refresh data sources if required

---

## Skills Demonstrated

- Data Cleaning
- Data Transformation
- Data Modeling
- Star Schema Design
- DAX Calculations
- KPI Development
- Dashboard Design
- Business Analysis
- Data Quality Monitoring
- Performance Analytics

---

## Author

**Sini Jakava**

Computer Science Student  
Institute of Technology of Cambodia (ITC)

### Interests

- Data Analytics
- Business Intelligence
- Machine Learning
- Full-Stack Development

---

## License

This project uses PPSHV Expressway open data for educational and portfolio purposes only.

---

**Built with Power BI Desktop • Cambodia Open Data • 4.91M Records**
