# 🌍 TravelTide Customer Segmentation & Rewards Program
---

## 🧠 Overview

**TravelTide** is an online travel startup focused on improving customer retention by launching a **personalized rewards program**. They have 1 million users and 5 million unique app sessions. This project segments Traveltide customers based on website behavior to enable targeted perks using data-driven segmentation. To ensure meaningful results, the dataset was filtered to include **only users with more than 7 sessions since January 4, 2023**.

---

## 🎯 Objectives

- Analyze behavioral data to identify trends.
- Segment users based on travel and booking behaviors.
- Recommend perks for each segment to maximize engagement:
  - 🧳 Free Checked Bag  
  - 🏨 Free Hotel Meal  
  - 1️⃣ Discount on First Travel  
  - 🛋️ Airport Lounge Access
  - 🎁 1 Free Hotel Night with Flight
  - ✈️ Free Flight
  - 💺 Free Seat Upgradee

---

## 🔨 Tools Used

- SQL - for data cleaning and extraction
- Tableau - for visualization and pattern recognition

---

## 🗂️ Data Sources
 
The dataset consisted of four original tables:

- **Users**: Demographic information about each customer
- **Sessions**: Information about individual browsing sessions
- **Flights**: Information about purchased flights
- **Hotels**: Information about purchased hotel stays


From these, I created three working tables for the analysis:

- **Session-based table**: Cleaned and filtered session-level data with relevant activity metrics.
  - [Session-based table code]()
- **User-based table**: Aggregated customer metrics such as age, number of trips, session counts, and family status.
  - [User-based table code](https://www.notion.so/User-based-Table-23b52541c1658016b9e3fb15b8c5e56e?source=copy_link)
- **Final segmentation table**: Combined user attributes and behavior into defined customer groups and assigned a likely preferred perk.
  - [Final table code](https://www.notion.so/Final-Table-with-Customer-Groups-and-Assigned-Perk-23b52541c16580518459e3a61a5247b3?source=copy_link)
  - [Final Cleaned Dataset]()

#### 🔍 Data Filtering
To focus on engaged users, only **active users** were included in the analysis.
- Users with **more than 7 sessions since January 4, 2023**. 
  - 5,998 eligible users


#### ⚠️ Data Cleaning Notes
- Some records included **negative night stayed** due to check-out date occuring before check-in date.
  - This was caused by default or placeholder values in the check out field.
  - Affected rows were replaced with a value of **1** (night).

---

## 🗺️ Project Plan

1. **Data Cleaning & Filtering**  
   - Removed duplicate sessions  
   - Cleaned hotel booking data (e.g. adjusted negative nights)
   - Included sessions starting after January 4, 2023
   - Filtered for users with more than 7 sessions to ensure engagement

2. **User-Level Feature Engineering**  
   - Aggregated sessions into customer profiles
   - Calculated metrics like `age`, `num_clicks`, `avg_session_duration`, `num_flights`, `money_spend_hotel`, `avg_km_flown`, and   `time_after_booking`

3. **Customer Segmentation (SQL)**  
   - Created a decision tree to group users
   - Applied these rules using `CASE WHEN` logic  
   - Categories based on age, trip frequency, and family status

4. **Perk Assignment**  
   - Created visuals in Tableau to find traveler insights and patterns
   - EDA in SQL to find insights
   - Matched reward to each group’s top travel need

5. **Insights & Report**  
   - Created summaries and reports for stakeholders  
   - Offered marketing and product recommendations
     
---

## 🔧 Feature Engineering

Sample features created:

| Feature               | Description                                                          |
|-----------------------|----------------------------------------------------------------------|
| `num_sessions`        | Total sessions per user. Used to identify active users (7+ sessions).|
| `num_trips`           | Number of trips taken (excluding cancellations).                     |
| `age`                 | Derived from birthdate                                               |
| `cust_group`          | Final segmentation label combining age, travel frequency, and family status.      |
| `customer_perk`       | Assigned perk most likely to appeal to each group.                   |
| `avg_session_duration`| How long users spend on website. Behavioral insight                  |
| `money_spend_hotel`   | Hotel expenses. Behavioral insight                                   |
| `avg_km_flown`        | Avg. distance flown. Behavioral insight                              |

---

## 🔍 Segmentation Approach

- Decision Tree
- Users were segmented using SQL `CASE WHEN` logic based on **age**, **trip frequency**, and **family status**:

  ### 🧮 Segmentation Logic (SQL)
  
  ```sql
  CASE 
    WHEN has_children = TRUE THEN 'Family traveler'
    WHEN age > 60 THEN 'Senior traveler'
    WHEN age < 60 THEN 
       CASE
         WHEN num_trips <= 2 THEN 'Dreamers'
         WHEN age < 30 AND num_trips > 2 THEN 'Young frequent traveler'
         WHEN age > 30 THEN 
           CASE 
             WHEN num_trips > 5 THEN 'Business traveler'
             WHEN num_trips BETWEEN 2 AND 5 THEN 'Adult frequent traveler'
             ELSE 'Others'
           END
         ELSE 'Others'
       END
    ELSE 'Others'
  END AS cust_group;
  ```

---

## 🧑‍🤝‍🧑 Customer Segments and Perks

**Family Travelers - Free Checked Bag**  
- Travelers with Children
- High Bag Usage

**Senior Traveler - Free Hotel Meal**  
- Travelers older than 60
- Take Long Trips

**Dreamers - Discount on First Travel**  
- Fewer than 2 trips
- High Cancellations

**Young Frequent Traveler - 1 Free Hotel Night with Flight**  
- Younger than 30  
- More than 2 trips

**Adult Frequent Traveler - Free Flight**  
- Older than 30  
- Between 2 and 5 trips
- Highest Total Trips

**Business Traveler - Airport Lounge Access**  
- Older than 30  
- More than 5 trips taken

**Other Traveler - Free Seat Upgrade**  
- Irregular and Ungrouped Users

---

## 📄 Reports and Presentation

**Executive Summary**
  - [View here](Reports/summary_report.pdf)
    
**Detailed Report**
  - [View Full project report](Reports/Detailed_Report.pdf)
    
**Video Presentation**
- A brief walkthrough of the project, insights, and outcomes is available here:
  - [View Slide deck](Reports/TravelTide.pptx)
  - [Video Presentation](https://www.loom.com/share/4e0f17df651242c18a5e7f9f667d0a95?sid=5e2d2dea-708c-4762-85d8-3d3b006b8fc6)
---

## ✅ Recommendations

1. **Personalize Rewards** – Implement a segmented rewards program that aligns perks with customer travel behaviors
2. **Monitor Performance** – Enable optimization with regualr tracking of perk usage and customer feedback
Future Analysis can help refine segments and identify shifts in travel behavior to ensure continued alignment between customer needs and the reward program

---
