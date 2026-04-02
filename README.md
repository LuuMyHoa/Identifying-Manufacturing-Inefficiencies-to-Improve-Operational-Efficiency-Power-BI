# Identifying Manufacturing Inefficiencies to Improve Operational Efficiency | Power BI

![banner](PICTURE/banner.png)

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

- **Quality issues:**  Scrap quantity has increased significantly, indicating rework and overload in the production process.

🎯 The goal of this analysis is to identify the root causes behind these issues and provide actionable, data-driven insights to improve operational efficiency.

- Monitor manufacturing performance through key KPIs  

- Diagnose production delays across Work Orders

- Detect bottlenecks and idle time within routing steps

- Analyze scrap trends and identify high-risk products  

- Provide data-driven recommendations to improve planning and execution

### 👤 Who is this project for?  

- Production Directors & CEOs

- Operations Managers & Production Planners

- Data Analysts in the manufacturing domain

## 📂 Dataset Description & Data Structure  

### Data Source  
- Source: AdventureWorks2019 (BigQuery)
- Size: 71,591 rows in Work Order table and 67,131 rows in Work Order Routing table

### Data Structure 
- Database Structure: Online Transaction Processing (OLTP) database, showcasing a real-world relational database structure.
- Full dataset information in [data dictionary](AdventureWorks Data Dictionary.pdf).
- Tables: This project uses 7 tables from the Production schema.

| Table Name                     | Description |
|--------------------------------|-------------|
| Production.Product             | Contains master data for all products manufactured or sold by the company |
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
- WO On-time Rate (~67 % in 2013) is below target (70%) and is decreasing (~4.9% YoY)
- The average Work Order actual duration is higher than planned (~2.4 days). The planned duration is fixed at 11 days.
- Scrap Rate is still below target (~0.29% in 2013) but increasing (~26.7% YoY)
- Production Quantity and Work Orders are increasing (~46.4% and ~54.6% YoY)
  
&nbsp; **Insight**: The factory is producing more, but performance is getting worse → This indicates that production demand is exceeding system capacity, leading to performance degradation.

2. Monthly Trends of Work Orders, On-time Rate, and Production Quantity in 2013
- February has the lowest Work Orders (1,470) and Production Quantity (10,692)
- However, it has the highest On-time Rate (~71%)
  
 &nbsp; **Insight**: When workload is low, performance improves → Confirms that high volume is hurting delivery performance

3. Work Order status distribution: 
- On-time rate (~67.3%) includes both Early and On time orders (Due Date >= End Date)
- A large portion (~32.7%) of Work Orders are Overdue: ~18.1% late by 1–7 days and ~14.6% late by 7+ days
  
&nbsp; **Insight**: Delivery performance is not stable → Many orders cannot meet the planned schedule

4. Planning issue
- The planned duration is fixed at 11 days for all products
  
&nbsp; **Insight**: This is unrealistic because different products have different complexity → Poor planning is a root cause of delays

#### II. Delivery Performance
![dashboard_page2](PICTURE/dashboard_page2.png)

📌 Key Insights:   

1. Delays only happen in Work Orders with routing
- Two types of Work : WO with Routing & WO no Routing
- Work Orders with routing create delays, and account for a higher proportion (~61.5%)
- Work Orders without routing are consistently completed early, account for a smaller proportion (~38.5%)
  
&nbsp; **Insight**: The higher WO with routing rate, the higher WO Delay rate.
  
2. Monthly delivery performance
- Months with high volume (from Jun to Dec) → more late orders
- On-time Rate is declining over time in 2013 (from ~68.9% in Jan to ~66.1% in Dec)

&nbsp; **Insight**: This is not a one-time issue → It is a consistent and structural problem
  
3. Volume vs On-time relationship
- Work Orders are increasing ~54.6% YoY
- On-time Rate is decreasing ~4.9% YoY
- Both show opposite trends every month
  
&nbsp; **Insight**: The increasing Work Order volume puts pressure on delivery performance

4. Product & Subcategory performance
- Subcategory Touring Frames has WO On-time rate 100%
- Some products have a delay rate of 100%
  
&nbsp; **Insight**: Performance is not equal across products → Need to focus on high-risk products

#### III. Operation Efficiency
![dashboard_page3](PICTURE/dashboard_page3.png)

📌 Key Insights:   
1. Operation-level performance
- Work Orders with routing involve multiple operational steps
- There are 7 operations across 7 locations
- Step 6 has the highest number of Work Orders
- Operation On-time Rate is low (~42% in 2013) and lowest (~38.3%) in Operation 4, with no significant gap between the max and min.
  
&nbsp; **Insight**: The delays are not only at Work Order level → They occur within internal process steps (operation level)

2. Bottleneck identification
- Step 6 has the highest workload (12,514/17,788 WOs ~70%) and low performance (delay ~43.1% and ~5.7 days)
  
&nbsp; **Insight**: Step 6 is the main bottleneck of the system

3. Complexity effect (Steps per WO)
- There are 4 type of WO with routing : 1/2/3/6 steps
- 6-step WOs accounts for the smallest proportion (~4%), but have the lowest On-time Rate (~39%) in all steps
- 1-step WOs accounts for largest volume (~66%), still have relatively low On-time Rate (~41.9%)
  
&nbsp; **Insight**: System is overloaded, not just complex Work Orders.

4. Operation trend in 2013
- Avg Operation Delay is quite stable (min ~4.9 days in January, max ~6.6 days in March, avg ~5.6 days)
- Operation On-time Rate is very low (min ~30.4% in Mar, max ~49.6% in Feb, avg ~42%)

&nbsp; **Insight**: The system is consistently inefficient, not improving over time

#### IV. Scrap Analysis
![dashboard_page4](PICTURE/dashboard_page4.png)

📌 Key Insights:   
1. Scrap vs Production growth in 2013
- Scrap Quantity increased ~85.6% YoY
- Production Quantity increased ~46.4% YoY
- Scrap Rate increased ~26.7%
  
&nbsp; **Insight**: Scrap is growing faster than production → Quality is getting worse. Higher scrap rates may contribute to production delays, as scrap items require rework, further increasing system load

2. Monthly pattern
- Scrap is highest in September (Scrap Quantity 1,319 and Scrap Rate ~1%)
- Production volume (135,942 units) is not highest in September (max 235,037 in August)
  
&nbsp; **Insight**: This peak is not fully explained by production volume → There may be process or quality issues

3. Scrap by Work Order type
- WO without routing accounts for ~68.4% of scrap
- WO without routing are completed early but have high scrap
  
&nbsp; **Insight**: This suggests a trade-off between speed and quality, WO without routing may lack sufficient quality control.

4. Scrap Reason: Pareto Chart or Table
- A small number of reasons contribute to most scrap
- Top causes: Trim length too long, drill pattern incorrect, and other factors
  
&nbsp; **Insight**: Focus on top causes → Apply 80/20 rule to improve quality faster

5. Product-level scrap
- High scrap comes from Unclassified Products
  
&nbsp; **Insight**: Possible data issue or poor product classification → Need data cleaning or better categorization

#### V. Work Order Detail
![dashboard_page5](PICTURE/dashboard_page5.png)

![dashboard_page6](PICTURE/dashboard_page6.png)

## 🔎 Final Conclusion & Recommendations 

The analysis shows that the factory is facing a structural performance problem, not a temporary issue.

Despite increasing production volume, both delivery performance and product quality are getting worse.

| **Problem**                | **Impact**                          | **Priority**        | **Recommendations**                     |
| ------------------------ | ------------------------------ | -------------------- | ------------------------------------|
| Capacity overload (Too many Work Orders)     | On-time Rate drops as volume increases → system becomes unstable under peak load |  High          | - Implement capacity-based planning (cap WOs per period) <br> - Introduce order prioritization logic (urgent / high-margin first) <br> - Align sales forecast with production capacity |
| Fixed planning duration (11 days for all WOs) | Unrealistic schedule → systematic delays across almost all orders                |  High | - Replace fixed duration with dynamic estimation model (based on product, routing steps) <br> - Use historical lead time data to improve accuracy     |
| High WOs with routing      | Multi-step WOs are more delays → reduce overall On-time Rate       |  High                 | - Simplify routing by removing non-value-added steps <br> - Modularize production (split large WOs) <br> - Standardize best-performing routing patterns     |
| Bottleneck at Step 6 (Subassembly)  | Congestion point → delays propagate across entire production flow         |  Critical        | - Increase capacity (machine / labor / shift) at Step 6 <br> - Rebalance workload upstream/downstream <br> - Track queue time before Step 6 (key hidden KPI)      |
| Low operation efficiency (across steps)      | Persistent inefficiency → system fails to improve over time                      |  Medium              | - Track and build operation-level KPI (cycle time, wait time) <br> - Optimize handoff between steps<br> - Reduce idle time (focus on waiting, not processing) |
| Increasing Scrap Rate | Higher cost + rework → impacts both margin and delivery       |  Medium            | - Apply Pareto analysis on scrap reasons <br> - Shift quality checks earlier in process <br> - Improve operator training for high-error steps  |
| High scrap in no-routing WOs                  | Faster production but poor quality → inefficient trade-off                       |  Medium               | - Define minimum quality standards even for simple WOs <br> - Introduce lightweight QC checkpoints  |
| Data issue (Unclassified Products)           | Reduces analytical accuracy and may lead to misleading insights → affects decision-making quality                    | Quick Win | - Perform one-time data cleanup (manual + rule-based mapping) <br> - Establish data governance process to prevent recurrence        |
