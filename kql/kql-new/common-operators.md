# Common Operators

## Common Operators You'll Use

| Operator  | Purpose                         | Example     |
| --------- | ------------------------------- | ----------- |
| `take`    | Return a limited number of rows | \`Heartbeat |
| `limit`   | Same as `take`                  | \`Heartbeat |
| `project` | Select specific columns         | \`Heartbeat |
| `where`   | Filter rows based on conditions | \`Heartbeat |

You'll use **`take`**, **`limit`**, **`project`**, and **`where`** all the time.

***

### Operator 1: `take` and `limit`

Both `take` and `limit` do the same thing: they quickly grab a set number of results.

**Example:**

```kql
Heartbeat
| take 5
```

* This query will return 5 random entries from the Heartbeat table.

**Why use it?**

* When you first open a new table, you often want a quick look at the data.
* It’s a great way to understand what fields are available.

**Alternative using `limit`:**

```kql
Heartbeat
| limit 5
```

**Tip:** `take` and `limit` are interchangeable.

***

### Operator 2: `project`

**`project`** lets you choose specific columns you want to display.

**Without `project`:**

```kql
Heartbeat
| take 5
```

Shows _everything_ (all columns) — which can be overwhelming!

**With `project`:**

<pre class="language-kql"><code class="lang-kql"><strong>Heartbeat
</strong>| project Computer, TimeGenerated, OSName
| take 5
</code></pre>

You now only see the Computer, TimeGenerated, and OSName columns.

**Why use it?**

* To make your results easier to read.
* To improve performance by only pulling what you need.

***

### Operator 3: `where`

**`where`** lets you **filter** your data.

**Example: Find all computers that contain "server" in their name:**

```kql
Heartbeat
| where Computer contains "server"
```

**Key things about `where`:**

* Case-sensitive: `"server"` and `"Server"` are different unless you use case-insensitive functions.
* Supports many operators: `==`, `!=`, `<`, `>`, `contains`, `startswith`, `endswith`, etc.

**More Examples:**

| Purpose     | Example                           |
| ----------- | --------------------------------- |
| Equals      | `where Computer == "SRV-01"`      |
| Not Equals  | `where Computer != "SRV-01"`      |
| Contains    | `where Computer contains "prod"`  |
| Starts With | `where Computer startswith "WEB"` |
| Ends With   | `where Computer endswith "01"`    |

***

### Putting It All Together

Let's combine everything into a real-world style query:

**Example: Show computers running Linux whose name includes "server":**

```kql
Heartbeat
| where OSName contains "Linux"
| where Computer contains "server"
| project Computer, TimeGenerated, OSName
| take 5
```

**Breakdown:**

1. Start from the Heartbeat table.
2. Filter where OSName contains "Linux".
3. Further filter where Computer contains "server".
4. Only show the columns Computer, TimeGenerated, and OSName.
5. Take 5 results.
