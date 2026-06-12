# 🚚 FedEx Logistics Optimization — SQL Analytics Project

A SQL-driven analytics project built to analyze shipment performance,
identify delivery delay patterns, and generate actionable KPI insights
across FedEx's simulated global logistics network.

---

## 📌 Project Overview

FedEx operates across 220+ countries through major hubs in Memphis,
Dubai, Singapore, Paris, and London. This project uses relational
database analysis to uncover operational inefficiencies, rank route
performance, and recommend data-driven improvements for on-time
delivery and cost efficiency.

---

## 🗃️ Dataset

5 relational tables with 1,376 total records:

| Table | Records | Description |
|---|---|---|
| Orders | 300 | Order-level delivery details |
| Routes | 20 | Source/destination cities, distance, transit time |
| Warehouses | 10 | Hub locations and daily capacity |
| Delivery Agents | 50 | Agent performance and experience data |
| Shipments | 1000 | Pickup/delivery timestamps, delay hours, status |

---

## 🛠️ Tools Used

- **MySQL** — All SQL queries and analysis
- **Power BI / Excel** — Data visualization and charts
- **PowerPoint** — Final presentation of findings

---

## 📋 Tasks Performed

### Task 1 — Data Cleaning & Preparation
- Checked and removed duplicate Order IDs and Shipment IDs
- Handled NULL values in Delay_Hours using route-level averages
- Validated date formats and flagged invalid date records
- Verified referential integrity across all 5 tables
- **Result:** Dataset was clean — 0 duplicates, 0 nulls, 0 integrity violations

### Task 2 — Delivery Delay Analysis
- Calculated delivery delay using `TIMESTAMPDIFF(HOUR, Pickup_Date, Delivery_Date)`
- Identified Top 10 most delayed routes by average delay hours
- Used `RANK()` window function with `PARTITION BY Warehouse_ID` to rank shipments
- Compared Express vs Standard delivery average delays
- **Finding:** R002 (Dubai→Shanghai) leads at 41.04h avg delay

### Task 3 — Route Optimization Insights *(20 marks)*
- Calculated actual average transit time per route from shipment data
- Computed Distance-to-Time Efficiency Ratio = `Distance_KM / Avg_Transit_Time_Hours`
- Identified 3 worst efficiency routes (R003, R015, R006)
- Found that all 20 routes exceed expected transit time benchmarks
- Generated hub optimization recommendations using CASE statements
- **Finding:** R003 (Singapore→Hong Kong) has worst ratio of 37.66 — 885km route taking 23.5hrs

### Task 4 — Warehouse Performance
- Ranked top 3 warehouses with highest average delay (Shanghai, London, Amsterdam)
- Calculated total vs delayed shipments per warehouse
- Used **CTEs** to identify warehouses exceeding global average delay of 21.41h
- Ranked all warehouses by on-time delivery percentage
- **Finding:** Best warehouse (Amsterdam) achieves only 10.7% on-time — network-wide failure

### Task 5 — Delivery Agent Performance
- Ranked agents per route using `RANK()` with `PARTITION BY Route_ID`
- Identified all agents below 85% on-time threshold — all 49 agents failed
- Compared Top 5 vs Bottom 5 agents using subqueries and `UNION ALL`
- **Finding:** Top and bottom agents have nearly identical ratings (4.42 vs 4.36) — delays are systemic, not agent-driven

### Task 6 — Shipment Tracking Analytics
- Displayed latest delivery status and date per shipment
- Checked routes where majority of shipments are stuck In Transit or Returned
- Analyzed most frequent delay reasons
- Identified 52 shipments with extreme delays exceeding 120 hours
- **Finding:** Traffic is #1 delay cause at 48.6% — biggest actionable lever

### Task 7 — Advanced KPI Reporting
- Avg Delivery Delay by Source Country using CASE severity classification
- Overall On-Time Delivery % = 6.80% (93.2% of shipments delayed)
- Avg Delay per Route with Critical / High / Moderate / Low categorization
- Warehouse Utilization % — all warehouses critically under-utilized (max 10.3%)

---

## 📊 Key Findings

| KPI | Value |
|---|---|
| Overall On-Time Delivery Rate | **6.80%** |
| Most Delayed Route | **R002 Dubai→Shanghai — 41.04h** |
| Worst Efficiency Route | **R003 Singapore→Hong Kong — Ratio 37.66** |
| #1 Delay Cause | **Traffic — 48.6% of all delays** |
| Shipments with >120h Delay | **52 shipments** |
| Max Warehouse Utilization | **10.3% (Johannesburg)** |
| Global Average Delay | **21.41 hours** |

---

## 💡 Business Recommendations

1. **Audit R003 immediately** — Singapore→Hong Kong is 885km but taking 23.5hrs. Add direct air link and fix ground handling.
2. **Address UAE and China corridors** — Both are Critical severity. Pre-clearance customs agreements needed.
3. **Target traffic-based delays** — 48.6% of delays are traffic-related. Implement dynamic routing.
4. **Update transit benchmarks** — All 20 routes exceed expected transit times. Recalibrate using rolling 90-day actuals.
5. **Consolidate warehouses** — Max utilization is 10.3%. Current capacity is massively oversized for shipment volumes.
6. **Do not blame agents** — Top vs bottom performers are statistically identical. Fix routes, not people.

---

## 📁 Repository Structure
