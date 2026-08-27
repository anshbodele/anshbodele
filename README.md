
# Airlines-Dashboard

### Dashboard Link : https://app.powerbi.com/groups/me/reports/384d017e-e935-44dc-9e7d-1626c1a36de1/ReportSection

## Problem Statement

This dashboard helps the airlines understand their customers better. It helps the airlines know if their customers are satisfied with their services. Through different ratings, they get to know their improvement area, & thus they can improve their services by identifying these area. It also lets them know the average delay & departure time, thus since by using this dashboard they have identified this problem, they can further work on factors responsible for these unwanted delays.

Since, number of neutral/dissatisfied customers (almost 57 %) are more than satisfied customers (around 43 %), thus in all they must work on improving their services. 



### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that in none of the columns errors & empty values were present except column named "Arrival Delay".
- Step 5 : For calculating average delay time, null values were not taken into account as only less than 1% values are null in this column(i.e column named "Arrival Delay") 
- Step 6 : In the report view, under the view tab, theme was selected.
- Step 7 : Since the data contains various ratings, thus in order to represent ratings, a new visual was added using the three ellipses in the visualizations pane in report view. 
- Step 8 : Visual filters (Slicers) were added for four fields named "Class", "Customer Type", "Gate Location" & "Type of travel".
- Step 9 : Two card visuals were added to the canvas, one representing average departure delay in minutes & other representing average arrival delay in minutes.
           Using visual level filter from the filters pane, basic filtering was used & null values were unselected for consideration into average calculation.
           
           Although, by default, while calculating average, blank values are ignored.
- Step 10 : A bar chart was also added to the report design area representing the number of satisfied & neutral/unsatisfied customers. While creating this visual, field named "Gender" was also added to the Legends bucket, thus number of customers are also seggregated according the gender. 
- Step 11 : Ratings Visual was used to represent different ratings mentioned below,

  (a) Baggage Handling

  (b) Check-in Services
  
  (c) Cleanliness
  
  (d) Ease of online booking
  
  (e) Food & Drink
  
  (f) In-flight Entertainment

  (g) In-flight Service
  
  (h) In-flight wifi service
  
  (i) Leg Room service
  
  (j) On-board service
  
  (k) Online boarding
  
  (l) Seat comfort
  
  (m) Departure & arrival time convenience
  
In our dataset, Some parameters were assigned value 0, representing those parameters are not applicable for some customers.

All these values have been ignored while calculating average rating for each of the parameters mentioned above.

- Step 12 : In the report view, under the insert tab, two text boxes were added to the canvas, in one of them name of the airlines was mentioned & in the other one company's tagline was written.
- Step 13 : In the report view, under the insert tab, using shapes option from elements group a rectangle was inserted & similarly using image option company's logo was added to the report design area. 
- Step 14 : Calculated column was created in which, customers were grouped into various age groups.

for creating new column following DAX expression was written;
       
        Age Group = 
        
        if(airline_passenger_satisfaction[Age]<=25, "0-25 (25 included)",
        
        if(airline_passenger_satisfaction[Age]<=50, "25-50 (50 included)",
        
        if(airline_passenger_satisfaction[Age]<=75, "50-75 (75 included)",
        
        "75-100 (100 included)")))
        
Snap of new calculated column ,

![Snap_1](https://user-images.githubusercontent.com/102996550/174089602-ab834a6b-62ce-4b62-8922-a1d241ec240e.jpg)

        
- Step 15 : New measure was created to find total count of customers.

Following DAX expression was written for the same,
        
        Count of Customers = COUNT(airline_passenger_satisfaction[ID])
        
A card visual was used to represent count of customers.

![Snap_Count](https://user-images.githubusercontent.com/102996550/174090154-424dc1a4-3ff7-41f8-9617-17a2fb205825.jpg)

        
 - Step 16 : New measure was created to find  % of customers,
 
 Following DAX expression was written to find % of customers,
 
         % Customers = (DIVIDE(airline_passenger_satisfaction[Count of Customers], 129880)*100)
 
 A card visual was used to represent this perecntage.
 
 Snap of % of customers who preferred business class
 
 ![Snap_Percentage](https://user-images.githubusercontent.com/102996550/174090653-da02feb4-4775-4a95-affb-a211ca985d07.jpg)

 
 - Step 17 : New measure was created to calculate total distance travelled by flights & a card visual was used to represent total distance.
 
 Following DAX expression was written to find total distance,
 
         Total Distance Travelled = SUM(airline_passenger_satisfaction[Flight Distance])
    
 A card visual was used to represent this total distance.
 
 
 ![Snap_3](https://user-images.githubusercontent.com/102996550/174091618-bf770d6c-34c6-44d4-9f5e-49583a6d5f68.jpg)
 
 - Step 18 : The report was then published to Power BI Service.
 
 
![Publish_Message](https://user-images.githubusercontent.com/102996550/174094520-3a845196-97e6-4d44-8760-34a64abc3e77.jpg)

# Snapshot of Dashboard (Power BI Service)

![dashboard_snapo](https://user-images.githubusercontent.com/102996550/174096257-11f1aae5-203d-44fc-bfca-25d37faf3237.jpg)

 
 # Report Snapshot (Power BI DESKTOP)

 
![Dashboard_upload](https://user-images.githubusercontent.com/102996550/174074051-4f08287a-0568-4fdf-8ac9-6762e0d8fa94.jpg)

# Insights

A single page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the dashboard;

### [1] Total Number of Customers = 129880

   Number of satisfied Customers (Male) = 28159 (21.68 %)

   Number of satisfied Customers (Female) = 28269 (21.76 %)

   Number of neutral/unsatisfied customers (Male) = 35822 (27.58 %)

   Number of neutral/unsatisfied customers (Female) = 37630 (28.97 %)


           thus, higher number of customers are neutral/unsatisfied.
           
### [2] Average Ratings

    a) Baggage Handling - 3.63/5
    b) Check-in Service - 3.31/5
    c) Cleanliness - 3.29/5
    d) Ease of online booking - 2.88/5
    e) Food & Drink - 3.21/5
    f) In-flight Entertainment - 3.36/5
    g) In-flight service - 3.64/5
    h) In-flight Wifi service - 2.81/5
    i) Leg room service - 3.37/5
    j) On-board service - 3.38/5
    k) Online boarding - 3.33/5
    l) Seat comfort - 3.44/5
    m) Departure & arrival convenience - 3.22/5
  
  while calculating average rating, null values have been ignored as they were not relevant for some customers. 
  
  These ratings will change if different visual filters will be applied.  
  
  ### [3] Average Delay 
  
      a) Average delay in arrival(minutes) - 15.09
      b) Average delay in departure(minutes) - 14.71
Average delay will change if different visual filters will be applied.

 ### [4] Some other insights
 
 ### Class
 
 1.1) 47.87 % customers travelled by Business class.
 
 1.2) 44.89 % customers travelled by Economy class.
 
 1.3) 7.25 % customers travelled by Economy plus class.
 
         thus, maximum customers travelled by Business class.
 
 ### Age Group
 
 2.1)  21.69 % customers belong to '0-25' age group.
 
 2.2)  52.44 % customers belong to '25-50' age group.
 
 2.3)  25.57 % customers belong to '50-75' age group.
 
 2.4)  0.31 % customers belong to '75-100' age group.
 
         thus, maximum customers belong to '25-50' age group.
         
### Customer Type

3.1) 18.31 % customers have customer type 'First time'.

3.2) 81.69 % customers have customer type 'returning'.
       
       thus, more customers have customer type 'returning'.

### Type of travel

4.1) 69.06 % customers have travel type 'Business'.

4.2) 30.94 % customers have travel type 'Personal'.

        thus, more customers have travel type 'Business'.


**anshbodele/anshbodele** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->















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


<img width="1152" height="202" alt="Image" src="https://github.com/user-attachments/assets/ba2fa5f5-589a-435c-8013-5ed2fc5439a3" />


<img width="465" height="72" alt="Image" src="https://github.com/user-attachments/assets/011b1f9b-b83f-4b59-bdf2-595c3558d06a" />


<img width="1155" height="72" alt="Image" src="https://github.com/user-attachments/assets/e353e13e-d70f-45ea-8aed-b09f19dd8b21" />


<img width="991" height="51" alt="Image" src="https://github.com/user-attachments/assets/25fd172a-7802-4646-bf4b-2acee3715107" />


<img width="1148" height="182" alt="Image" src="https://github.com/user-attachments/assets/5e863530-be8b-48bb-959c-e7dc12b7ae7a" />


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

