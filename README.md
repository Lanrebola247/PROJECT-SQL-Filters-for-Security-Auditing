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
