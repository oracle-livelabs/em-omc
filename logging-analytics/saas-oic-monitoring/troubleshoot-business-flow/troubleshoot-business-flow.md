# Lab 5 - Monitor Business Flow Using Fusion and OIC Process Monitoring Dashboard

## Introduction

This lab demonstrates how to use the Oracle Fusion and OIC Process Monitoring Dashboard to monitor and troubleshoot business flows in real-time. You will learn to leverage pre-built monitoring capabilities to track Purchase Order processes, identify performance bottlenecks, and quickly resolve issues across Fusion Applications and Oracle Integration Cloud.

The Process Monitoring Dashboard provides comprehensive visibility into business process execution, allowing you to monitor end-to-end flows, track business metrics, and receive real-time alerts for process anomalies.

Estimated Time: 30 minutes

### Objectives
In this lab, you will:
- Understand the Fusion and OIC Process Monitoring Dashboard capabilities
- Learn to navigate and interpret dashboard visualizations
- Monitor Purchase Order business flows in real-time
- Troubleshoot business process issues using dashboard insights


## Task 1: Understanding the Fusion and OIC Process Monitoring Dashboard

### Dashboard Overview

The Fusion and OIC Process Monitoring Dashboard provides a centralized view of business process execution across Oracle Cloud services. It offers real-time monitoring capabilities with the following key features:

**Key Dashboard Components:**
- **Process Flow Visualization**: Real-time view of business process execution
- **Performance Metrics**: Response times, throughput, and success rates
- **Error Monitoring**: Real-time error detection and alerting
- **Business Metrics**: PO volume, supplier performance, and processing trends
- **System Health**: Overall system status and availability

### Accessing the Process Monitoring Dashboard

- **Navigate to Oracle Cloud Console**
   - Log in to your Oracle Cloud Infrastructure console
   - Navigate to **Observability & Management** → **Log Analytics**

- **Access Process Monitoring**
   - Click on **Dashboards** in the left navigation menu
   - Select **Fusion and OIC Process Monitoring** from the dashboard list
   - Or create a new dashboard specifically for PO monitoring


## Task 2: Understanding the Dashboard Widgets

The Fusion and OIC Process Monitoring Dashboard provides comprehensive visibility into your business processes through seven specialized tabs. Each widget is designed to monitor specific aspects of your Purchase Order flow and help identify bottlenecks, errors, and performance issues in real-time.

### **Tab 1: OIC Metrics**
**Purpose**: Monitor Oracle Integration Cloud performance and activity for Purchase Order integrations

#### **OIC Billed Message Count**
- **Description**: Tracks the total number of billed messages processed by OIC over time, providing insights into integration volume and usage patterns
- **Business Use**: Monitor PO integration volume trends, identify peak processing times, and track integration usage for capacity planning
- **Key Insights**: 
  - PO integration volume spikes during business hours
  - Seasonal variations in integration traffic
  - Integration usage growth patterns
- **Troubleshooting**: Sudden drops may indicate integration failures; spikes may suggest system overload

#### **OIC Failed Message Rate**
- **Description**: Monitors the percentage of failed integration messages, providing real-time visibility into integration reliability
- **Business Use**: Track PO integration success rates, identify problematic integrations, and ensure business process continuity
- **Key Insights**:
  - Integration failure trends over time
  - Failure rate by integration type
  - Correlation between failures and system load
- **Troubleshooting**: High failure rates indicate integration issues requiring immediate attention

#### **Outbound Request Invocation Time**
- **Description**: Measures the response time for outbound integration requests, helping identify performance bottlenecks
- **Business Use**: Monitor PO integration performance, ensure SLA compliance, and optimize integration response times
- **Key Insights**:
  - Integration response time trends
  - Performance comparison across different integrations
  - Impact of system load on response times
- **Troubleshooting**: High response times may indicate network issues, system overload, or integration design problems

### **Tab 2: Database Metrics**
**Purpose**: Monitor Autonomous Database performance and health supporting Purchase Order processes

#### **ADBs Availability**
- **Description**: Tracks database uptime and availability percentage, ensuring continuous access to PO data
- **Business Use**: Monitor database reliability, ensure business continuity, and track SLA compliance
- **Key Insights**:
  - Database availability trends
  - Planned vs. unplanned downtime
  - Availability by database instance
- **Troubleshooting**: Low availability indicates database issues requiring immediate investigation

#### **ADBs CPU Time**
- **Description**: Monitors CPU utilization across database instances, helping identify resource constraints
- **Business Use**: Track database resource consumption, plan capacity upgrades, and optimize performance
- **Key Insights**:
  - CPU usage patterns during PO processing
  - Resource consumption trends
  - Peak usage identification
- **Troubleshooting**: High CPU usage may indicate inefficient queries or insufficient resources

#### **Average Active Sessions**
- **Description**: Tracks concurrent database connections, providing visibility into user activity and system load
- **Business Use**: Monitor user activity levels, plan for peak usage periods, and ensure adequate connection capacity
- **Key Insights**:
  - User activity patterns
  - Peak usage times
  - Connection pool utilization
- **Troubleshooting**: High session counts may indicate connection leaks or insufficient connection pooling

#### **Query Latency**
- **Description**: Measures database query response times, helping identify slow-performing queries
- **Business Use**: Optimize PO-related queries, improve user experience, and ensure responsive applications
- **Key Insights**:
  - Query performance trends
  - Slow query identification
  - Performance impact of system load
- **Troubleshooting**: High latency indicates query optimization needs or resource constraints

#### **Connection Latency**
- **Description**: Tracks database connection establishment time, monitoring network and authentication performance
- **Business Use**: Ensure fast application startup, monitor network performance, and optimize connection management
- **Key Insights**:
  - Connection performance trends
  - Network latency impact
  - Authentication performance
- **Troubleshooting**: High connection latency may indicate network issues or authentication problems

#### **Current Logons**
- **Description**: Shows active database connections, providing real-time visibility into user activity
- **Business Use**: Monitor active users, track system usage, and ensure proper connection management
- **Key Insights**:
  - Real-time user activity
  - Connection distribution
  - User session patterns
- **Troubleshooting**: Unusual connection patterns may indicate security issues or application problems

### **Tab 3: OIC Milestones**
**Purpose**: Track integration flow execution milestones and performance for Purchase Order processes

#### **Oracle Integration 3: Action Types**
- **Description**: Shows the distribution of different action types within integration flows, providing visibility into integration complexity
- **Business Use**: Understand integration flow structure, identify complex integrations, and optimize flow design
- **Key Insights**:
  - Integration flow complexity
  - Action type distribution
  - Integration design patterns
- **Troubleshooting**: Unusual action distributions may indicate integration design issues

#### **Milestones Summary**
- **Description**: Provides an overview of integration milestone completion rates, showing overall integration health
- **Business Use**: Track integration success rates, identify problematic milestones, and ensure process completion
- **Key Insights**:
  - Milestone completion rates
  - Integration success patterns
  - Process flow efficiency
- **Troubleshooting**: Low milestone completion rates indicate integration failures requiring investigation

#### **Milestones Trend**
- **Description**: Shows milestone execution trends over time, helping identify performance patterns and issues
- **Business Use**: Monitor integration performance trends, identify seasonal patterns, and track improvement efforts
- **Key Insights**:
  - Performance trends over time
  - Seasonal variations
  - Impact of system changes
- **Troubleshooting**: Declining trends indicate deteriorating integration performance

#### **OIC - Error Percentage**
- **Description**: Calculates error rates by integration, providing clear visibility into integration reliability
- **Business Use**: Prioritize integration fixes, track improvement efforts, and ensure business process reliability
- **Key Insights**:
  - Error rates by integration
  - Integration reliability comparison
  - Error trend analysis
- **Troubleshooting**: High error percentages require immediate attention and root cause analysis

### **Tab 4: Fusion Apps User Access**
**Purpose**: Monitor Fusion Applications user activity and access patterns for Purchase Order management

#### **Oracle Fusion Apps: Login Events**
- **Description**: Tracks user login and logout events, providing visibility into application usage patterns
- **Business Use**: Monitor user activity, track application usage, and ensure proper access management
- **Key Insights**:
  - User login patterns
  - Application usage trends
  - Access time distribution
- **Troubleshooting**: Unusual login patterns may indicate security issues or access problems

#### **Oracle Fusion Apps: Unique Users**
- **Description**: Shows the count of unique users accessing the system, indicating user engagement levels
- **Business Use**: Track user adoption, monitor system usage, and plan for user growth
- **Key Insights**:
  - User engagement trends
  - System adoption rates
  - User growth patterns
- **Troubleshooting**: Declining unique users may indicate system issues or user training needs

#### **Oracle Fusion Apps: Successful Logins**
- **Description**: Tracks successful authentication events, monitoring login success rates
- **Business Use**: Ensure user access reliability, track authentication performance, and monitor system health
- **Key Insights**:
  - Login success trends
  - Authentication performance
  - User access patterns
- **Troubleshooting**: Low success rates indicate authentication or system issues

#### **Oracle Fusion Apps: Failed Login Attempts**
- **Description**: Monitors failed login attempts, providing security visibility and access issue detection
- **Business Use**: Enhance security monitoring, identify access issues, and prevent unauthorized access
- **Key Insights**:
  - Security threat patterns
  - Access issue identification
  - User authentication problems
- **Troubleshooting**: High failure rates may indicate security attacks or user credential issues

#### **Oracle Fusion Apps: Top Users**
- **Description**: Shows the most active users, providing insights into system usage patterns
- **Business Use**: Identify power users, monitor system usage, and plan for capacity needs
- **Key Insights**:
  - User activity patterns
  - System usage distribution
  - Power user identification
- **Troubleshooting**: Unusual user activity patterns may indicate security issues or system problems

#### **Oracle Fusion Apps: Failed Logins Top Users**
- **Description**: Identifies users with the most failed login attempts, highlighting potential security risks
- **Business Use**: Enhance security monitoring, identify compromised accounts, and prevent unauthorized access
- **Key Insights**:
  - Security risk identification
  - Account compromise detection
  - User authentication issues
- **Troubleshooting**: High failure counts for specific users require immediate security investigation

### **Tab 5: ESS Jobs**
**Purpose**: Monitor Enterprise Scheduler Service job execution for Purchase Order processing

#### **Fusion ESS Requests**
- **Description**: Tracks total ESS job requests, providing visibility into background job volume
- **Business Use**: Monitor background job activity, track system workload, and plan for capacity needs
- **Key Insights**:
  - Job volume trends
  - System workload patterns
  - Background processing activity
- **Troubleshooting**: Unusual job volumes may indicate system issues or configuration problems

#### **Fusion ESS States**
- **Description**: Shows the distribution of job execution states, providing visibility into job health
- **Business Use**: Monitor job success rates, identify failed jobs, and ensure process completion
- **Key Insights**:
  - Job status distribution
  - Success/failure rates
  - Job execution patterns
- **Troubleshooting**: High failure rates indicate job execution issues requiring investigation

#### **Fusion ESS Applications**
- **Description**: Shows job distribution by application, providing insights into workload distribution
- **Business Use**: Monitor application workload, identify resource-intensive applications, and plan capacity
- **Key Insights**:
  - Application workload distribution
  - Resource usage patterns
  - Application performance trends
- **Troubleshooting**: Unusual workload distribution may indicate application issues or configuration problems

#### **Fusion ESS Jobs by Product Heatmap Schedule**
- **Description**: Provides a heatmap view of job scheduling patterns, showing resource utilization over time
- **Business Use**: Optimize job scheduling, identify resource conflicts, and improve system efficiency
- **Key Insights**:
  - Job scheduling patterns
  - Resource utilization trends
  - Peak usage identification
- **Troubleshooting**: Resource conflicts in the heatmap indicate scheduling optimization needs

### **Tab 6: Transaction Performance**
**Purpose**: Analyze end-to-end transaction execution and performance for Purchase Order processes

#### **Transaction Execution Times and Milestones Chronology**
- **Description**: Provides a complete timeline view of transaction execution, showing all milestones and their timing
- **Business Use**: Track end-to-end PO processing times, identify bottlenecks, and optimize process flow
- **Key Insights**:
  - Complete transaction timeline
  - Milestone execution order
  - Process flow efficiency
- **Troubleshooting**: Long execution times or missing milestones indicate process issues requiring investigation

#### **Fusion ESS Jobs Summary**
- **Description**: Provides comprehensive analysis of job performance, including execution metrics and trends
- **Business Use**: Monitor job performance, identify optimization opportunities, and ensure reliable background processing
- **Key Insights**:
  - Job execution metrics
  - Performance trends
  - Resource utilization
- **Troubleshooting**: Poor job performance indicates resource constraints or configuration issues

### **Tab 7: Transaction Tracking Fields**
**Purpose**: Monitor business process tracking and correlation for Purchase Order transactions

#### **Tracking Fields and Values Grouped by Transactions**
- **Description**: Shows business process tracking fields and their values, enabling transaction correlation
- **Business Use**: Track PO transactions across systems, correlate related processes, and ensure data consistency
- **Key Insights**:
  - Transaction correlation
  - Field mapping accuracy
  - Process flow tracking
- **Troubleshooting**: Missing or incorrect tracking fields indicate integration or configuration issues

#### **Transaction Details ERP-PO**
- **Description**: Provides PO-specific transaction details, showing all tracking fields for Purchase Orders
- **Business Use**: Monitor PO-specific processes, track PO status, and ensure proper PO handling
- **Key Insights**:
  - PO transaction details
  - PO status tracking
  - PO-specific metrics
- **Troubleshooting**: Missing PO details indicate integration or data flow issues

#### **Transaction Details ERP-PO-Sequence**
- **Description**: Shows the sequence of events for PO transactions, providing process flow visibility
- **Business Use**: Understand PO process flow, identify process bottlenecks, and optimize PO handling
- **Key Insights**:
  - PO process sequence
  - Event timing
  - Process flow efficiency
- **Troubleshooting**: Incorrect sequence or missing events indicate process flow issues

#### **RF: AIW25 OIC Integration Analysis**
- **Description**: Provides detailed analysis of OIC integration flows, showing execution patterns and performance
- **Business Use**: Monitor integration flow performance, identify optimization opportunities, and ensure reliable integration
- **Key Insights**:
  - Integration flow patterns
  - Performance analysis
  - Flow execution details
- **Troubleshooting**: Poor integration performance indicates flow design or configuration issues


**Congratulations!** In this lab, you have successfully completed the following tasks:

- Understanding the Fusion and OIC Process Monitoring Dashboard capabilities
- Creating comprehensive monitoring dashboards with detailed visualizations
- Setting up real-time monitoring alerts for critical business processes
- Implementing business metrics tracking and KPI monitoring
- Learning troubleshooting techniques for common PO processing issues
- Applying root cause analysis methods for business flow problems

You now have comprehensive knowledge of how to use the Fusion and OIC Process Monitoring Dashboard to monitor, troubleshoot, and optimize business processes in real-time.

## Learn More

* [Oracle Cloud Infrastructure Log Analytics Documentation](https://docs.oracle.com/en-us/iaas/log-analytics/)
* [Creating Dashboards in Log Analytics](https://docs.oracle.com/en-us/iaas/log-analytics/doc/create-dashboards.html)
* [Setting up Alerts in Log Analytics](https://docs.oracle.com/en-us/iaas/log-analytics/doc/set-up-alerts.html)
* [Oracle Fusion Applications Documentation](https://docs.oracle.com/en/applications/)
* [Oracle Integration Cloud Documentation](https://docs.oracle.com/en/cloud/paas/integration-cloud/)
* [Oracle Integration 3 - Automate ERP Cloud and B2B Integration with Trading Partners](https://livelabs.oracle.com/pls/apex/r/dbpm/livelabs/run-workshop?p210_wid=3803&p210_wec=&session=25827311700854)

## Acknowledgements
* **Author** - Royce Fu, Master Principal Cloud Architect,Kumar Varun, Log Analytics Product Management
* **Contributors** -  Kumar Varun, Royce Fu, Supriya Joshi, Jolly Kundu
* **Last Updated By/Date** - Royce Fu, Sep, 2025
