# Best Practices

### 🛠️ Writing Clean and Readable Queries

Clean code isn’t just for developers — it’s for **KQL** too.

***

#### ✨ 1. Use Line Breaks and Indentation

**Bad:**

```kql
kqlCopyEditSecurityEvent|where EventID==4624|summarize count() by Account|order by count_ desc
```

**Good:**

```kql
kqlCopyEditSecurityEvent
| where EventID == 4624
| summarize LoginCount = count() by Account
| order by LoginCount desc
```

**Tip:**\
✅ Every pipe `|` should start a new line.\
✅ Indent sub-queries or `join` blocks clearly.

***

#### ✨ 2. Use Meaningful Names in `let` Statements

**Bad:**

```kql
kqlCopyEditlet t = SecurityEvent | where EventID == 4625;
t | summarize c = count() by Account
```

**Good:**

```kql
kqlCopyEditlet FailedLogins = SecurityEvent
| where EventID == 4625;
FailedLogins
| summarize FailedLoginCount = count() by Account
```

**Tip:**\
✅ Choose variable names that describe **what the data is**.

***

#### ✨ 3. Comment Your Queries

Use comments (`//`) to explain **why** you are doing something — especially in complex queries.

**Example:**

```kql
kqlCopyEdit// Find accounts with more than 10 failed logins in the past day
SecurityEvent
| where EventID == 4625
| where TimeGenerated > ago(1d)
| summarize FailedAttempts = count() by Account
| where FailedAttempts > 10
```

**Tip:**\
✅ Write comments like you’re helping your future self!

***

### 🛠️ Optimizing Query Performance

Now let’s make your queries faster and lighter.

***

#### ✨ 1. Filter Early

Always **filter your data as early as possible** using `where`.

**Good:**

```kql
kqlCopyEditSecurityEvent
| where EventID == 4624
| project Account, TimeGenerated
```

**Bad (slow):**

```kql
kqlCopyEditSecurityEvent
| project Account, TimeGenerated
| where EventID == 4624
```

**Tip:**\
✅ Filter early to reduce the amount of data that needs processing.

***

#### ✨ 2. Use `project` to Select Only the Fields You Need

Don’t bring back every field if you only need a few.

**Good:**

```kql
kqlCopyEditHeartbeat
| project Computer, TimeGenerated
```

**Bad (slow):**

```kql
kqlCopyEditHeartbeat
// All fields retrieved even if you only use two
```

**Tip:**\
✅ Project early and often to reduce data size.

***

#### ✨ 3. Limit Data with `take`

When testing queries, always use `take` to avoid pulling millions of records.

**Example:**

```kql
kqlCopyEditSecurityEvent
| take 100
```

**Tip:**\
✅ Remove or adjust `take` once you move to production.

***

#### ✨ 4. Summarize Data Before Rendering

If you want a chart, always summarize first — don’t send thousands of raw rows to `render`.

**Good:**

```kql
kqlCopyEditSecurityEvent
| summarize LoginCount = count() by bin(TimeGenerated, 1h)
| render timechart
```

**Bad (slow):**

```kql
kqlCopyEditSecurityEvent
| render timechart
```

**Tip:**\
✅ Always shape your data first!

***

#### ✨ 5. Use `top` to Limit Large Result Sets

When you just need the **top results**, say it clearly with `top`.

**Example:**

```kql
kqlCopyEditSecurityEvent
| summarize LoginCount = count() by Account
| top 10 by LoginCount
```

**Tip:**\
✅ `top` automatically sorts and limits results.

***

### 🛠️ Common Pitfalls to Avoid

| Mistake                                       | Fix                                                  |
| --------------------------------------------- | ---------------------------------------------------- |
| Querying huge tables without a `where` filter | Always add a time filter (`TimeGenerated > ago(7d)`) |
| Pulling all columns unnecessarily             | Use `project`                                        |
| Writing long one-line queries                 | Break into readable blocks                           |
| Skipping comments                             | Explain logic in complex queries                     |
| Not summarizing before rendering a chart      | Always `summarize` first                             |

***

### 📈 Real-World Example: Optimized vs. Unoptimized

**Unoptimized Query:**

```kql
kqlCopyEditSecurityEvent
| where EventID == 4625 or EventID == 4624
| summarize count() by Account, bin(TimeGenerated, 1h)
| order by count_ desc
| render timechart
```

**Optimized Query:**

```kql
kqlCopyEdit// Find failed and successful logins summarized hourly
SecurityEvent
| where EventID in (4624, 4625)
| where TimeGenerated > ago(1d)
| project Account, TimeGenerated, EventID
| summarize Logins = count() by bin(TimeGenerated, 1h)
| order by TimeGenerated asc
| render timechart
```

***

### 📝 Mini Practice Exercises

#### 1. Refactor a Messy Query

**Messy Query:**

```kql
kqlCopyEditSigninLogs|where ResultType==0|summarize count() by UserPrincipalName|order by count_ desc
```

✅ Break it into a clean, readable format.

***

#### 2. Filter Early

Start your query with a time filter to limit the data pulled.

***

#### 3. Project Only Needed Fields

Instead of pulling all fields, project only the important ones.

***

#### 4. Add Comments

Write a small query and add meaningful comments explaining what each step does.

***

### ⚡ Pro Tips

* **Filter early, project early, summarize before visualizing.**
* **Write clean, readable queries** — future you will thank you!
* **Small optimizations add up**, especially when queries run on millions of records.

***

### 📢 Key Takeaways

* Good KQL = **Fast, readable, and maintainable**.
* Always **filter, project, and summarize** before rendering or displaying data.
* **Comment your queries** and **break complex ones into sections**.
* Think about **performance** when writing every query.
