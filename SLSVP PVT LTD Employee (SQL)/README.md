# 💼 Salary & Experience Analysis 📊  

## 📌 Overview  
This project analyzes **average salaries of professionals across companies** based on their **job title and years of experience**.  
The data is processed using **SQL queries**, and insights are visualized using **dashboards and charts**.  

---

## 📊 **Data Visualization**  
📌 **Example Dashboard:**  
![Dashboard Preview](https://github.com/MBTaras/Data-Analysis/blob/main/SLSVP%20PVT%20LTD%20Employee%20(SQL)/dashboard/dashboard1.jpg)  
!(https://github.com/MBTaras/Data-Analysis/blob/main/SLSVP%20PVT%20LTD%20Employee%20(SQL)/dashboard/dashboard12.jpg)

---

## 📌 **Dataset Information**
- **Job Titles:** Data Scientist, Software Engineer, HR Manager, Sales Executive, etc.
- **Experience Levels:** Grouped as `0`, `1-2`, `3-5`, `6-10`, `11-20`, `21-30`, `>30` years.
- **Companies Included:** Microsoft, IBM, Google, AWS, TCS.
- **Metrics:** Number of employees per company and job title, average salary per experience level.

---

## **🛠 SQL Query**
This SQL query groups employees by **experience level, job title, and company**, calculating the **average salary** for each combination.

```sql
SELECT  
  CASE
    WHEN Experience_Years = 0 THEN "0"
    WHEN Experience_Years BETWEEN 1 AND 2 THEN "1-2"
    WHEN Experience_Years BETWEEN 3 AND 5 THEN "3-5"
    WHEN Experience_Years BETWEEN 6 AND 10 THEN "6-10"
    WHEN Experience_Years BETWEEN 11 AND 20 THEN "11-20"
    WHEN Experience_Years BETWEEN 21 AND 30 THEN "21-30"
    WHEN Experience_Years > 30 THEN ">30"
  END AS exp_yrs, 
  Job_Title, count(Job_Title) as Job_Title_count,Company,
  ROUND(AVG(Salary)) AS Avg_salary
FROM employedataset
GROUP BY exp_yrs, Job_Title, Company
ORDER BY 
  CASE 
    WHEN exp_yrs = "0" THEN 0
    WHEN exp_yrs = "1-2" THEN 1
    WHEN exp_yrs = "3-5" THEN 3
    WHEN exp_yrs = "6-10" THEN 6
    WHEN exp_yrs = "11-20" THEN 11
    WHEN exp_yrs = "21-30" THEN 21
    WHEN exp_yrs = ">30" THEN 31
  END, Job_Title;
