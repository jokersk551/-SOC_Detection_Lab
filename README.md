# SOC_Detection_Lab
# 🧠 Splunk Failed Login Detection — SOC Monitoring Project

## 📘 Project Overview
This project demonstrates the use of **Splunk Enterprise** to detect and analyze **failed Windows login attempts (Event ID 4625)**.  
It simulates a mini **Security Operations Center (SOC)** scenario where failed login patterns are monitored to identify brute-force or unauthorized access attempts.

---

## 🧩 Objective
To detect multiple failed login attempts from the same IP or user account and visualize them through Splunk dashboards.

---

## ⚙️ Tools Used
- **Splunk Enterprise (Free Trial / Local Instance)**
- **Windows Security Event Log**
- **Index:** `soc_lab`
- **Sourcetype:** `WinEventLog:Security`

---

## 🗂️ Dataset
File: `windows_failed_logons.log`  
Contains:
- EventCode  
- AccountName  
- SourceNetworkAddress  
- FailureReason  

Each log entry represents a failed Windows login attempt.

---

## 🚀 Steps to Reproduce

### 1️⃣ Create Index and Add Data
1. Open Splunk → **Settings → Indexes → New Index**  
   → Name it `soc_lab`.
2. Go to **Add Data → Upload File → Select** your log file (`windows_failed_logons.log`).
3. Assign:
   - Index: `soc_lab`
   - Sourcetype: `WinEventLog:Security`

---

### 2️⃣ Basic Search
```
index="soc_lab" EventCode=4625
Displays all failed login attempts from the imported logs.

3️⃣ Failed Login Summary

index="soc_lab" EventCode=4625
| stats count by AccountName, SourceNetworkAddress, FailureReason
| sort - count
Shows which accounts and IPs have the most failed attempts.

4️⃣ Top Users with Most Failures
index="soc_lab" EventCode=4625
| stats count by AccountName
| sort - count
Visualize this as a Bar Chart to easily identify the most targeted users.

5️⃣ Dashboard Panels
Create a dashboard named “Failed Login Detection Dashboard” and add these queries as panels:

Panel Name	Query	Visualization
Failed Login Summary	`index="soc_lab" EventCode=4625	stats count by AccountName, SourceNetworkAddress`
Top Failed Accounts	`index="soc_lab" EventCode=4625	stats count by AccountName
Failure Reason Breakdown	`index="soc_lab" EventCode=4625	stats count by FailureReason`

⚠️ Observations
Repeated login failures from the same IP indicate possible brute-force activity.

Administrator and guest accounts are most commonly targeted.

Some attempts show “Unknown user” errors — possible enumeration attempts.

🛡️ Recommendations
Implement account lockout policies.

Monitor repeated login failures using Splunk alerts.

Disable or rename default accounts like administrator and guest.

Restrict login attempts from external IP ranges.

✅ Conclusion
Using Splunk Enterprise, we successfully:

Indexed and searched Windows log data

Detected failed login attempts (Event ID 4625)

Built visual dashboards for monitoring login failures

Identified potential brute-force patterns

📂 Folder Structure
Splunk_Failed_Login_Detection/
│
├── README.md
├── windows_failed_logons.log
└── Screenshort/
    └── screenshorts 
👨‍💻 Author
Sahil Rajesh Koli
🎓 B.Tech IT | Ethical Hacker | Cybersecurity Analyst
📧 sahilkoli11223@gmail.com
🔗 LinkedIn • GitHub

“Logs never lie — they tell the real story.” 🕵️‍♂️
