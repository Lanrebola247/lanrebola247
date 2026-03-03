# SQL Case Study: Applying Filters for Security Investigations

## Project Overview
In this project, I acted as a Security Analyst responsible for auditing system access and managing organizational assets. I used **SQL filters** to investigate potential security incidents, detect unauthorized geographic access, and facilitate department-specific security updates.

## Scenarios & Solutions

### 🕵️ Incident Investigation (After-Hours)
**Scenario:** A potential security breach occurred after 18:00. 
**Solution:** I queried the `log_in_attempts` table using `AND` operators to isolate failed attempts occurring after business hours. This allowed the team to focus on high-risk unauthorized access patterns.

### 📍 Geographic & Temporal Auditing
**Scenario:** Suspicious activity was reported from users outside of the primary region (Mexico).
**Solution:** I utilized the `NOT LIKE 'MEX%'` filter to identify any international login attempts. I also performed a date-based audit using `OR` logic to capture activity logs across a specific 48-hour window.

### 💻 Security Patch Management (Asset Audit)
**Scenario:** The organization required targeted security updates for specific departments (Marketing, Finance, Sales) while excluding the IT department to avoid disrupting specialized systems.
**Solution:** I used `LIKE` with wildcards (`%`) to find machines in specific office wings (e.g., "East%") and utilized `NOT` to exclude IT infrastructure from general deployment scripts.

## Skills Demonstrated
- **Boolean Logic:** Proficient use of `AND`, `OR`, and `NOT` to refine security data.
- **Pattern Matching:** Implementing `LIKE` and `%` wildcards for flexible data retrieval.
- **Vulnerability Identification:** Sifting through logs to find indicators of compromise (IOCs).
- **Compliance Auditing:** Ensuring the right employees receive the right security patches.

---
*This project is part of my transition into Cybersecurity, demonstrating my ability to handle raw security data for actionable insights.*

-- PROJECT: SQL Filters for Security Auditing
-- AUTHOR: Olanrewaju Bolarinwa

-- 1. Investigating After-Hours Failed Logins
-- Logic: Filter for unsuccessful attempts (success = 0) occurring after 18:00.
SELECT * FROM log_in_attempts 
WHERE login_time > '18:00' AND success = FALSE;

-- 2. Investigating Specific Incident Dates
-- Logic: Filtering for a 48-hour window surrounding a suspicious event.
SELECT * FROM log_in_attempts 
WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';

-- 3. Geo-Fencing Audit: Identifying Logins Outside of Mexico
-- Logic: Using NOT and LIKE with wildcards to find anomalies in regional access.
SELECT * FROM log_in_attempts 
WHERE country NOT LIKE 'MEX%';

-- 4. Asset Management: Targeting Marketing/East Building for Updates
-- Logic: Correlating department and physical office location for patch management.
SELECT * FROM employees 
WHERE department = 'Marketing' AND office LIKE 'East%';

-- 5. Asset Management: Targeting Finance and Sales Departments
-- Logic: Isolating specific departments for tailored security updates.
SELECT * FROM employees 
WHERE department = 'Finance' OR department = 'Sales';

-- 6. Excluding IT Department from General Updates
-- Logic: Filtering out specialized machines that require different security protocols.
SELECT * FROM employees 
WHERE NOT department = 'Information Technology';



