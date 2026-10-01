# Module 4 – Ops Insights Service

## Introduction

Explore an optional capability using Demo Mode: Exadata Capacity Planning, SQL Explorer, ADDM Spotlight, Exadata Cost Management, or dashboards. Choose an area and record a finding or recommended action.

Estimated Time: 30 minutes

### Objectives

Depending on the option you choose:

- Identify Exadata capacity risks or unused resources.
- Create a fleet SQL visualization with SQL Explorer.
- Prioritize performance findings using ADDM Spotlight.
- Explore Exadata resource usage and cost allocation.
- Use dashboards to drill into database and SQL performance.

### Prerequisites

- An OCI account with access to Ops Insights.
- Ops Insights Demo Mode enabled through **Ops Insights → Overview**.
- Database Management Demo Mode enabled if you choose to explore Database Management dashboards.

## Task 9: Explore an Optional Service Capabilities

Choose one module for the 90-minute event version. The remaining modules can be completed in a self-paced session.

### Option A: Exadata Capacity Planning

Exadata Insights extends capacity planning from individual databases to Exadata systems, hosts, VM clusters, and storage servers. It helps you identify an Exadata resource that is over-utilized, growing, forecasted to constrain demand, or materially under-used.

1. Open **Exadata Insights** and review the aggregate fleet view, current utilization, and forecast utilization.
    ![Left Pane](images/exadata-insights-ocw.png)
    ![Left Pane](images/exadata-systems-ocw.png)
    ![Branch Exadata aggregate view](images/branch-aggregate-view-ocw.png)
2. Select a populated Exadata system and review **Rack and Key Metrics**.
    ![Left Pane](images/current-forecast-ocw.png)
    ![Left Pane](images/rack-and-key-metrics-ocw.png)
3. Open **Metrics by Database** and compare CPU usage by database and host.
    ![Left Pane](images/metrics-by-database-ocw.png)
    ![Left Pane](images/metrics-by-database-host-ocw.png)
4. Use **Allocation (CPU)** for size and **Usage Change (%)** for color to identify growing or shrinking consumers.
    ![Left Pane](images/max-allocation-usage-change-ocw.png)
5. Drill into host and database trend/forecast views.
    ![Left Pane](images/trend-host-cpu-ocw.png)
    ![Branch host and database trend](images/branch-trend-host-database-ocw.png)
6. Select **Usage (average active CPU)** for size and **Utilization (%)** for color, then enable **Show Unused Capacity**.
    ![Left Pane](images/exa-unused-host.png)
7. Repeat the unused-capacity view by VM cluster.
    ![Left Pane](images/exa-unused-vmcluster.png)
8. Open **Metrics by Host** and review aggregate CPU trends and forecasts.
    ![Left Pane](images/metrics-by-host-ocw.png)
    ![Left Pane](images/cpu-all-hosts-ocw.png)
9. Open **Exadata Storage Server** and compare individual data series with aggregate series and forecast.
    ![Left Pane](images/exadata-storage-server-ocw.png)
    ![Left Pane](images/exadata-storage-server1-ocw.png)
    ![Left Pane](images/exadata-storage-server2.png)

    **Module output:** Identify one Exadata host, VM cluster, database, or storage resource that is over-utilized, growing, forecasted to constrain demand, or under-used.

### Option B: SQL Explorer

Use SQL Explorer to create a focused fleet visualization and understand how query dimensions affect the result.

1. Open **SQL Insights → SQL Explorer**.
    ![Branch SQL Explorer entry](images/branch-sql-explorer.png)
2. In basic mode, run a validated query that aggregates CPU time or elapsed time by database and SQL ID.
    ![Branch SQL Explorer main view](images/branch-sql-explorer-main.png)
3. Sort by descending resource use and limit the result set.
    ![Branch SQL query](images/branch-sql-query.png)
4. Display the result as a stacked bar chart.
    ![Branch SQL query table](images/branch-sql-query-table.png)
    ![Branch SQL query visualization](images/branch-sql-query-visual.png)
5. Open **Advanced** mode and inspect available views, columns, and sample queries.
    ![Branch SQL Explorer advanced mode](images/branch-sql-explorer-advanced.png)
    ![Branch SQL Explorer advanced main view](images/branch-sql-explorer-advanced-main.png)
6. Modify one filter or grouping and rerun the visualization.
    ![Branch clear SQL Explorer query](images/branch-sql-explorer-clear.png)
    ![Branch second SQL query](images/branch-sql-query1.png)
    ![Branch second SQL query table](images/branch-sql-query-table1.png)
    ![Branch second SQL query visualization](images/branch-sql-query-visual1.png)
    ![Branch SQL Explorer available views and columns](images/branch-sql-explorer-view-queries.png)
    ![Branch SQL Explorer view queries](images/branch-view-queries.png)
    ![Branch SQL Explorer column details](images/branch-sql-column-details.png)

    **Module output:** Produce one fleet SQL visualization and explain the query dimensions used.

### Option C: ADDM Spotlight

ADDM Spotlight provides a strategic view of findings and recommendations over time. Use the aggregated evidence to prioritize chronic or high-impact issues rather than reacting to a single event without context.

1. Open **Database Insights → ADDM Spotlight**.
    ![Branch ADDM Spotlight entry](images/branch-addm-spot01.png)
2. Review the database listing, findings count, maximum overall impact, and most frequent category.
    ![Branch ADDM Spotlight landing page](images/branch-addm-spot02.png)
3. Filter by time range and search for a database.
4. Open a populated database.
    ![Branch ADDM Spotlight database findings](images/branch-addm-spot03.png)
5. Review the summary timeline and determine whether the finding or recommendation is recurring or intermittent.
    ![Branch ADDM Spotlight detailed findings](images/branch-addm-spot04.png)
6. Review **Findings** and **Recommendations**, comparing frequency, average active sessions, maximum impact, and recommendation benefit when available.
    ![Branch ADDM recommendations](images/branch-addm-reco.png)
7. Review **Database Parameters** for high-impact parameters, changes during the reporting period, ADDM-recommended changes, and non-default values.
    ![Branch ADDM database parameters](images/branch-addm-dbpars.png)
8. Compare an impactful finding with the DBM or OPSI evidence.

    **Module output:** Record the highest-impact finding and the recommended next action.

### Option D: Exadata Cost Management

Exadata Cost Management connects resource usage with actual or attributed cost. Groupings, tags, sunburst views, trends, and table data help explain ownership and identify optimization or showback/chargeback opportunities.

1. Open **Exadata Insights → Exadata Cost Management**.
    ![Branch Exadata Cost Management](images/branch-opsi-chargeback-main.png)
2. Select a populated Exadata system.
    ![Branch Exadata Cost Management details](images/branch-opsi-chargeback-details.png)
3. Review actual cost, attributed cost, VM cluster CPU utilization, and the database table.
4. Set **Primary grouping** to **CostCenter** and **Secondary grouping** to **Environment**, when available.
    ![Branch primary grouping](images/branch-primary-grouping.png)
    ![Branch secondary grouping](images/branch-opsi-chargeback-grouping.png)
5. Select a chart segment to filter the database table to one cost center or environment.
    ![Branch cost center filter](images/branch-cost-center-01.png)
6. Review usage and charge trends, then switch to table data.
    ![Branch time range](images/branch-time-range.png)
    ![Branch VM cluster color grouping](images/branch-vm-cluster-button.png)
    ![Branch usage and charge trends](images/branch-trend-charts.png)
    ![Branch table data selection](images/branch-select-show-table.png)
    ![Branch cost management table](images/branch-table.png)
7. Inspect how OCI standard or free-form tags support cost-center or line-of-business hierarchy and filtering.
    ![Branch deselected cost center](images/branch-deselect-test-vmc1.png)

    **Module output:** Identify a cost center or environment with a resource-usage or chargeback optimization opportunity.

### Option E: Ops Insights or Database Management Dashboards

Out-of-the-box dashboards shorten the path from a fleet-level signal to database and SQL analysis by providing reusable views and drill-downs.

1. Open **Dashboards** and review the out-of-the-box dashboard list.
    ![Branch dashboards landing page](images/branch-opsi-dash-main.png)
    ![Branch dashboards list](images/branch-opsi-left-dash.png)
2. Open **(Demo) SQL Insights – Fleet Analysis**, when available.
    ![Branch Demo SQL Insights Fleet Analysis dashboard](images/branch-opsi-demo-insights-fleet-analysis.png)
3. Select the **Degrading SQL** insight to list affected databases.
    ![Branch degrading SQL insight](images/branch-opsi-degrading-sql.png)
4. Open a database analysis view.
    ![Branch database with degraded SQL](images/branch-opsi-db-with-degraded-sql.png)
    ![Branch database analysis](images/branch-opsi-db-analysis.png)
5. Select **Degraded plan changes**, when available.
    ![Branch degraded plan changes](images/branch-opsi-degraded-plan.png)
6. Open a SQL analysis view for one SQL ID.
    ![Branch SQL ID analysis](images/branch-opsi-sql-id-analysis.png)

**Module output:** Explain how a saved dashboard shortens the path from a fleet signal to database and SQL investigation.

### If your data does not match the example

Demo Mode data is curated and can change over time. Follow the evidence in the current environment rather than waiting for a fixed value or exact count.

- If **CRMCDB** is absent or empty, select another database with populated charts.
- If Performance Hub, SQL Monitoring, AWR Explorer, or ADDM Spotlight is unavailable for the selected database, return to Fleet Summary and select another populated target.
- If the exact DBM SQL ID is not available in SQL Insights, use a high-impact SQL statement with a related degradation, plan-change, CPU, or I/O pattern.
- If a forecast view is empty, use a populated aggregate CPU or storage view and document the visible trend.
- If Exadata data is unavailable, complete Database Capacity Planning and treat Exadata modules as optional.
- ADDM Spotlight has no populated target, continue with SQL Insights or Capacity Planning.
- If dashboard names or drill-down counts differ, use the closest populated out-of-the-box SQL Insights dashboard.

Do not use a fabricated target, finding, metric, SQL ID, or forecast value.

## Acknowledgements

- **Author** - Derik Harlow
- **Contributors** - Sriram Vrinda, Derik Harlow, Kranti Agrawal, Shaickmohamed Sirajudeen
