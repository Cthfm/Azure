# Advanced Query Techniques

## **Joins and Unions**

* **Inner Join**
  * The `join` operator combines rows from two tables based on a related column between them.
  *   Example: Join `SecurityEvent` and `SigninLogs` to find login events and their details.

      ```kusto
      SecurityEvent
      | where EventID == 4624
      | join kind=inner (SigninLogs | project SigninTime, UserPrincipalName, IPAddress) on $left.AccountName == $right.UserPrincipalName
      | project TimeGenerated, Computer, AccountName, IPAddress, SigninTime
      ```
* **Left Join**
  * A `leftouter` join includes all rows from the left table and the matched rows from the right table. If there is no match, the result is `null` on the side of the right table.
  *   Example: Left join `SecurityEvent` with `ThreatIntelligence` to find logins and match with threat intelligence data.

      ```kusto
      SecurityEvent
      | where EventID == 4624
      | join kind=leftouter (ThreatIntelligence | project IPAddress, ThreatType) on $left.IPAddress == $right.IPAddress
      | project TimeGenerated, Computer, AccountName, IPAddress, ThreatType
      ```
* **Union Operations**
  * The `union` operator combines the results of two or more tables.
  *   Example: Combine `SecurityEvent` and `SigninLogs` for comprehensive analysis.

      ```kusto
      union SecurityEvent, SigninLogs
      ```

## **Subqueries and Nested Queries**

* **Writing Subqueries**
  * Subqueries are queries within queries and are used to break down complex operations.
  *   Example: Subquery to filter security events for a specific user and then summarize.

      ```kusto
      let UserLogons = SecurityEvent | where AccountName == "jdoe" and EventID == 4624;
      UserLogons
      | summarize LogonCount = count() by Computer
      ```
* **Using Nested Queries for Complex Data Retrieval**
  * Nested queries can be used to perform multiple transformations in a single query.
  *   Example: Nested query to find the peak login times for a user.

      ```kusto
      SecurityEvent
      | where AccountName == "jdoe" and EventID == 4624
      | summarize LogonCount = count() by bin(TimeGenerated, 1h)
      | where LogonCount > 10
      ```

## **String Operations**

* **String Functions**
  *   `substring()`: Extracts a substring from a string.

      ```kusto
      SecurityEvent
      | project ShortComputerName = substring(Computer, 0, 5)
      ```
  *   `trim()`: Removes leading and trailing spaces from a string.

      ```kusto
      SecurityEvent
      | project TrimmedAccountName = trim(" ", AccountName)
      ```
  *   `replace()`: Replaces occurrences of a substring with another substring.

      ```kusto
      SecurityEvent
      | project AnonymizedIP = replace(".", "[dot]", IPAddress)
      ```
* **Pattern Matching with `extract` and `parse`**
  *   `extract()`: Extracts a substring using a regular expression.

      ```kusto
      SecurityEvent
      | project Domain = extract("@(.+)", 1, AccountName)
      ```
  *   `parse()`: Parses a string using a custom format.

      ```kusto
      SecurityEvent
      | parse AccountName with "prefix" ParsedName "suffix"
      ```
