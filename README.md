# Identifying Manufacturing Inefficiencies to Improve Operational Efficiency | Power BI

![banner](.png)

## 📑 Table of Contents  
1. [📌 Background & Overview](#-background--overview)  
2. [📂 Dataset Description & Data Structure](#-dataset-description--data-structure)  
3. [🧠 Design Thinking Process](#-design-thinking-process)  
4. [📊 Key Insights & Visualizations](#-key-insights--visualizations)  
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

![Data Modeling]()

## 🧠 Design Thinking Process  

1️⃣ Empathize  
2️⃣ Define point of view  
3️⃣ Ideate  
4️⃣ Prototype and review  
<details>
<summary>Click to toggle</summary>


</details>

## 📊 Key Insights & Visualizations  

#### Production Overview
![dashboard_page1](Project3_HoaLuu_ver3-trang-1.pdf)

📌 Analysis 1:  
- Observation: _Describe trends, key metrics, and patterns. Any insights from those observation_  
- Recommendation: _Suggest actions based on insights._  

#### Delivery Performance
![dashboard_page2](.png)

#### Operation Efficiency
![dashboard_page3](.png)


#### Scrap Analysis
![dashboard_page4](.png)
#### Work Order Detail
![dashboard_page5](.png)

![dashboard_page6](.png)

## 🔎 Final Conclusion & Recommendations  



