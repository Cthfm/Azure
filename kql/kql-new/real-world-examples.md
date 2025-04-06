# Real World Examples

### 🛠️ Real-World Scenario 1: Find Brute-Force Login Attempts

**Problem:**\
Attackers often try to guess passwords by attempting many logins quickly.

***

#### 🔥 Detection Query

```kql
kqlCopyEditSecurityEvent
| where EventID == 4625 // Failed login
| where TimeGenerated > ago(1d)
| summarize FailedAttempts = count() by Account, bin(TimeGenerated, 1h)
| where FailedAttempts > 10
| order by FailedAttempts desc
| render barchart
```

**Explanation:**

* Look for failed logins in the past day.
* Group by account and 1-hour windows.
* Find accounts with more than 10 failures in an hour.
* Visualize accounts with the most failures.

***

### 🛠️ Real-World Scenario 2: Detect Rare Sign-in Locations

**Problem:**\
An attacker signs in from a country or location not seen before for a user.

***

#### 🔥 Detection Query

```kql
kqlCopyEditSigninLogs
| summarize Locations = makeset(Location) by UserPrincipalName
| where array_length(Locations) > 1
| project UserPrincipalName, Locations
```

**Explanation:**

* Group locations each user has signed in from.
* If a user has signed in from **multiple different locations**, that’s suspicious.

***

### 🛠️ Real-World Scenario 3: Monitor Critical Servers' Health

**Problem:**\
You want to make sure your production servers are sending heartbeat signals regularly.

***

#### 🔥 Monitoring Query

```kql
kqlCopyEditHeartbeat
| where Computer startswith "PROD-"
| where TimeGenerated > ago(1h)
| summarize LastHeartbeat = max(TimeGenerated) by Computer
| order by LastHeartbeat asc
```

**Explanation:**

* Check if any production servers (`PROD-`) have missed their heartbeat in the last hour.

***

### 🛠️ Real-World Scenario 4: Find Users with Multiple Failed and Successful Logins

**Problem:**\
A compromised account might show both failed and successful logins.

***

#### 🔥 Detection Query

```kql
kqlCopyEditSecurityEvent
| where EventID in (4624, 4625) // Successful and failed logins
| where TimeGenerated > ago(1d)
| summarize FailedCount = countif(EventID == 4625), SuccessCount = countif(EventID == 4624) by Account
| where FailedCount > 5 and SuccessCount > 0
| order by FailedCount desc
```

**Explanation:**

* Find accounts with **more than 5 failures** but **at least 1 success**.
* Highly suspicious: someone eventually guessed the password!

***

### 🛠️ Real-World Scenario 5: Summarize Alerts by Severity

**Problem:**\
You want to prioritize incident response by alert severity.

***

#### 🔥 Detection Query

```kql
kqlCopyEditSecurityAlert
| where TimeGenerated > ago(7d)
| summarize AlertCount = count() by Severity
| render piechart
```

**Explanation:**

* Summarize how many alerts occurred for each severity level (High, Medium, Low).
* Visualize using a pie chart.

***

### 🛠️ Bonus: Quick Threat Hunt Template

**Hunting Template Structure:**

```kql
kqlCopyEdit<TableName>
| where <Filter> 
| extend <Create New Fields if Needed>
| summarize <Group Data>
| order by <Order Results>
| render <Visualize>
```

You can use this basic flow to **hunt for anything**:

* Choose a table.
* Filter suspicious activity.
* Create new fields if needed (like labels).
* Summarize and sort your data.
* Visualize the results.

***

### 📈 Real-World Thinking Tips

| Situation                     | KQL Strategy                               |
| ----------------------------- | ------------------------------------------ |
| Too much data?                | Use `where` early to filter                |
| Missing information?          | Use `join` to pull in more context         |
| Suspicious pattern?           | Use `summarize` to group and detect trends |
| Messy fields?                 | Use `parse` or `extract` to clean it       |
| Need to communicate findings? | Use `render` to create charts              |

***

### 📝 Mini Practice Exercises

#### 1. Brute-Force Detection

**Query:** Find users with more than 10 failed login attempts in 1 hour.

***

#### 2. Rare Location Detection

**Query:** Find users who logged in from multiple locations.

***

#### 3. Critical Server Monitoring

**Query:** Find production servers with missing heartbeats in the last hour.

***

#### 4. Alert Prioritization

**Query:** Summarize number of alerts by severity in a pie chart.

***

### ⚡ Pro Tips

* **Think like an attacker:** How would you try to break into a system? Now write a query to find that behavior.
* **Start simple:** Filter, summarize, visualize.
* **Always time-bound your queries:** Use `TimeGenerated > ago(1d)` to avoid pulling unnecessary old data.

***

### 📢 Key Takeaways

* Real-world KQL means **solving actual problems**: hunting threats, monitoring systems, investigating incidents.
* Combining skills like **filtering**, **summarizing**, **joining**, and **visualizing** makes you a powerful KQL user.
* Practicing real-world scenarios helps you move from theory to action.
