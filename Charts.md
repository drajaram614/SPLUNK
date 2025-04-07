[Table of Contents](https://github.com/drajaram614/SPLUNK/blob/main/README.md)

# **Understanding Charts in Splunk**

## **Introduction**
This guide covers how to create basic visualizations in Splunk, including time charts, bar charts, pie charts, and single-value panels. These visualizations help analyze data trends and improve decision-making.  

## **Basic Splunk Searches for Charts**
Below are some key searches and how they translate into different chart types.

### **1. Time Chart - Average Bytes Over Time**
```spl
index=web
| timechart avg(bytes) 
```
- **Displays the average number of bytes over time as a line chart.**  

![ ](img/58.png)

---

### **2. Time Chart - Average Bytes Per Host**
```spl
index=web
| timechart avg(bytes) by host
```
- **Shows the average bytes per web server over time, each represented by a different color-coded line.**  

![ ](img/59.png)

---

### **3. Bar Chart - Average Bytes Per Host (Static)**
```spl
index=web
| chart avg(bytes) by host
```
- **Displays the total average bytes per host as a static bar chart (not over time).**  

![ ](img/60.png)

---

### **4. Time Chart - Actions Taken by Users**
```spl
index=web
| where isnotnull(action)
| timechart count by action
```
- **Counts actions taken over time, visualized as a line chart.**  
- **Can be customized with stacking, labels, and legend positioning.**  

![ ](img/61.png)
*line chart*

![ ](img/62.png)
*column chart*

![ ](img/63.png)
*stacked column chart*

![ ](img/64.png)
*Added Chart Overlay line for purchases and moved legend to bottom*


## Create Dashboard

![ ](img/65.png)
*Dashboard created for actions taken by shoppers, will be updated with more charts and info*
---

### **5. Pie Chart - Total Actions Taken**
```spl
index=web
| stats count by action
```
- **Displays a pie chart showing the distribution of different actions taken by users.**  

![ ](img/66.png)
---

### **6. Single-Value Chart - Total Purchases**
```spl
index=web action=purchase
| stats count
```
- **Shows the total number of purchases as a single-value visualization.**  
- **Color coding can highlight high or low sales performance.**  

![ ](img/67.png)

---

### **7. Column Chart - What Was Purchased**  
```spl
index=web action=purchase
| lookup productinfo.csv productId OUTPUT description
| where isnotnull(productId)
| chart count over host by description useother=f limit=0
```
- **Shows the number of purchases for each product, grouped by host, in a column chart.**

![ ](img/68.png)

---

### **8. Time Chart - Failed Login Attempts**
```spl
index=security eventtype=failed_login
| timechart count by user limit=5 useother=f usenull=f
```
- **Shows the top 5 users with the most failed login attempts over time.**  

![ ](img/69.png)

---

## **Creating a Dashboard**
You can save these searches as panels in a Splunk **dashboard** for easy access to key insights. Follow these steps:  

1. **Run a search** and adjust visualization settings.  
2. Click **Save As → Dashboard Panel**.  
3. **Name the panel** appropriately (e.g., "Top Failed Logins").  
4. Add it to an existing **"Weekly Info"** dashboard or create a new one.  
5. **Customize** panel layout, colors, and labels for better readability.  

![ ](img/70.png)

---

## **Summary**
By using **time charts, bar charts, pie charts, and single-value visualizations**, you can gain valuable insights from Splunk data. These visualizations are essential for **monitoring trends, identifying issues, and making data-driven decisions.**  

