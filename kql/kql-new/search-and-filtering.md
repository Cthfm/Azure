# Search and Filtering

### Searching and Filtering Overview:

The following section goes over searching and filtering commands and how to use them.

### The `where` Operator (Deep Dive)

You already learned that `where` filters data.\
Now let’s look at the full power of `where`.

| Operator             | Meaning               | Example                           |
| -------------------- | --------------------- | --------------------------------- |
| `==`                 | Equal to              | `where Computer == "SRV-01"`      |
| `!=`                 | Not equal to          | `where Computer != "SRV-01"`      |
| `<`, `>`, `<=`, `>=` | Comparisons           | `where EventID >= 5000`           |
| `contains`           | Contains substring    | `where Computer contains "prod"`  |
| `startswith`         | Starts with substring | `where Computer startswith "WEB"` |
| `endswith`           | Ends with substring   | `where Computer endswith "01"`    |
| `in`                 | In a list             | `where EventID in (4624, 4625)`   |
| `!in`                | Not in a list         | `where EventID !in (4634, 4647)`  |

***

### Filtering Multiple Conditions

You can combine filters using:

| Logical Operator | Example                                                          |
| ---------------- | ---------------------------------------------------------------- |
| `and`            | `where OSName contains "Windows" and Computer contains "server"` |
| `or`             | `where Computer contains "prod" or Computer contains "web"`      |

**Example: Find Windows servers named 'prod'**

```kql
Heartbeat
| where OSName contains "Windows" and Computer contains "prod"
| project Computer, OSName
```

#### Using `has` for Whole Word Matching

* `contains` matches **any part** of a word.
* `has` matches **whole words**.

**Example:**

```kql
Heartbeat
| where Computer has "prod"
```

If the computer name is `production-server`, `has` **will** match.\
But if the computer name is `product-server`, `has` **will NOT** match.

***

### The `search` Operator

**`search`** is like a giant "find anywhere" across multiple fields.

It’s useful when:

* You’re **not sure which field** contains the value.
* You want to **search across everything** quickly.

**Example: Search for any entry containing “adminuser”**

```kql
search "adminuser"
```

**Notes:**

* `search` checks all fields in all records.
* It’s **slower** than `where`, so use it carefully.
* Good for **quick investigations**, not optimized queries.

#### ✨ Focused `search`

You can limit `search` to a specific table.

**Example:**

```kql
SecurityEvent
| search "adminuser"
```

This only searches within the **SecurityEvent** table.

***

### The `distinct` Operator

**`distinct`** returns **only unique values** for a given field.

**Example: Find all unique computer names**

```kql
Heartbeat
| distinct Computer
```

**Example: Find all unique operating systems**

```kql
Heartbeat
| distinct OSName
```

***

#### Multiple Fields with `distinct`

You can find unique combinations of fields too.

**Example:**

```kql
Heartbeat
| distinct Computer, OSName
```

This gives you a list of unique **Computer + OSName** pairs.

***

### Putting It All Together

Here’s a real-world style query that **filters**, **searches**, and finds **unique values**:

**Scenario:**

> You want to find all unique computers that had failed logins.

```kql
SecurityEvent
| where EventID == 4625 // Failed login
| project Computer, Account
| distinct Computer
```
