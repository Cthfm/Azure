# Presenting Data

### 🛠️ The `render` Operator

**`render`** tells Azure to **display the output of your query as a chart** instead of just a table.

| Example            | Purpose                     |
| ------------------ | --------------------------- |
| `render timechart` | Show data over time         |
| `render piechart`  | Show parts of a whole       |
| `render barchart`  | Compare values side-by-side |

***

#### ✨ Basic `render` Syntax

```kql
kqlCopyEdit<your_query>
| render <chart_type>
```

***

### 🛠️ Creating a Time Chart (`render timechart`)

**Use when:** You want to show **how something changes over time**.

***

#### ✨ Example: Logins per Hour

```kql
kqlCopyEditSigninLogs
| where TimeGenerated > ago(24h)
| summarize Logins = count() by bin(TimeGenerated, 1h)
| render timechart
```

**Result:**\
A nice line graph showing how many logins occurred each hour over the past day.

**Use Case:**

* Detect unusual login times.
* Monitor service usage over time.

***

### 🛠️ Creating a Pie Chart (`render piechart`)

**Use when:** You want to show **proportions** — how different categories compare to each other.

***

#### ✨ Example: Logins by Device Type

```kql
kqlCopyEditSigninLogs
| summarize LoginCount = count() by DeviceDetail_deviceOSType
| top 5 by LoginCount
| render piechart
```

**Result:**\
A pie chart showing which device operating systems were used most.

**Use Case:**

* Visualize the distribution of users across different platforms (Windows, macOS, iOS, etc.).

***

### 🛠️ Creating a Bar Chart (`render barchart`)

**Use when:** You want to **compare values** side-by-side.

***

#### ✨ Example: Top Accounts by Failed Logins

```kql
kqlCopyEditSecurityEvent
| where EventID == 4625
| summarize FailedLogins = count() by Account
| top 10 by FailedLogins
| render barchart
```

**Result:**\
A bar chart showing which accounts had the most failed login attempts.

**Use Case:**

* Spot accounts under attack (brute-force attempts).

***

### 🛠️ Other Chart Types

| Chart Type     | Use Case                                      | Syntax                |
| -------------- | --------------------------------------------- | --------------------- |
| `areachart`    | Area under a line (good for totals over time) | `render areachart`    |
| `columnchart`  | Vertical bars (similar to bar chart)          | `render columnchart`  |
| `scatterchart` | Compare two numeric fields                    | `render scatterchart` |

***

### 📈 Real-World Example: Threat Trends Over Time

**Scenario:**

> Visualize failed login attempts per hour over the past 7 days.

```kql
kqlCopyEditSecurityEvent
| where EventID == 4625
| where TimeGenerated > ago(7d)
| summarize FailedLogins = count() by bin(TimeGenerated, 1h)
| render timechart
```

**Result:**\
You immediately see peaks in failed login activity — maybe spotting a brute-force attack window.

***

### 📝 Mini Practice Exercises

#### 1. Create a Timechart

**Query:** Show heartbeats per hour in the last day.

```kql
kqlCopyEditHeartbeat
| where TimeGenerated > ago(1d)
| summarize Heartbeats = count() by bin(TimeGenerated, 1h)
| render timechart
```

***

#### 2. Create a Piechart

**Query:** Show top 5 operating systems used in the last day.

```kql
kqlCopyEditHeartbeat
| summarize Count = count() by OSName
| top 5 by Count
| render piechart
```

***

#### 3. Create a Barchart

**Query:** Show top 5 accounts with the most successful logins.

```kql
kqlCopyEditSecurityEvent
| where EventID == 4624
| summarize SuccessfulLogins = count() by Account
| top 5 by SuccessfulLogins
| render barchart
```

***

### ⚡ Pro Tips

* **Use `bin()`** when building timecharts — it groups your time series data properly.
* **Use `top`** before rendering piecharts or barcharts to limit to the top N results.
* **Simplify your data before rendering**: Summarize and clean it for clear visuals.
* **Pick the right chart**: Time = timechart, Proportions = piechart, Comparisons = bar/columnchart.

***

### 📢 Key Takeaways

* **`render`** transforms query output into visual charts.
* Use **timecharts** for trends, **piecharts** for proportions, and **barcharts** for comparisons.
* Visualizations are essential for **fast analysis**, **reporting**, and **hunting patterns**.

***

### 🚀 What's Next?

In the next module, you’ll move into **Real-World Scenarios**!

You’ll learn how to:

* Threat hunt with KQL.
* Build monitoring queries.
* Solve practical problems using everything you’ve learned so far.

This is where your KQL skills will **come to life in real investigations**!
