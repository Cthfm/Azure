# Advanced KQL Techniques

### 🛠️ The `let` Statement

**`let`** allows you to **define variables** inside your query.

* Helps break long queries into **logical sections**.
* Makes complex queries **easier to read and troubleshoot**.

***

#### ✨ Basic `let` Example

```kql
kqlCopyEditlet FailedLogins = SecurityEvent
| where EventID == 4625;
FailedLogins
| summarize Count = count() by Account
| order by Count desc
```

**Explanation:**

* The **first part** defines a search for all failed login events and **stores it** in a variable called `FailedLogins`.
* The **second part** uses the `FailedLogins` variable to summarize the number of failures per account.

***

#### ✨ Why Use `let`?

| Without `let`          | With `let`                  |
| ---------------------- | --------------------------- |
| Big, messy query       | Clean, readable sections    |
| Hard to troubleshoot   | Easy to modify small parts  |
| Repeating same filters | Define once, use many times |

***

### 🛠️ Conditional Logic with `case()`

**`case()`** is like an **IF-THEN-ELSE** statement inside KQL.

It allows you to assign **different values** depending on conditions.

***

#### ✨ Basic `case()` Example

**Scenario:**

> Label operating systems as "Windows", "Linux", or "Other".

```kql
kqlCopyEditHeartbeat
| extend OSLabel = case(
    OSName contains "Windows", "Windows",
    OSName contains "Linux", "Linux",
    "Other"
)
| project Computer, OSName, OSLabel
```

**Explanation:**

* If OSName contains "Windows", label it "Windows."
* If OSName contains "Linux", label it "Linux."
* Otherwise, label it "Other."

***

#### ✨ Real-World Use Case: Threat Level Tagging

```kql
kqlCopyEditSecurityEvent
| extend ThreatLevel = case(
    EventID == 4625, "Failed Login",
    EventID == 4624, "Successful Login",
    "Other Event"
)
| project TimeGenerated, Account, EventID, ThreatLevel
```

**Result:**\
Each event is tagged with a **human-readable Threat Level**.

***

### 🛠️ Working with Arrays using `mv-apply`

You’ve seen `mv-expand` — but sometimes you want to **apply a function** to every item in an array and produce results.

This is where **`mv-apply`** shines.

***

#### ✨ `mv-apply` Basic Example

**Scenario:**

> You have a list of IP addresses, and you want to turn each into a separate row while keeping the original context.

```kql
kqlCopyEditdatatable(Computer:string, IPs: dynamic)
[
    "Computer1", dynamic(["192.168.1.1", "10.0.0.1"]),
    "Computer2", dynamic(["172.16.0.5"])
]
| mv-apply IPAddress = IPs on (
    project Computer, IPAddress
)
```

**Result:**

* One row per Computer + IPAddress pair.
* Preserves Computer name while expanding each IP.

***

#### ✨ When to Use `mv-apply`?

| Use Case                                               | Example                         |
| ------------------------------------------------------ | ------------------------------- |
| Expand arrays while keeping parent data                | List of users in an alert       |
| Apply filters or transformations to each array element | IP filtering, entity extraction |

***

### 📈 Real-World Example: Advanced Modular Query

**Scenario:**

> Find failed logins, tag them by threat level, and show the latest event per account.

```kql
kqlCopyEditlet FailedLogins = SecurityEvent
| where EventID == 4625;
FailedLogins
| extend ThreatLabel = case(
    Account contains "admin", "Admin Account",
    Account contains "guest", "Guest Account",
    "Regular Account"
)
| summarize LastSeen = max(TimeGenerated) by Account, ThreatLabel
| order by LastSeen desc
```

**Explanation:**

* Filter failed logins into a variable.
* Tag accounts based on risk (admin, guest, or regular).
* Summarize by account and show the last seen time.

***

### 📝 Mini Practice Exercises

#### 1. Define a `let` Variable

**Query:** Define a set of Linux computers.

```kql
kqlCopyEditlet LinuxComputers = Heartbeat
| where OSName contains "Linux";
LinuxComputers
| project Computer, OSName
| take 10
```

***

#### 2. Create a Threat Label

**Query:** Label events based on success or failure.

```kql
kqlCopyEditSecurityEvent
| extend LoginResult = case(
    EventID == 4624, "Success",
    EventID == 4625, "Failure",
    "Other"
)
| project TimeGenerated, Account, EventID, LoginResult
| take 10
```

***

#### 3. Expand an Array with `mv-apply`

**Query:** Expand multiple IP addresses per computer.

```kql
kqlCopyEditdatatable(Computer:string, IPs: dynamic)
[
    "ServerA", dynamic(["192.168.1.10", "10.1.1.10"]),
    "ServerB", dynamic(["172.16.5.10"])
]
| mv-apply IPAddress = IPs on (
    project Computer, IPAddress
)
```

***

### ⚡ Pro Tips

* **Use `let`** to make queries modular and easy to update.
* **Use `case()`** to build readable and dynamic labels inside your queries.
* **Use `mv-apply`** when working with complex arrays and you need to transform them intelligently.
* **Break long queries into logical parts** so your future self (and your team) will thank you!

***

### 📢 Key Takeaways

* **`let`** simplifies big queries by creating variables.
* **`case()`** adds flexible logic for labeling or categorizing data.
* **`mv-apply`** works great when dealing with arrays.
* Advanced techniques make your queries **more powerful**, **easier to maintain**, and **professional-grade**.
