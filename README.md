# Project Management Analysis

## Table of content
- [Project Overview](#project-overview)
- [Data Sources](#data-sources)

### Project Overview

This project focuses on organizing workforce and financial data to develop a Power BI dashboard that provides insights into employee performance, financial risks, and project health. The dashboard will help the organization identify departments and projects that are at risk of being over budget or underperforming, allowing for timely corrective actions. Additionally, it will analyse departmental expenses over a two-year interval to determine if budgets can sufficiently cover all expenses.

### Data Sources
The dataset for this project was obtained from the AbsentData website. The data consists of CSV files, which were used to create a database. Queries were written and then imported into Power BI for analysis.

### Tools
- SQL Server Management Studio (SSMS)- This tool was used to create a database, write queries, and import the data into Power BI for analysis.
- Power Query Editor- This was used for data cleaning and transformation of the data such as grouping departments and creating custom columns for cost and revenue. 
- Power BI- For creating the reports.

### Exploratory Data Analysis
To effectively address the organization’s needs and challenges, I categorized the problem into two major areas: Financial Risk Analysis and Project Risk Assessment. This categorization was deemed necessary to provide management and stakeholders with a clear understanding of how financial, budgeting, and performance-related decisions will be handled with corrective actions been taken. 
#### Financial Risk Analysis
- Which departments and projects are over budget?
- Which projects have the highest financial risks?
- Can the allocated budget cover all expenses for the 2-year project plan?
- Are there any departments with unusually high or low salary distributions?
#### Performance Assessment
- Are there any departments and projects that are underperforming?
- Can management and stakeholders realistically achieve upcoming projects?
- Is there sufficient budget to cover upcoming projects.

### Data Modelling
A relationship was established between the two tables-one imported from SQL and the other from Excel because they contained complementary data necessary for comprehensive analysis. The SQL table provided structured and relational data, while the Excel table contained additional details that were not available in the SQL database.
A cost table was also created, but no relationship was established with the other tables. This was intentional, as managing relationships with only the two primary tables was sufficient for analysis. Additionally, avoiding unnecessary relationships helped prevent unwanted filtering in the dashboard, ensuring a clearer and more accurate representation of financial and performance insights.

### Data Analysis
``` SQL

-- project status
With project_status as(
select project_id,
project_name,
project_budget,
'upcoming' as status
from upcoming_projects
union
select project_id,
project_name,
project_budget,
'completed' as status
from completed_projects)

-- Big Table
select e.employee_id,e.first_name,e.last_name,e.job_title,e.salary,d.Department_Name,
pa.project_id, p.project_name,p.status 
from employees e
join departments d
on e.department_id =d.department_ID
join project_assignments pa
on pa.employee_id= e.employee_id
join project_status p
on p.project_id = pa.project_id;
```

### Results /Findings.
#### Financial Risk Analysis
- None of the departments appear to be over budget for the two-year project plan.
- None of the projects appear to be over budget for the two-year project plan.
- The "Enhance Employee Engagement" project appears to have the highest financial risk for the company, as its returns show a loss of -£25,000.
- The budget for the two-year project plan is £3,450,000, while the total project cost for the same period is £1,140,000. This indicates that the allocated budget is sufficient to cover all expenses for the two-year project plan.
- All salaries are moderately distributed across various departments.

#### Performance Assessment
- The Human Resources department is the only department that is underperforming.
- The "Enhance Employee Engagement" project is the only project that is underperforming.
- There is a remaining budget of £365,000, which will be sufficient to cover the expenses of upcoming projects. However, management may consider increasing the budget to provide additional support for underperforming projects.

### Recommendations
- Since no department or project is currently over budget, management should continue tracking expenses closely to ensure financial discipline is maintained.
- Implement periodic budget reviews to identify any early signs of overspending and take corrective action as needed.
- Conduct an internal assessment to identify the root causes of underperformance of Human Resource department. Example:  inefficiencies, skill gaps, or resource limitations.
- Adjust project goals and strategies based on feedback from employees and stakeholders.
- Consider reallocating additional funds from the remaining budget to boost project outcomes and minimize financial losses.
- Since the ‘Enhance Employee Engagement’ project presents the highest financial risk, management should implement a risk mitigation plan. Example: Define clear success metrics and track progress closely.
- If the project continues to generate losses, reassess its feasibility and explore alternative strategies or project termination if necessary.
