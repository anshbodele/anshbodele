

# 📊 Loan Default Risk Analysis – Power BI Dashboard

---

## Table of Contents
- <a href="#overview">Overview</a>
- <a href="#problem-statement">Problem Statement</a>
- <a href="#dataset-description">Dataset Description</a>
- <a href="#tools-technologies">Tools & Technologies</a>
- <a href="#project-structure">Project Architecture</a>
- <a href="#data-preparation">Data Preparation</a>
- <a href="#dashboard-pages">Dashboard Pages & Visuals</a>
- <a href="#research-questions-key-findings">Research Questions & Key Findings</a>
- <a href="#final-recommendations">Final Recommendations</a>
- <a href="#author-contact">Author & Contact</a>

---

<h2><a class="anchor" id="overview"></a>Overview</h2>
An end-to-end BI solution that analyzes loan default risk using a production-grade pipeline:  
**SQL Server → Power BI Dataflow → Power BI Desktop → Power BI Service** with automated daily refresh.

---

<h2><a class="anchor" id="problem-statement"></a>Problem Statement</h2>
Lenders need to identify high-risk borrowers and monitor portfolio health. This project answers:

- Which borrower segments (employment, age, credit score) default the most?
- What factors influence loan amounts and repayment behavior?
- How does portfolio risk evolve year-over-year?

---

<h2><a class="anchor" id="dataset-description"></a>Dataset Description</h2>

| Attribute | Detail |
| :--- | :--- |
| **Source** | On-premise SQL Server |
| **Records** | 10,000+ (scaled in production) |
| **Target** | `Default` (0 = Repaid, 1 = Defaulted) |
| **Key Columns** | • `Age` · `Income` · `LoanAmount` · `CreditScore` <br/> • `EmploymentType` · `DTIRatio` · `LoanPurpose` <br/> • `HasCoSigner` · `Loan Date` |
> Full column definitions are available in `Column_Definitions.xlsx`.

---

<h2><a class="anchor" id="tools-technologies"></a>Tools & Technologies</h2>

| Component | Technology / Tool |
| :--- | :--- |
| **Storage** | Microsoft SQL Server |
| **Integration** | Power BI Dataflow (Gen1) + Standard Gateway |
| **Transformation** | Power Query (M) |
| **Modeling** | DAX |
| **Visualization** | Power BI Desktop / Service |
| **Automation** | Scheduled Refresh |
---

<h2><a class="anchor" id="project-architecture"></a>Project Architecture</h2>

1. **SQL Server** – Raw data.
2. **Standard Gateway** – Secure connection from on-prem SQL to cloud.
3. **Dataflow (Gen1)** – Ingests SQL tables into Power BI cloud storage.
4. **Power BI Desktop** – Connects to Dataflow (Import Mode).
5. **Power Query** – Data cleaning, type validation, feature creation.
6. **DAX** – Calculated columns & measures for dynamic analysis.
7. **Dashboard** – 3 interactive pages published to Service.
8. **Scheduled Refresh** – Dataflow refreshes at 6:00 AM, Report at 6:30 AM.

---

<h2><a class="anchor" id="data-preparation"></a>Data Preparation</h2>

### ✅ Data Type Validation
Set correct types: `LoanAmount` (Decimal), `CreditScore` (Whole Number), `Default` (Whole Number), categorical flags (Text).

### ✅ Feature Engineering (Calculated Columns)

#### Column

- **Age Groups**  
  Teen (≤19) / Adults (20–39) / Middle Age Adults (40–59) / Senior Citizens (≥60)

- **Credit Score Bins**  
  Very Low (≤400) / Low (401–450) / Medium (451–650) / High (>650)

- **Year**  
  Extracted from standardized date

### ✅ Data Modeling & Key DAX Measures

All measures are optimized for performance and correct filter context. Below are the final corrected DAX formulas implemented in the model.

**Snap of some key DAX Measures**

<img width="1052" height="143" alt="Image" src="https://github.com/user-attachments/assets/bd1a52a4-b8f1-4755-8d63-3a419fc80ec4" />

---

<img width="1152" height="202" alt="Image" src="https://github.com/user-attachments/assets/ba2fa5f5-589a-435c-8013-5ed2fc5439a3" />

---

<img width="465" height="72" alt="Image" src="https://github.com/user-attachments/assets/011b1f9b-b83f-4b59-bdf2-595c3558d06a" />

---

<img width="1155" height="72" alt="Image" src="https://github.com/user-attachments/assets/e353e13e-d70f-45ea-8aed-b09f19dd8b21" />

---

<img width="991" height="51" alt="Image" src="https://github.com/user-attachments/assets/25fd172a-7802-4646-bf4b-2acee3715107" />

---

<img width="1148" height="182" alt="Image" src="https://github.com/user-attachments/assets/5e863530-be8b-48bb-959c-e7dc12b7ae7a" />

---

<img width="1157" height="183" alt="Image" src="https://github.com/user-attachments/assets/880ec390-4263-49b5-b1d7-bbc600a32992" />


---


<h2><a class="anchor" id="dashboard-pages"></a>Dashboard Pages & Visuals</h2>

The report is structured into three focused analytical pages

1. **Page 1: Loan Default & Overview**:
   - **Visuals:** Loan Amount by Purpose, Average Income by Employment Type, Default Rate by Employment Type, Average Loan by Age Group, Default Rate by Year.
   - **Key Takeaway:** Overall default rate is steady at ~11.5%. Unemployed borrowers exhibit significantly higher risk.

<img width="1298" height="727" alt="Image" src="https://github.com/user-attachments/assets/00c52656-d7b1-4d45-95d0-f464db7af3bc" />

---

2. **Page 2: Applicant Demographics & Financial Profile**:
   - **Visuals:** Median Loan by Credit Score, Average Loan Amount (High Credit) cross-tab with Age/Marital Status, Total Loans by Credit Bins (Adults), Loan segmentation by Mortgage/Dependents, Loan counts by Education.
   - **Key Takeaway:** Education distribution is nearly equal (~24k each). High-credit borrowers average ~$127K loans.

<img width="1292" height="730" alt="Image" src="https://github.com/user-attachments/assets/2590f9f6-0510-4033-b713-634d19f5e6b3" />

---

3. **Page 3: Financial Risk Matrix**:
   - **Visuals:** YOY Loan Amount Change, YOY Default Change, YTD Loan Amount by Credit Score/Marital Status, Income Brackets.
   - **Key Takeaway:** 2014 and 2017 saw negative loan growth (-1.5% and -1%), while 2018 rebounded strongly (+1.7%).

<img width="1292" height="725" alt="Image" src="https://github.com/user-attachments/assets/992f8085-5718-4502-a573-2b3d92f4d980" />


---

<h2><a class="anchor" id="research-questions-key-findings"></a>Research Questions & Key Findings</h2>

  - **Q1: Which employment type poses the highest default risk?**
    Finding: Unemployed and Self-employed applicants default at significantly higher rates than Full-time employees. Financial instability is a primary risk driver.
  - **Q2: Does a higher credit score correlate with larger loan amounts?**
    Finding: Yes. Borrowers in the "High" credit score bracket take out larger average loans (~$128K) compared to "Very Low" scores ($124K), indicating lenders trust high-score individuals with more capital.
  - **Q3: Are there cyclical yearly trends in lending?**
    Finding: Year-over-year growth is volatile. 2014 and 2017 saw contractions, while 2015 and 2018 showed recovery. Default rates inversely mirror these growth patterns.
  - **Q4: How do dependents and mortgages affect borrowing for middle-aged adults?**
    Finding: Loan amounts are split almost evenly (50/50) between those with dependents/mortgages and those without, suggesting stable borrowing demand across both sub-groups.


---


<h2><a class="anchor" id="final-recommendations"></a>Final Recommendations</h2>

  - Tighten Criteria for Unemployed: Implement stricter validation (e.g., higher down payments, mandatory co-signers) for unemployed and self-employed applicants to mitigate elevated default risks.
  - Attract High-Credit Borrowers: Since this segment takes larger loans and defaults less, develop premium loan products with competitive APRs to capture this profitable market.
  - Monitor DTI Ratio Closely: Build an automated alert system for loan applications where DTIRatio exceeds 0.60, as this is a classic red flag for over-leverage.
  - Align Marketing with YOY Trends: Increase marketing spend during historically positive growth years (e.g., 2018) and tighten underwriting during contraction years (e.g., 2017).


---


<h2><a class="anchor" id="author--contact"></a>Author & Contact</h2>


  - **Ansh Bodele**
  - Data Analyst
  - Email: anshbodele517@gmail.com
  - [LinkedIn](https://www.linkedin.com/in/ansh-bodele-897b5a31a/)
  - [Portfolio](https://github.com/anshbodele?tab=repositories)
