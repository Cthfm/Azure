# Summarize

### 🛠️ The `summarize` Operator

**`summarize`** groups rows together and applies **aggregations** like counting, averaging, finding minimums, etc.

| Aggregation          | Purpose                          | Example                                    |
| -------------------- | -------------------------------- | ------------------------------------------ |
| `count()`            | Number of rows                   | `summarize count()`                        |
| `countif(condition)` | Count rows that meet a condition | `countif(EventID == 4625)`                 |
| `avg()`              | Average value                    | `avg(CounterValue)`                        |
| `min()` / `max()`    | Smallest / largest value         | `min(TimeGenerated)`, `max(TimeGenerated)` |
| `dcount()`           | Count of distinct values         | `dcount(Account)`                          |

***

#### ✨ Basic `summarize` with `count()`

**Example:** Count the total number of heartbeat events.

```kql
kqlCopyEditHeartbeat
| summarize TotalHeartbeats = count()
```

***

#### ✨ Grouping with `by`

You can group your summarized results by one or more fields.

**Example:** Count the number of heartbeat events **per Computer**.

```kql
kqlCopyEditHeartbeat
| summarize HeartbeatCount = count() by Computer
```

**Result:**\
A list of computers with how many heartbeats each sent.

***

#### ✨ Multiple Aggregations

You can do multiple calculations at once.

**Example:** Count events and find the latest time each computer sent a heartbeat.

```kql
kqlCopyEditHeartbeat
| summarize HeartbeatCount = count(), LastSeen = max(TimeGenerated) by Computer
```

***

### 🛠️ Common Aggregation Functions

#### 1. `count()` - Total number of events

```kql
kqlCopyEditSecurityEvent
| summarize TotalEvents = count()
```

***

#### 2. `avg()` - Average value (e.g., CPU usage)

```kql
kqlCopyEditPerf
| where ObjectName == "Processor" and CounterName == "% Processor Time"
| summarize AvgCPU = avg(CounterValue) by Computer
```

***

#### 3. `min()` / `max()` - Minimum and Maximum

```kql
kqlCopyEditSecurityEvent
| summarize FirstSeen = min(TimeGenerated), LastSeen = max(TimeGenerated) by Account
```

***

#### 4. `dcount()` - Distinct count

**Example:** How many distinct user accounts signed in?

```kql
kqlCopyEditSigninLogs
| summarize UniqueUsers = dcount(UserPrincipalName)
```

***

### 📈 Real-World Example

**Scenario:**

> Find the top 5 computers with the most heartbeat signals.

```kql
kqlCopyEditHeartbeat
| summarize HeartbeatCount = count() by Computer
| order by HeartbeatCount desc
| take 5
```

**Explanation:**

* Group by `Computer`.
* Count how many heartbeat signals each computer sent.
* Sort by `HeartbeatCount` in descending order.
* Take the top 5.

***

### 📉 Aggregating Over Time

You can **bin** data into time intervals for trends (like hourly or daily counts).

#### ✨ Binning with `bin()`

**Example:**

> Count heartbeat signals **per hour**.

```kql
kqlCopyEditHeartbeat
| summarize Count = count() by bin(TimeGenerated, 1h)
| order by TimeGenerated asc
```

**Result:**\
A time series showing heartbeat activity per hour.

**Tip:** `bin()` groups times into neat, regular intervals.
