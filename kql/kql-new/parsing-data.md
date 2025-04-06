# Parsing Data

### 🛠️ Parsing Data with `parse`

**`parse`** breaks apart structured strings into **new columns**.

***

#### ✨ Example: Parsing a URL

Suppose you have a URL field like:

```
arduinoCopyEdithttps://example.com/path/file.html
```

You can extract the domain:

```kql
kqlCopyEditdatatable(URL:string)
[
    "https://example.com/path/file.html"
]
| parse URL with "https://" Domain "/" *
| project Domain
```

**Result:**\
New column `Domain = example.com`

***

#### ✨ How `parse` works:

* It **matches the pattern** you provide.
* It **pulls out** the parts you want into new fields.
* The `*` wildcard at the end means "and ignore the rest."

**Tips:**

* `parse` works well when your data has a **consistent structure** (e.g., all rows look similar).

***

### 🛠️ Extracting Data with `extract`

**`extract`** uses **regular expressions (regex)** to pull data out of text.

It’s more powerful than `parse` but requires understanding regex.

***

#### ✨ Example: Extract a Domain with Regex

```kql
kqlCopyEditdatatable(URL:string)
[
    "https://example.com/path/file.html"
]
| extend Domain = extract(@"https://([^/]+)", 1, URL)
| project Domain
```

**Explanation:**

* `https://([^/]+)` captures everything after `https://` until the next `/`.
* `1` refers to the **first capture group**.

***

#### ✨ When to use `extract` over `parse`?

| Use       | When                          |
| --------- | ----------------------------- |
| `parse`   | Data has a consistent format  |
| `extract` | Data is messy or inconsistent |

***

### 🛠️ Parsing JSON with `parse_json`

**`parse_json`** turns a **JSON string** into **a dynamic object** you can query.

***

#### ✨ Example: Parsing JSON Data

Suppose a field has this JSON string:

```json
jsonCopyEdit{"user":"admin", "role":"owner"}
```

You can parse it like this:

```kql
kqlCopyEditdatatable(jsonField: string)
[
    '{"user":"admin", "role":"owner"}'
]
| extend parsed = parse_json(jsonField)
| project User = parsed.user, Role = parsed.role
```

**Result:**

* `User = admin`
* `Role = owner`

***

#### ✨ Use Case

Parsing alerts or audit logs that store their **details as JSON** inside a field.

**Common in:**

* Microsoft Sentinel
* Defender for Endpoint
* Azure Activity Logs

***

### 🛠️ Expanding Arrays with `mv-expand`

Sometimes a field contains **multiple values** (an array).

**`mv-expand`** breaks the array into **individual rows**.

***

#### ✨ Example: Expanding an Array

```kql
kqlCopyEditdatatable(Users: dynamic)
[
    dynamic(["user1", "user2", "user3"])
]
| mv-expand Users
| project Users
```

**Result:**\
Each user appears on a separate row!

***

#### ✨ Real-World Use Case

**Microsoft Sentinel Alerts** often have `Entities`, a field containing an array of users, IPs, or machines involved in an incident.

`mv-expand` helps you **analyze each entity individually**.

***

### 🛠️ Splitting Strings with `split`

**`split`** divides a string into parts **based on a separator** (like `/`, `,`, or `:`).

***

#### ✨ Example: Splitting a File Path

```kql
kqlCopyEditdatatable(FilePath: string)
[
    "C:/Program Files/Example/file.txt"
]
| extend Parts = split(FilePath, "/")
| project Drive = Parts[0], Folder = Parts[1], SubFolder = Parts[2], FileName = Parts[3]
```

**Result:**

* Drive = `C:`
* Folder = `Program Files`
* SubFolder = `Example`
* FileName = `file.txt`

***

#### ✨ Real-World Example

Splitting a full path, URL, or email address into components like:

* Domain
* Username
* File name
* File extension

***

### 📈 Real-World Example: Parse, Split, and Expand

**Scenario:**

> You receive logs with a full URL, and you want to extract the domain and file name.

```kql
kqlCopyEditdatatable(URL:string)
[
    "https://example.com/path/file.html"
]
| parse URL with "https://" Domain "/" Path
| extend PathParts = split(Path, "/")
| extend FileName = tostring(PathParts[-1])
| project Domain, FileName
```

**Result:**

* `Domain = example.com`
* `FileName = file.html`



### ⚡ Pro Tips

* Use **`parse`** when the structure is predictable.
* Use **`extract`** when the data is messy and needs regex magic.
* Use **`parse_json`** for logs or alerts that store rich JSON details.
* Use **`mv-expand`** to break apart arrays and analyze individual items.
* Use **`split`** to divide long strings into smaller, meaningful parts.

***

### 📢 Key Takeaways

* **`parse`**, **`extract`**, **`parse_json`**, **`mv-expand`**, and **`split`** are your **power tools** for working with messy or complex fields.
* Mastering data transformation allows you to **analyze deeply** and **hunt threats** effectively.
* You can unlock **hidden insights** by parsing, splitting, and expanding your data.

