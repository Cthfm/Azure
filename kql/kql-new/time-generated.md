# Time Generated

### 🛠️ The `TimeGenerated` Field

In most Azure tables (like `Heartbeat`, `SecurityEvent`, `SigninLogs`), there’s a field called **`TimeGenerated`**.

* It records the **exact time** the event occurred.
* Almost all time-based analysis will start with `TimeGenerated`.

***

### 🛠️ Filtering by Time with `ago()`

The **`ago()`** function returns a timestamp that is **X time ago from now**.

| Example    | Meaning      |
| ---------- | ------------ |
| `ago(1h)`  | 1 hour ago   |
| `ago(24h)` | 24 hours ago |
| `ago(7d)`  | 7 days ago   |

***

#### ✨ Filtering Events in the Last 24 Hours

**Example:** Get all events from the last 24 hours.

```kql
kqlCopyEditSecurityEvent
| where TimeGenerated > ago(24h)
```

***

#### ✨ Filtering Events in the Last 7 Days

```kql
kqlCopyEditSigninLogs
| where TimeGenerated > ago(7d)
```

**Tip:**\
Use **`ago()`** instead of manually typing dates whenever possible.

***

### 🛠️ Grouping Time with `bin()`

You can use **`bin()`** to group time into **fixed-size intervals**.

| Example                  | Meaning                   |
| ------------------------ | ------------------------- |
| `bin(TimeGenerated, 1h)` | Group into 1-hour buckets |
| `bin(TimeGenerated, 1d)` | Group into 1-day buckets  |

***

#### ✨ Example: Logins per Hour

```kql
kqlCopyEditSigninLogs
| where TimeGenerated > ago(1d)
| summarize Logins = count() by bin(TimeGenerated, 1h)
| order by TimeGenerated asc
```

**Result:**\
See how many logins occurred during each hour.

**Tip:**\
This is how you **build time charts** later!

***

### 🛠️ Calculating Differences with `datetime_diff()`

**`datetime_diff()`** lets you calculate the **difference between two times**.

| Example                                       | Meaning                          |
| --------------------------------------------- | -------------------------------- |
| `datetime_diff('hour', end_time, start_time)` | How many hours between two times |
| `datetime_diff('day', end_time, start_time)`  | How many days between two times  |

***

#### ✨ Example: How Many Hours Between First and Last Event

```kql
kqlCopyEditSecurityEvent
| summarize FirstEvent = min(TimeGenerated), LastEvent = max(TimeGenerated)
| extend HoursBetween = datetime_diff('hour', LastEvent, FirstEvent)
```

**Result:**\
You’ll see how many hours passed between the first and last event in the dataset.

***

### 🛠️ Extracting Parts of a Date with `datetime_part()`

**`datetime_part()`** lets you extract **pieces of a timestamp**, like:

* Year
* Month
* Day
* Hour
* Minute

***

#### ✨ Example: Extract the Hour of the Event

```kql
kqlCopyEditSecurityEvent
| extend EventHour = datetime_part("hour", TimeGenerated)
| project TimeGenerated, EventHour
```

**Result:**\
You’ll see what hour (0–23) each event happened.

**Use Case:**\
Build patterns like “Most logins happen at 2 AM!”

***

### 📈 Real-World Example: Failed Logins Over Time

**Scenario:**

> Find how many failed logins happened each hour in the last day.

```kql
kqlCopyEditSecurityEvent
| where EventID == 4625 // Failed login
| where TimeGenerated > ago(1d)
| summarize FailedLogins = count() by bin(TimeGenerated, 1h)
| order by TimeGenerated asc
```

**Result:**\
You get a nice time series of failed logins.
