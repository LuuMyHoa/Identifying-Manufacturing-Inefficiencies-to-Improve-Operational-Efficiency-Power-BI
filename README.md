# Identifying Manufacturing Inefficiencies to Improve Operational Efficiency | Power BI

![banner](.png)

## Table of Contents  
1. [📌 Background & Overview](#-background--overview)  
2. [📂 Dataset Description & Data Structure](#-dataset-description--data-structure)  
3. [🧠 Design Thinking Process](#-design-thinking-process)  
4. [💡 Key Insights & Visualizations](#-key-insights--visualizations)  
5. [🔎 Final Conclusion & Recommendations](#-final-conclusion--recommendations)

## 📌 Background & Overview  

### What is this project about? 
This project analyzes manufacturing performance in a bicycle production company using Power BI.

🔥 The business is currently facing two major challenges:

- **Production delays:**  The Work Order On-time Rate has been declining over time, while actual production duration consistently exceeds planned schedules.

- **Quality issues:**  Scrap quantity has increased significantly, indicating rework and overload in production process.

🎯 The goal of this analysis is to identify the root causes behind these issues and provide actionable insights to improve operational efficiency.

- Monitor manufacturing performance using key KPIs  

- Diagnose production delays across Work Orders

- Detect bottlenecks and idle time in routing steps

- Analyze scrap trends and detect high-risk products  

- Provide data-driven recommendations to improve planning and execution

### 👤 Who is this project for?  

- Production Directors & CEO 

- Operations Managers & Planners

- Data Analysts in Manufacturing domain

## 📂 Dataset Description & Data Structure  

### Data Source  
- Source: adventureworks2019 in BigQuery
- Size: 71591 rows in Work Order table and 67131 rows in Work Order Routing table

### Data Structure 
- Database Structure: Online Transaction Processing (OLTP) database, showcasing a real-world relational database structure.

- Tables: My project uses 7 tables in Production. Full infomation in data dictionary.

| Table Name                     | Description |
|--------------------------------|-------------|
| Production.Product             | Contains master data for all products manufactured or sold by the company, including product name, color,... |
| Production.ProductCategory     | Defines high-level product categories (e.g., Bikes, Components). |
| Production.ProductSubcategory  | Defines subcategories within each product category (e.g., Mountain Bikes, Road Bikes). |
| Production.WorkOrder           | Records manufacturing orders, including order quantity, start and end dates, and scrapped quantity. |
| Production.WorkOrderRouting    | Details the steps (operations) required for each work order, including location, scheduled hours, and actual costs. |
| Production.Location            | Represents manufacturing and storage locations within the facility. |
| Production.ScrapReason         | Defines the reasons for scrapped items during production. |

### Data Relationships

![Data Modeling](PICTURE/modeling.png)

## 🧠 Design Thinking Process  

1️⃣ Empathize  
2️⃣ Define point of view  
3️⃣ Ideate  
4️⃣ Prototype and review  
<details>
<summary>Click to toggle</summary>
🧠 
</details>

## 💡 Key Insights & Visualizations  

#### I. Production Overview
![dashboard_page1](PICTURE/dashboard_page1.png)

📌 Key Insights:   

1. Overall KPIs show a capacity problem  
- WO On-time Rate is below target (70%) and is decreasing vs LY 2012
- Avg WO Actual Duration is higher planned (11 days fixed)
- Scarp Rate is still below target (0.29% vs 2%) but increasing vs LY 2012
- Production Quantity and Work Orders is increasing
  
👉 Insight: The factory is producing more, but performance is getting worse → This shows a capacity overload problem.

2. Work Orders, WO On-time Rate, Production Quantity Trend | monthly in 2013
- February has the lowest Work Orders and Production Quantity
- But it has the highest On-time Rate
  
👉 Insight: When workload is low, performance improves → Confirms that high volume is hurting delivery performance

3. Work Order status distribution: Due Date and End Date
- On-time rate includes both Early and On time orders
- A large portion (%) of Work Orders are Late or Overdue
  
👉 Insight: Delivery performance is not stable → Many orders cannot meet the planned schedule

4. Planning issue
- Planned Duration is always fixed at 11 days for all products
  
👉 Insight: This is unrealistic because different products have different complexity → Poor planning is a root cause of delays

#### II. Delivery Performance
![dashboard_page2](PICTURE/dashboard_page2.png)

📌 Key Insights:   

1. Delays only happen in Work Orders with routing
- 2 Type Work Order: WO with Routing & WO no Routing
- WO with Routing create delays, and account for higher (%)
- WO no Routing are always completed early, account for smaller (%)
  
👉 Insight: The higher WO with routing rate, the higher WO Delay rate.
  
2. Monthly delivery performance
- Months with high volume → more Late & Overdue orders
- On-time Rate is declining over time

👉 Insight: This is not a one-time issue → It is a consistent and structural problem
  
3. Volume vs On-time relationship
- Work Orders are increasing YoY
- On-time Rate is decreasing YoY
- Both show opposite trends every month
  
👉 Insight: The rising WO volume pressure delivery.

4. Product & Subcategory performance
- Subcategory Touring Frames has WO Ontime rate 100%
- Some products have delays rate 100%
  
👉 Insight: Performance is not equal across products → Need to focus on high-risk products

#### III. Operation Efficiency
![dashboard_page3](PICTURE/dashboard_page3.png)

📌 Key Insights:   
1. Operation-level performance
- WO with routing has Operation Level.
- There are 7 Operation (Step) in 7 Location
- Step 6 has the highest number of Work Orders
- Operation Ontime Rate is low and lowest in Operation 4, but not a big gap between max min ()
  
👉 Insight:
The delays is not only at Work Order level → It happens inside the process (operation level)

2. Bottleneck identification
- Step 6 has: Highest workload and Lowest performance
  
👉 Insight: Step 6 is the main bottleneck of the system

3. Complexity effect (Steps per WO)
- There are 4 Type of WO with routing : 1/2/3/6 steps
- 6-step WOs accounts for the smallest with %, but have the lowest On-time Rate in all steps
- 1-step WOs accounts for largest volume (~66%), still have relatively low On-time Rate
  
👉 Insight: System is overloaded, not just complex WOs

4. Operation trend
- Avg Operation Delay is quite stable
-  Operation On-time Rate is very low

👉 Insight: The system is consistently inefficient, not improving over time

#### IV. Scrap Analysis
![dashboard_page4](PICTURE/dashboard_page4.png)

📌 Key Insights:   
1. Scrap vs Production growth in 2013
- Scrap Quantity increased 85.55% YoY
- Production Quantity inscreased 46.43% YoY
- Scrap Rate inscreased 26.72%
  
👉 Insight: Scrap is growing faster than production → Quality is getting worse

2. Monthly pattern
- Scrap is highest in September (Scrap Quantity and Scrap Rate )
- Production volume in September
  
👉 Insight: This peak is not fully explained by production volume → There may be process or quality issues

3. Scrap by Work Order type
- WO without Routing accounts for 68.44% of Scrap
- These WOs are completed early but have high scrap
  
👉 Insight: Fast production does not mean good quality → Speed vs Quality trade-off exists

. Scarp Reason: Pereto Chart or Table
- A small number of reasons contribute to most scrap
  
👉 Insight: Focus on top causes → Apply 80/20 rule to improve quality faster

5. Product-level scrap
- High scrap comes from Unclassified Products
  
👉 Insight: Possible data issue or poor product classification → Need data cleaning or better categorization

#### V. Work Order Detail
![dashboard_page5](PICTURE/dashboard_page5.png)

![dashboard_page6](PICTURE/dashboard_page6.png)

## 🔎 Final Conclusion & Recommendations 

The analysis shows that the factory is facing a structural performance problem, not a temporary issue.

Despite increasing production volume, both delivery performance and product quality are getting worse.

| **Problem**                                       | **Impact**                                                                       | **Priority**                | **Recommendations **                                                                                                                                                  |
| ------------------------------------------------- | -------------------------------------------------------------------------------- | --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Capacity overload (Too many Work Orders)     | On-time Rate drops as volume increases → system becomes unstable under peak load | 🔴 High          | - Implement capacity-based planning (cap WOs per period) <br> - Introduce order prioritization logic (urgent / high-margin first) <br> - Align sales forecast with production capacity |
| Fixed planning duration (11 days for all WOs) | Unrealistic schedule → systematic delays across almost all orders                | 🔴 High              | - Replace fixed duration with dynamic estimation model (based on product, routing steps) <br> - Use historical lead time data to improve accuracy                                      |
| High WOs with routing      | Multi-step WOs are more delays → reduce overall On-time Rate                   | 🔴 High                 | - Simplify routing by removing non-value-added steps <br> - Modularize production (split large WOs) <br> - Standardize best-performing routing patterns                         |
| Bottleneck at Step 6 (Subassembly)            | Congestion point → delays propagate across entire production flow                | 🔴 Critical        | - Increase capacity (machine / labor / shift) at Step 6 <br> - Rebalance workload upstream/downstream <br> - Track queue time before Step 6 (key hidden KPI)                           |
| Low operation efficiency (across steps)      | Persistent inefficiency → system fails to improve over time                      | 🟠 Medium              | - Track and build operation-level KPI (cycle time, wait time) <br> - Optimize handoff between steps<br> - Reduce idle time (focus on waiting, not processing)                         |
| Increasing Scrap Rate                         | Higher cost + rework → impacts both margin and delivery                          | 🟠 Medium            | - Apply Pareto analysis on scrap reasons <br> - Shift quality checks earlier in process <br> - Improve operator training for high-error steps                                          |
| High scrap in no-routing WOs                  | Faster production but poor quality → inefficient trade-off                       | 🟡 Medium               | - Define minimum quality standards even for simple WOs <br> - Introduce lightweight QC checkpoints                                                                                     |
| Data issue (Unclassified Products)           | Reduces analytical accuracy → affects decision-making quality                    | 🟢 Quick Win | - Perform one-time data cleanup (manual + rule-based mapping) <br> - Establish data governance process to prevent recurrence                                                           |



