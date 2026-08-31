

#   Inventory Performance Metrics: Overstock vs. Shortage

---

## Table of Contents
- <a href="#overview">Overview</a>
- <a href="#problem-statement">Problem Statement</a>
- <a href="#dataset-description">Dataset Description</a>
- <a href="#tools-technologies">Tools & Technologies</a>
- <a href="#project-architecture">Project Architecture</a>
- <a href="#data-preparation">Data Preparation</a>
- <a href="#dashboard-pages">Dashboard Pages & Visuals</a>
- <a href="#research-questions-key-findings">Research Questions & Key Findings</a>
- <a href="#final-recommendations">Final Recommendations</a>
- <a href="#author-contact">Author & Contact</a>

---

<h2><a class="anchor" id="overview"></a>Overview</h2>
An end-to-end Business Intelligence solution designed to track inventory efficiency and its direct financial impact. This project translates raw daily supply/demand data into actionable insights through two interactive Power BI dashboards.

The pipeline follows a production-grade workflow: **MySQL/PostgreSQL → Power Query → DAX → Power BI Dashboards**, with a seamless transition from a **Test Environment** to a **Production Environment** without redesigning the reports.

**Key Results Snapshot:**
- **Test Environment:** $97K Total Loss, $22K Total Profit, 579 Unit Shortages.
- **Production Environment:** $8M Total Loss, $301K Total Profit, 61K Unit Shortages.

---

<h2><a class="anchor" id="problem-statement"></a>Problem Statement</h2>
Businesses constantly face a critical trade-off between **overstocking** (which ties up capital and increases holding costs) and **understocking** (which causes lost sales and customer dissatisfaction). Without a unified view, stakeholders struggle to answer:

- How many units are we short on average per day?
- What is the actual financial cost of these inventory shortages?
- Where are we recovering losses through overstock sales?
- How do these metrics scale from test datasets to live production data?

This project solves this by creating a single source of truth that differentiates between **operational health (unit-based)** and **financial health (monetary-based)**.

---

<h2><a class="anchor" id="dataset-description"></a>Dataset Description</h2>
The analysis is built upon two core flat-file datasets, imported into a SQL environment for staging.

| Attribute | Detail |
| :--- | :--- |
| **Source** | On-premise MySQL / PostgreSQL (Test & Prod) |
| **Test Records** | ~100 rows (Inventory + 20 Products) |
| **Production Records** | ~1,200+ rows (Scaled Inventory + 22 Products) |
| **Target Metric** | Supply Shortage (`Demand` > `Availability`) |

### 1. Inventory Dataset (`Test/Prod Environment`)
| Column | Description |
| :--- | :--- |
| `Order Date (DD/MM/YYYY)` | Specific date of the inventory record. |
| `Product ID` | Foreign key referencing the product table. |
| `Availability` | Number of units physically available in stock. |
| `Demand` | Number of units requested by customers. |

### 2. Products Dataset (Dimension)
| Column | Description |
| :--- | :--- |
| `Product ID` | Primary key (IDs 1 to 20 in Test, extended to 22 in Prod). |
| `Product Name` | Descriptive name (e.g., *Wireless Mouse*, *4K Smart TV*). |
| `Unit Price ($)` | The selling price per unit used for financial calculations. |

---

<h2><a class="anchor" id="tools-technologies"></a>Tools & Technologies</h2>

| Component | Technology / Tool |
| :--- | :--- |
| **Storage & Staging** | MySQL (Test), PostgreSQL / MySQL (Production) |
| **Transformation** | SQL (Joins, Data Cleaning), Power Query (M) |
| **Semantic Model** | DAX (Calculated Columns & Measures) |
| **Visualization** | Microsoft Power BI Desktop / Service |
| **Version Control** | Git & GitHub |
| **Deployment** | Switched Data Source Settings (Test → Prod) seamlessly |

---

<h2><a class="anchor" id="project-architecture"></a>Project Architecture</h2>

1. **Raw CSVs** – Uploaded to SQL Server (Test & Prod environments).
2. **SQL Staging** – Data quality checks, type validations, and `LEFT JOIN` to combine Inventory with Products.
3. **Power BI (Import Mode)** – Connected to SQL tables (Test first, then switched to Prod).
4. **Power Query** – Data type validation, ensuring `Order_Date` is correctly parsed.
5. **DAX** – Created calculated columns (`Profit/Loss`) and performance-tuned measures.
6. **Dashboard** – Two interactive pages published (Operational & Financial).
7. **Environment Switch** – Updated *Data Source Settings* to point from Test DB to Production DB, fully scaling the report.

---

<h2><a class="anchor" id="data-preparation"></a>Data Preparation</h2>

### ✅ SQL Staging (Test & Production)
The raw CSV files were imported into the database. After rigorous data quality checks (checking for nulls, duplicates, and invalid dates), the following `LEFT JOIN` was executed to combine the fact table with the product dimension:

```sql
CREATE TABLE new_table AS
SELECT
    a.`Order Date (DD/MM/YYYY)` AS Order_Date_DD_MM_YYYY,
    a.`Product ID` AS product_id,
    a.availability,
    a.demand,
    b.`Product Name` AS product_name,
    b.`Unit Price ($)` AS unit_price
FROM
    prod.`prod+env+inventory+dataset` AS a
LEFT JOIN
    prod.`products` AS b
ON
    a.`Product ID` = b.`Product ID`;
```

### ✅ Feature Engineering (Calculated Column) in Power BI

Once the data was loaded, a crucial calculated column was created to translate unit differences into monetary impact:

```dax
Profit/Loss = (availability - demand) * unit_price
```

### ✅ Data Modeling & Key DAX Measures

All measures are optimized for correct filter context. Below are the core DAX formulas implemented in the model.

**Snapshot of some key DAX Measures**

<img width="1156" height="50" alt="Image" src="https://github.com/user-attachments/assets/d22a7417-d86d-4f64-8031-7db9151217cf" />

---

<img width="1165" height="51" alt="Image" src="https://github.com/user-attachments/assets/fc9e1f62-0561-40b1-ba3f-271eeedc1326" />

---

<h2><a class="anchor" id="dashboard-pages"></a>Dashboard Pages & Visuals</h2>


The report is structured into **two focused analytical pages**, designed to separate operational metrics from financial outcomes.

### 1. 📦 Page 1: Operational Health (Unit Metrics)
**This are production environment dashboards**

---

<img width="1321" height="786" alt="Image" src="https://github.com/user-attachments/assets/c8ac9c97-123f-46c0-8959-7dd58c8c7e29" />

---

**🔑 Key Takeaway:**

Across both environments, **Demand consistently exceeds Availability**. Production shows a significant gap, with:

- **Average Demand:** 48.65 units/day
- **Average Availability:** 24.70 units/day


---

### 2. 💰 Page 2: Financial Health (Monetary Metrics)

---

<img width="1321" height="793" alt="Image" src="https://github.com/user-attachments/assets/99b381a8-bdfa-4e5d-94a9-092bfefb2321" />

---
**🔑 Key Takeaway:**

In Production, **Total Loss ($8M) drastically outweighs Total Profit ($301K)**, indicating a profit-to-loss ratio of approximately **1:26**.


---

### 3. 🔄 Test vs. Production Scaling (Comparative Insight)

The dashboard also provides a comparative view of how key operational metrics changed as the business scaled from **Test to Production**.

**Key Metrics:**

| Metric | Test | Production | Growth |
|---|---:|---:|---:|
| Average Daily Demand | 3.40 | 48.65 | **14.3×** |
| Average Daily Availability | 2.87 | 24.70 | **8.6×** |

---
**Test environment Dashboards**

---

<img width="1321" height="795" alt="Image" src="https://github.com/user-attachments/assets/fc651ec3-fee8-4951-a43b-aae19b3e22a5" />

--

<img width="1327" height="797" alt="Image" src="https://github.com/user-attachments/assets/9c54a403-d59a-41db-ba88-e29ddf117131" />

---

**🔑 Key Takeaway:**

As the business scaled from **Test to Production**, average daily demand increased by approximately **14×**, while availability increased by only **8.6×**.

This imbalance resulted in a **worsening supply shortage gap**, highlighting the need for improved supply planning and inventory management as demand scales.

---

<h2><a class="anchor" id="research-questions-key-findings"></a>Research Questions & Key Findings</h2>


### Q1: How severe is the supply-demand gap in Production?

**Finding:**  
The gap is severe. Average daily demand (**48.65 units**) outpaces average daily availability (**24.70 units**) by nearly **24 units per day**, resulting in a cumulative shortage of approximately **61K units**.

**💡 Insight:**  
Supply chain velocity has not kept pace with customer demand growth, creating a significant and persistent supply shortage in the Production environment.

---

### Q2: What is the financial cost of these shortages?

**Finding:**  
For every unit of shortage, the weighted average loss is approximately **$131**. Total Loss reached a staggering **$8 Million** in the Production dataset.

**💡 Insight:**  
High-value electronic products, such as **VR Headsets and 4K TVs**, being understocked drive a significant portion of the financial losses.

---

### Q3: Does overstocking compensate for the losses?

**Finding:**  
No. **Total Profit ($301K)** is substantially lower than **Total Loss ($8M)**, resulting in a detrimental **1:26 profit-to-loss ratio**.

**💡 Insight:**  
The profit generated from selling excess low-cost inventory cannot offset the revenue lost from failing to meet demand for high-value products.

---

### Q4: How reliable is the scaling from Test to Production?

**Finding:**  
The migration was seamless. By switching the data source connection in Power BI, the same measures and visualizations populated correctly with Production data.

**💡 Insight:**  
This demonstrates the robustness and scalability of the underlying **SQL queries and DAX logic**, allowing the analytical framework to transition from the Test environment to Production without requiring changes to the core calculations or dashboard design.

---

<h2><a class="anchor" id="final-recommendations"></a>Final Recommendations</h2>


Based on the analysis, I recommend the following business actions:

1. **Prioritize High-Value Products:**  
   Investigate stock levels for products with the highest unit prices, such as **4K Smart TV and VR Headset**. These products contribute significantly to the **$8M loss**, so securing their supply should be a top priority.

2. **Implement Dynamic Replenishment:**  
   Move from static safety stock levels to dynamic inventory buffers. With average Production demand of around **48 units/day**, consider setting replenishment triggers when stock falls below **50 units**.

3. **Automate Alerts:**  
   Set up Power BI Data Alerts when **Total Supply Shortage** crosses a critical threshold, such as **1,000 units in a single day**, to support timely procurement decisions.

4. **Strengthen Data Governance:**  
   Maintain a proper master product list in the Production SQL database containing all active Product IDs, including new additions such as **21 and 22**, to prevent NULL price errors in future imports.

5. **Re-evaluate Overstock Strategy:**  
   Analyze why low-cost products are consistently overstocked. If these products are contributing to the **$301K profit**, consider reducing bulk orders to free up warehouse space and capital for high-demand products.


---


<h2><a class="anchor" id="author--contact"></a>Author & Contact</h2>


  - **Ansh Bodele**
  - Data Analyst
  - Email: anshbodele517@gmail.com
  - [LinkedIn](https://www.linkedin.com/in/ansh-bodele-897b5a31a/)
  - [Portfolio](https://github.com/anshbodele?tab=repositories)
