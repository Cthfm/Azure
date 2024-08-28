# Time Series Analysis

## **Time-Based Data Operations**

* **Filtering by Time Ranges**
  *   Use the `where` clause to filter data based on a specific time range.

      ```kusto
      AzureActivity
      | where TimeGenerated between (datetime(2024-01-01) .. datetime(2024-12-31))
      ```
  *   You can also use relative time filters with `ago()`.

      ```kusto
      AzureActivity
      | where TimeGenerated > ago(7d)
      ```

## **Time Series Aggregations**

* **Summarizing Data Over Time Intervals**
  *   The `summarize` operator can be used with time intervals to aggregate data.

      ```kusto
      AzureActivity
      | summarize OperationNameValue = count() by bin(TimeGenerated, 1h)
      ```
  *   Example of summarizing data by day:

      ```kusto
      Azure Activity
      | summarize OperationNameValue = count() by bin(TimeGenerated, 1d)
      ```
* **Using `make-series` for Time Series Data**
  * The `make-series` operator creates a series of data points over a specified time range.
  *   Example:

      <pre class="language-kusto"><code class="lang-kusto">AzureActivity
      <strong>| make-series OperationNameValue = count() on TimeGenerated from ago(30d) to now() step 1d
      </strong></code></pre>

## **Anomaly Detection**

* **Identifying Trends and Anomalies**
  * KQL provides functions for identifying trends and detecting anomalies in time series data.
  *   `series_decompose_anomalies()`: Detects anomalies in a time series.

      ```kusto
      AzureActivity
      | make-series OperationNameValue = count() on TimeGenerated from ago(30d) to now() step 1d
      | extend (Trend, Seasonality, Anomaly) = series_decompose_anomalies(OperationNameValue)
      ```
* **Using Built-in Functions for Anomaly Detection**
  *   `series_outliers()`: Detects outliers in a series.

      ```kusto
      AzureActivity
      | make-series OperationNameValue = count() on TimeGenerated from ago(30d) to now() step 1d
      | extend Anomalies = series_outliers(OperationNameValue, 2)
      ```
