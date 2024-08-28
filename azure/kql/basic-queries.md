# Basic Queries

## **Overview:**

The following section goes over the basic queries that can be run within KQL.&#x20;

## **Data Retrieval**

* **Selecting Columns**
  * Use the `project` operator to select specific columns from a table.
  *   Example with security logs:

      ```kusto
      AzureActivity
      | project TimeGenerated, Computer, EventID, AccountName, LogonType
      ```
* **Filtering Rows with `where` Clause**
  * The `where` clause filters rows based on a condition.
  *   Example to filter security logs for logon events:

      ```kusto
      SecurityEvent
      | where EventID == 4624
      ```
  * Multiple conditions can be combined using logical operators (`and`, `or`, `not`).
  *   Example to filter for successful logons by a specific user:

      ```kusto
      SecurityEvent
      | where EventID == 4624 and AccountName == "jdoe"
      ```

## **Sorting and Limiting Data**

* **Using `sort by`**
  * The `sort by` operator sorts the results by one or more columns.
  *   Example to sort security logs by time:

      ```kusto
      SecurityEvent
      | sort by TimeGenerated desc
      ```
* **Limiting Results with `top` and `take`**
  * The `top` operator returns the top N rows based on a specific column.
  *   Example to get the top 10 most recent security events:

      ```kusto
      SecurityEvent
      | top 10 by TimeGenerated desc
      ```
  * The `take` operator returns the first N rows from the result set.
  *   Example to take the first 5 rows from the security event log:

      ```kusto
      SecurityEvent
      | take 5
      ```

## **Aggregating Data**

* **Using `summarize` for Aggregations**
  * The `summarize` operator is used for data aggregation, such as calculating sums, averages, counts, etc.
  *   Example to count the number of events per computer:

      ```kusto
      SecurityEvent
      | summarize EventCount = count() by Computer
      ```
  * Aggregations can be grouped by one or more columns.
  *   Example to count the number of logon events per account:

      ```kusto
      SecurityEvent
      | where EventID == 4624
      | summarize LogonCount = count() by AccountName
      ```
* **Common Aggregation Functions**
  *   `sum()`: Calculates the sum of values.

      ```kusto
      SecurityEvent
      | summarize TotalEvents = sum(EventCount)
      ```
  *   `count()`: Counts the number of rows.

      ```kusto
      SecurityEvent
      | summarize TotalEvents = count()
      ```
  *   `avg()`: Calculates the average of values.

      ```kusto
      SecurityEvent
      | summarize AvgEventDuration = avg(Duration)
      ```
  *   `min()`, `max()`: Finds the minimum and maximum values.

      ```kusto
      SecurityEvent
      | summarize MinTime = min(TimeGenerated), MaxTime = max(TimeGenerated)
      ```
