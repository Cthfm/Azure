# KQL Introduction New

## What is KQL?

KQL stands for Kusto Query Language.\
It is a read-only query language designed to:

* Query large amounts of structured, semi-structured, or unstructured data.
* Extract insights quickly and easily.
* Visualize data with charts and graphs.

KQL is designed to work on massive datasets, even when those datasets are constantly updating in real time — perfect for security, monitoring, and troubleshooting tasks.

KQL is NOT used to modify or delete data.\
It's used purely for searching, analyzing, and visualizing data.

***

### Where is KQL Used In Azure?

| Service                  | Purpose                                            |
| ------------------------ | -------------------------------------------------- |
| **Azure Data Explorer**  | Big data analytics and storage                     |
| **Azure Monitor**        | Monitor and analyze metrics and logs               |
| **Azure Log Analytics**  | Search and analyze logs                            |
| **Microsoft Sentinel**   | Threat detection and incident response (SIEM/SOAR) |
| **Application Insights** | Application performance monitoring                 |
| **Defender for Cloud**   | Cloud security monitoring and compliance           |

***

### KQL vs SQL

At a glance, KQL and SQL look similar — **but they are different**.

| Feature             | SQL                            | KQL                                  |
| ------------------- | ------------------------------ | ------------------------------------ |
| **Purpose**         | Manage databases (CRUD)        | Search, analyze, visualize data      |
| **Language Type**   | Read and Write                 | Read-only                            |
| **Main Operations** | SELECT, INSERT, UPDATE, DELETE | Take, Project, Summarize, Render     |
| **Syntax Focus**    | Tables, rows, transactions     | Streaming large events, fast queries |

### Your First KQL Query

Let's run your **first KQL query**!

If you have access to **Azure Portal** and **Log Analytics**, follow along:

#### 1. Open Log Analytics Workspace

* Go to **Azure Portal**.
* Search for and open your **Log Analytics Workspace**.

#### 2. Open Logs

* Click on **Logs** in the left-hand menu.

#### 3. Run This Query:

<pre class="language-kql"><code class="lang-kql"><strong>Heartbeat
</strong>| take 10
</code></pre>

**What does this query do?**

* `Heartbeat` is a **table** that stores health pings from computers or servers.
* `take 10` means "show me 10 random entries."

**Result:**\
You should see a table showing 10 entries with information like `Computer`, `TimeGenerated`, and `OSName`.

***

### How a Basic KQL Query Works

**Every KQL query has a basic structure:**

```plaintext
TableName
| operator1
| operator2
| ...
```

* **Start with a Table:** Data always comes from a table (like `Heartbeat`, `SecurityEvent`, `SigninLogs`).
* **Pipe Data:** Use the `|` symbol to apply operators that filter, sort, transform, and summarize the data.

**Query Structure**

**Bucket of raw logs**

`|`  **Filter important logs**&#x20;

&#x20;`|` **Summarize insights** →&#x20;

`|` **Visualize as a chart**
