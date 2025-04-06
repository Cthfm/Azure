# Joins

### 🛠️ The `join` Operator

The `join` operator **combines rows from two tables** based on a common field.

| Term             | Meaning                                                                |
| ---------------- | ---------------------------------------------------------------------- |
| **Left table**   | Your main query (before `join`)                                        |
| **Right table**  | The table you are joining to the main query                            |
| **Common field** | The field that links the two tables (like `Computer`, `Account`, etc.) |

***

#### ✨ Basic `join` Example

**Scenario:**

> Join heartbeat data with security events where the computer name matches.

```kql
kqlCopyEditHeartbeat
| join kind=inner (
    SecurityEvent
) on Computer
```

**Breakdown:**

* Start with `Heartbeat`.
* **Inner join** with `SecurityEvent` where **Computer** matches in both tables.

***

#### 🔥 Types of Joins

| Type         | Meaning                                              | Use Case                                         |
| ------------ | ---------------------------------------------------- | ------------------------------------------------ |
| `inner`      | Only matching records from both tables               | Typical analysis                                 |
| `leftouter`  | All records from the left table + matches from right | Keep all left table data, add right if available |
| `rightouter` | All records from the right table + matches from left | (Rare) Keep all right table data                 |
| `fullouter`  | All records from both tables                         | See everything, matched or not                   |

***

#### ✨ Example: `leftouter` Join

**Scenario:**

> List all computers that sent a heartbeat, and show if they had any security events.

```kql
kqlCopyEditHeartbeat
| join kind=leftouter (
    SecurityEvent
) on Computer
```

* All Heartbeat records are kept.
* SecurityEvent data is added when a match is found.

***

### 🛠️ Optimizing Joins with `project`

When doing joins, **always use `project`** to select only the fields you need from each table — otherwise, the output can get **huge and messy**.

**Example:**

```kql
kqlCopyEditHeartbeat
| project Computer, TimeGenerated
| join kind=inner (
    SecurityEvent
    | project Computer, EventID, Account
) on Computer
```

**Tip:**\
Always **limit fields inside your join** to make the results clean and fast!

***

### 🛠️ The `union` Operator

The `union` operator **stacks rows from multiple tables together**.

**Think of it like:**

> Glueing tables on top of each other — not side-by-side like `join`.

***

#### ✨ Basic `union` Example

**Scenario:**

> Combine two tables of logs into one.

```kql
kqlCopyEditunion Heartbeat, SecurityEvent
| take 10
```

* Takes rows from both `Heartbeat` and `SecurityEvent`.
* Useful when different sources report the same kind of event.

***

#### ✨ Real-World Example: Alerts from Multiple Sources

**Scenario:**

> Combine alerts from Defender and Sentinel into one hunting query.

```kql
kqlCopyEditunion DefenderAlerts, SentinelIncidents
| where TimeGenerated > ago(7d)
| project TimeGenerated, AlertName, Severity, Status
```

**Result:**\
All alerts in one view, regardless of source.

***

### 📈 Real-World Example: Devices with Heartbeats but No Sign-Ins

**Scenario:**

> Find devices that have recent heartbeats but no user sign-ins in the last 7 days.

```kql
kqlCopyEditHeartbeat
| where TimeGenerated > ago(7d)
| project Computer
| join kind=leftouter (
    SigninLogs
    | where TimeGenerated > ago(7d)
    | project Computer, UserPrincipalName
) on Computer
| where isnull(UserPrincipalName)
```

**Explanation:**

* Start with devices sending heartbeats.
* Join sign-ins by Computer name.
* Filter where there was **no sign-in** (UserPrincipalName is null).

***

### 📝 Mini Practice Exercises

#### 1. Basic Join

**Query:** Join `Heartbeat` and `SecurityEvent` on `Computer`.

```kql
kqlCopyEditHeartbeat
| join kind=inner (
    SecurityEvent
) on Computer
| take 10
```

***

#### 2. Leftouter Join

**Query:** List all Heartbeat computers, and show any matching security events.

```kql
kqlCopyEditHeartbeat
| join kind=leftouter (
    SecurityEvent
) on Computer
| take 10
```

***

#### 3. Union Two Tables

**Query:** Combine `Heartbeat` and `SigninLogs` into one table.

```kql
kqlCopyEditunion Heartbeat, SigninLogs
| take 10
```

***

#### 4. Clean Join with Project

**Query:** Cleanly join Heartbeat and SecurityEvent showing only Computer and EventID.

```kql
kqlCopyEditHeartbeat
| project Computer, TimeGenerated
| join kind=inner (
    SecurityEvent
    | project Computer, EventID
) on Computer
| take 10
```

***

### ⚡ Pro Tips

* **Always use `project` inside a join** to avoid pulling in unnecessary data.
* **Use `inner` joins** for matching-only results, **leftouter** joins when you want everything from the left side.
* **Use `union`** when the schema (fields) between tables is similar.
* Always **check if you need a join or a union** — they solve different problems.

***

### 📢 Key Takeaways

* **`join`** = combine data **side-by-side** based on matching fields.
* **`union`** = combine data **top-to-bottom** from multiple tables.
* Choose the right **join type** depending on whether you want all data or only matches.
* Always **project the fields you need** to keep your queries fast and clean.
