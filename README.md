**Analysis of delivery delays using Power BI**

**SITUATION:**

 About 64% of orders received by Burlington Company result in late deliveries every week during the period (Aug.21 - Sep.22), resulting in an accumulation of backlog orders over the weeks.

**TASK:**
Develop suitable reports to effectively trace the root cause of delay of orders so that late deliveries are minimized in future

**ACTION:**
1. The first dataset contains high level overview of no of orders completed which were overdue, due for the week and due for the next week. This data is transformed in Power Query to organize the information and make it suitable for analysis. 
   ![image](https://github.com/user-attachments/assets/fa1041cf-2fed-4f47-a3ea-f6d78aee9393)

   There are calculated columns developed using DAX to calculate the difference between consecutive rows to calculate number of orders completed.
   ![image](https://github.com/user-attachments/assets/7ebe47e4-e581-4b79-92cc-3579532cadc6)


3. A calculated table is created from the this dataset to perform weekly analysis of the completed orders.
   ![image](https://github.com/user-attachments/assets/86006f74-df9e-461a-b940-70ea6ca0602c)

   A common date table is also created to simplify time series analysis.
   ![image](https://github.com/user-attachments/assets/a32f080a-99f3-4418-876f-5bb9e7586736)

4. The second dataset contains compilation of 90 daily reports that tracks every Manufacturing Order, identifying its department, process, customer order to which it belongs to, ETA, Promised delivery date, Days on hold and so on. To analyze delay contributors, duplicate records must be eliminated. For every Manufacturing Order, Dept and Process combination, there should be an unique latest record to analyze the delay.
   Different queries and transformations are applied in Power Query to obtain this data.

   **Query 1:**

   ![image](https://github.com/user-attachments/assets/82d45517-64fb-456c-b9e7-13443b68c82d)

   We obtain the recent reporting date for every Manufacturing Order, Dept and Process combination.

   **Query 2:**

   ![image](https://github.com/user-attachments/assets/6278ae45-a2ac-4227-83cc-32848913d188)

   Since multiple records with same reporting date existed, we use Maximum Manufacturing Order Line Number to obtain a unique record for the combination.

   ![image](https://github.com/user-attachments/assets/f0a19996-3a26-46a4-9219-1368a613236a)

  These resulting query is merged with original data to obtain the final table containing the required information.
  
   ![image](https://github.com/user-attachments/assets/3f405430-7932-4f73-8787-4a3c1db31cf9)

**RESULT**:
The visualizations are created in three reports to analyze the delay and progress of completing orders.
   
**REPORT 1:**
1. ![image](https://github.com/user-attachments/assets/b4424049-bb0a-450d-b648-82194dc75a45)

   In the Ribbon Chart "**Different type of orders completed every week**", we can identify what priority the company assigns to completing (i) Late/Overdue orders (ii) Due orders by that week (iii) Due orders by next week. Ideally, the company should first complete overdue orders, then due orders for the week and later, due orders for the next week.

   Ribbon chart is used since it can help easily identify the change in ranking across categories over time. Mostly, the company has prioritized order completion correctly. But for weeks 34, 36, 37 and 38, the priorities has changed. During the week 34, 36 and 38, orders that are due by next week are focused and this is not right. **The weeks 34, 36 and 38 of the year are identified as one of the maximum delay contributors**

   If the week 34 is selected in slicer and analyzed using other 2 visuals:

   ![image](https://github.com/user-attachments/assets/1e50e163-1879-4f81-b9e0-f445ac37bbe0)

   We observe that Day 1, Monday of the week has contributed to most of the order completion for next week, whereas the other days have the right priority. **Week 34, Monday is one of maximum delay contributor**

   Repeating same for week 36 and 38, we obtain Tuesday and Monday as Maximum delay contributors, respectively. Observing the pattern, we can infer that **the company prioritizes completion of future week orders at the start of the present week**. This needs to be corrected and resolved.

**REPORT 2:**
![image](https://github.com/user-attachments/assets/0a9d9030-8736-4ad1-b8ed-6beb8ba0124b)

The first visual **"Delay by Dept , Process and Mfg Order"** and the two adjacent tables **"Top 5 delayed departments and processes"** and **Top 5 delayed orders**  help us trace the Delay causing components.

On drilling down most delayed department: Finishing department further, we obtain:

![image](https://github.com/user-attachments/assets/db2bbeef-52a6-4e5e-86ff-7c618f81861f)

We can see maximum delay causing processes within the department. In the two adjacent tables, we can identify the top delayed components. On drilling down most delayed process "Pre-Finish" further, we obtain:

![image](https://github.com/user-attachments/assets/28cb77f3-d506-4495-8bf1-1b87fc76a0b1)

We can easily trace which Manufacturing Order caused the maximum delay with this process which is B71...69 with a delay of 73 days. This order needs investigation and focus. We can also observe the drill down path near the title to keep track. This is created using DAX.

The same process is repeated for identifying Maximum Days on hold causing contributors. 

![image](https://github.com/user-attachments/assets/d18c1414-b7e2-4bd0-a0ff-4414440089e5)

We observe that Prefinishing process is the contributor here as well but for a different order: BA123...70 with a hold of 13 days. This needs investigation.

**REPORT 3:**
![image](https://github.com/user-attachments/assets/ef4cc68e-4102-490e-9d3b-2fcbafdd27e7)

The first visual **Top Customers Affected** provides drilldown of Customer-> Customer order No -> Department -> Process -> Manufacturing Order. The two adjacent tables add detail to Top 10 customers affected and Top 10 Manufacturing Orders affected. 

On drilling down most delayed Customer, we obtain: 

![image](https://github.com/user-attachments/assets/fcdbb301-bf63-4958-811c-25528bdb654c)

3 customer orders are affected and this is caused by 25 Manufacturing orders. From the line graph, we see October is the season which caused surge in the Delay. 

On drilling down most delayed Customer order number, we obtain:

![image](https://github.com/user-attachments/assets/2d9beeaf-f59c-4e49-8842-6298edf9f766)

Inspection Department is maximum contributor. 9 Manufacturing Orders caused delay in this department. October is the season for the delays to occur.

On drilling down Inspection department further, we obtain:
![image](https://github.com/user-attachments/assets/27d62f98-ee10-4d6a-bf77-86b8f29980f3)

We observe High Stretch process is causing the delay.

Drilling down the high stretch process further, we obtain:

![image](https://github.com/user-attachments/assets/3ef61bc0-6ef4-4295-8d4f-ffbe39e3b667)

We identify that for this customer, 6 Manufacturing Orders caused the delay. The maximum contributor is B21...41 order. This needs to be investigated keeping in mind the october time period and should be resolved to reduce the delay for that customer.






















   

   
   

