# Project and Extend Deep Dive

### The Project Operator (Deep Dive)

You’ve already seen `project` before. Let’s go deeper.

| Feature        | What it Does                        | Example     |
| -------------- | ----------------------------------- | ----------- |
| `project`      | Select only specific fields to show | \`Heartbeat |
| `project-away` | Remove specific fields              | \`Heartbeat |

#### Basic `project`

**Example:** Select only Computer and OSName fields.

```kql
kqlCopyEditHeartbeat
| project Computer, OSName
```

**Result:** Cleaner output showing just the fields you care about.

***

### Project Away

Instead of listing fields you want to keep, you can remove fields you don't want.

**Example:** Remove the TimeGenerated field.

```kql
kqlCopyEditHeartbeat
| project-away TimeGenerated
```

***

### The Order By Operator

**`order by`** sorts your results based on one or more fields.

| Sorting             | Syntax                    |
| ------------------- | ------------------------- |
| Ascending (default) | `order by FieldName`      |
| Descending          | `order by FieldName desc` |

#### Basic Sorting

**Example:** Sort computers by time they last sent a heartbeat.

```kql
Heartbeat
| order by TimeGenerated desc
```

**Result:** Most recent heartbeats at the top.

#### Sorting Multiple Fields

You can sort by multiple fields by listing them.

**Example:** Sort first by OSName, then by Computer.

```kql
Heartbeat
| order by OSName asc, Computer asc
```

***

### The `extend` Operator

**`extend`** lets you create a **new column** that is **calculated** from existing data.

#### Basic `extend`

**Example:** Create a field that shows if a heartbeat is older than 1 hour.

```kql
kqlCopyEditHeartbeat
| extend IsOldHeartbeat = TimeGenerated < ago(1h)
| project Computer, TimeGenerated, IsOldHeartbeat
```

**Result:**

* `true` if the heartbeat is older than 1 hour ago.
* `false` otherwise.

#### Combining `extend` and `project`

You can create new fields and then decide exactly what to show.

**Example:** Create a custom status.

```kql
Heartbeat
| extend Status = case(OSName contains "Windows", "Windows Machine", OSName contains "Linux", "Linux Machine", "Other")
| project Computer, OSName, Status
```

**What’s happening?**

* If OSName contains "Windows" → Status = "Windows Machine"
* If OSName contains "Linux" → Status = "Linux Machine"
* Otherwise → Status = "Other"
