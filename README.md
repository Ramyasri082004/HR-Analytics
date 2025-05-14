# HR Analytics SQL Project

This project involves the use of structured SQL queries to analyze a Human Resources dataset. The goal is to uncover insights related to employee attrition, compensation, performance, and engagement. The dataset includes fields such as employee ID, department, education, gender, marital status, job level, salary, performance rating, and more.

## Dataset Source

[HR Analytics Prediction Dataset - Kaggle](https://www.kaggle.com/datasets/rishikeshkonapure/hr-analytics-prediction)

## Tools Used

- MySQL
- SQL Server Management Studio (Optional)
- Excel/CSV for dataset cleaning and formatting

## Project Objectives

- Analyze employee attrition rates and reasons.
- Compare compensation across departments and job levels.
- Evaluate employee satisfaction and performance.
- Identify factors influencing attrition and promotion.

---

## SQL Queries and Insights

-- HR Analytics SQL Project
-- Dataset: HR Analytics Prediction
-- Tool: MySQL

-- 1. Total employees and attrition counts
SELECT 
    COUNT(*) AS TotalEmployees,
    SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) AS EmployeesLeft,
    SUM(CASE WHEN Attrition = 'No' THEN 1 ELSE 0 END) AS EmployeesStayed,
    ROUND(SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2) AS AttritionRate,
    ROUND(SUM(CASE WHEN Attrition = 'No' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2) AS RetentionRate
FROM hr_analytics;

-- 2. Attrition rate by department
SELECT 
    Department,
    COUNT(*) AS TotalEmployees,
    SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) AS Attritions,
    ROUND(SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2) AS AttritionRate
FROM hr_analytics
GROUP BY Department;

-- 3. Attrition by job role
SELECT 
    JobRole,
    COUNT(*) AS TotalEmployees,
    SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) AS Attritions,
    ROUND(SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2) AS AttritionRate
FROM hr_analytics
GROUP BY JobRole
ORDER BY AttritionRate DESC;

-- 4. Attrition by education level
SELECT 
    Education,
    COUNT(*) AS TotalEmployees,
    SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) AS Attritions,
    ROUND(SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2) AS AttritionRate
FROM hr_analytics
GROUP BY Education;

-- 5. Average salary by job role and department
SELECT 
    Department,
    JobRole,
    ROUND(AVG(MonthlyIncome), 2) AS AvgMonthlyIncome
FROM hr_analytics
GROUP BY Department, JobRole
ORDER BY AvgMonthlyIncome DESC;

-- 6. Average income for employees who left vs stayed
SELECT 
    Attrition,
    ROUND(AVG(MonthlyIncome), 2) AS AvgIncome
FROM hr_analytics
GROUP BY Attrition;

-- 7. Total salary expenditure by department
SELECT 
    Department,
    SUM(MonthlyIncome) AS TotalSalary
FROM hr_analytics
GROUP BY Department
ORDER BY TotalSalary DESC;

-- 8. Average work-life balance by job role
SELECT 
    JobRole,
    ROUND(AVG(WorkLifeBalance), 2) AS AvgWorkLifeBalance
FROM hr_analytics
GROUP BY JobRole
ORDER BY AvgWorkLifeBalance DESC;

-- 9. Job satisfaction vs attrition
SELECT 
    Attrition,
    ROUND(AVG(JobSatisfaction), 2) AS AvgSatisfaction
FROM hr_analytics
GROUP BY Attrition;

-- 10. Number of employees promoted in the last 5 years
SELECT 
    COUNT(*) AS PromotedEmployees
FROM hr_analytics
WHERE YearsSinceLastPromotion > 0;

-- 11. Performance rating vs attrition
SELECT 
    Attrition,
    ROUND(AVG(PerformanceRating), 2) AS AvgPerformanceRating
FROM hr_analytics
GROUP BY Attrition;

-- 12. Training hours vs performance rating
SELECT 
    TrainingTimesLastYear,
    ROUND(AVG(PerformanceRating), 2) AS AvgPerformance
FROM hr_analytics
GROUP BY TrainingTimesLastYear
ORDER BY TrainingTimesLastYear;

-- 13. Average years at company by job role
SELECT 
    JobRole,
    ROUND(AVG(YearsAtCompany), 2) AS AvgTenure
FROM hr_analytics
GROUP BY JobRole
ORDER BY AvgTenure DESC;

-- 14. Employees with more than 10 years at the company
SELECT 
    COUNT(*) AS EmployeesWith10PlusYears
FROM hr_analytics
WHERE YearsAtCompany > 10;

-- 15. Attrition by marital status
SELECT 
    MaritalStatus,
    COUNT(*) AS AttritionCount
FROM hr_analytics
WHERE Attrition = 'Yes'
GROUP BY MaritalStatus;

-- 16. Attrition by overtime status
SELECT 
    OverTime,
    COUNT(*) AS AttritionCount
FROM hr_analytics
WHERE Attrition = 'Yes'
GROUP BY OverTime;

-- 17. Average age and income by department
SELECT 
    Department,
    ROUND(AVG(Age), 2) AS AvgAge,
    ROUND(AVG(MonthlyIncome), 2) AS AvgIncome
FROM hr_analytics
GROUP BY Department;

-- 18. Job role vs performance rating
SELECT 
    JobRole,
    ROUND(AVG(PerformanceRating), 2) AS AvgPerformance
FROM hr_analytics
GROUP BY JobRole
ORDER BY AvgPerformance DESC;

-- 19. Education field vs job satisfaction
SELECT 
    EducationField,
    ROUND(AVG(JobSatisfaction), 2) AS AvgJobSatisfaction
FROM hr_analytics
GROUP BY EducationField;

-- 20. Monthly income distribution by gender
SELECT 
    Gender,
    MIN(MonthlyIncome) AS MinIncome,
    MAX(MonthlyIncome) AS MaxIncome,
    ROUND(AVG(MonthlyIncome), 2) AS AvgIncome
FROM hr_analytics
GROUP BY Gender;
