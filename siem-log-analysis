-- 1. Identify all users with 'Admin' status to review high-privilege access
SELECT username, department, status 
FROM user_accounts 
WHERE status = 'Admin';

-- 2. Find 'Admin' users who have not logged in for over 90 days (Stale Accounts)
-- Stale accounts are a major security risk as they can be hijacked.
SELECT username, last_login_date, email 
FROM user_accounts 
WHERE status = 'Admin' 
AND last_login_date < '2025-12-01';

-- 3. Detect "After-Hours" login attempts that might indicate a breach
-- We are looking for logins between 11 PM and 5 AM.
SELECT login_id, username, login_time, ip_address 
FROM login_logs 
WHERE HOUR(login_time) BETWEEN 23 AND 5;

-- 4. Audit failed login attempts to identify potential Brute Force attacks
-- Filtering for more than 3 failed attempts from the same IP.
SELECT ip_address, COUNT(*) AS failed_attempts 
FROM login_logs 
WHERE success = FALSE 
GROUP BY ip_address 
HAVING failed_attempts > 3;
