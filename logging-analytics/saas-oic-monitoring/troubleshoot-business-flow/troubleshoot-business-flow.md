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


### Task 2: Understanding the Dashboard Widgets

The Fusion and OIC Process Monitoring Dashboard is organized into multiple tabs with comprehensive widgets for monitoring business processes. Here's a detailed breakdown of the dashboard structure:

#### **Tab 1: OIC Metrics**
**Purpose**: Monitor Oracle Integration Cloud performance and activity

| Widget | Description | Key Metrics | Query Focus |
|--------|-------------|-------------|-------------|
| **OIC Billed Message Count** | Tracks total billed messages over time | Message volume trends, billing metrics | `TotalBilledMessageCount[1h].grouping().count()` |
| **OIC Failed Message Rate** | Monitors integration failure rates | Error percentage, failure trends | `MessagesFailedCount[1h].grouping().count()/MessagesReceivedCount[1h].grouping().count()*100` |
| **Outbound Request Invocation Time** | Measures integration response times | Performance metrics, latency analysis | `OutboundRequestInvocationTime[1h].groupBy("integrationFlowIdentifier").mean()/1000` |

#### **Tab 2: Database Metrics**
**Purpose**: Monitor Autonomous Database performance and health

| Widget | Description | Key Metrics | Query Focus |
|--------|-------------|-------------|-------------|
| **ADBs Availability** | Database uptime and availability | System availability percentage | `DatabaseAvailability[auto].groupBy(resourceName).mean()` |
| **ADBs CPU Time** | CPU utilization monitoring | Resource consumption trends | `CPUTime[auto].groupBy(resourceName).mean()` |
| **Average Active Sessions** | Database connection monitoring | Concurrent user sessions | `AverageActiveSessions[auto].groupBy(resourceName).mean()` |
| **Query Latency** | Database query performance | Response time analysis | `QueryLatency[auto].groupBy(resourceName).mean()` |
| **Connection Latency** | Database connection performance | Connection speed metrics | `ConnectionLatency[auto].groupBy(resourceName).mean()` |
| **Current Logons** | Active database connections | User activity monitoring | `CurrentLogons[auto].groupBy(resourceName).mean()` |

#### **Tab 3: OIC Milestones**
**Purpose**: Track integration flow execution milestones and performance

| Widget | Description | Key Metrics | Query Focus |
|--------|-------------|-------------|-------------|
| **Oracle Integration 3: Action Types** | Distribution of integration actions | Action type breakdown | `'Action Type' in (Invoke, Log, Notification, Raise_error, Submitnow, Stop, Switch, Raise_new_error, Receive)` |
| **Milestones Summary** | Integration milestone overview | Milestone completion rates | `stats count(Action) as Milestones by Action` |
| **Milestones Trend** | Milestone execution trends over time | Performance patterns | `timestats count(Action) as Milestones by Action` |
| **OIC - Error Percentage** | Integration error rate analysis | Error rate by integration | `ErrorRate = ErrorExec / TotalExec * 100` |

#### **Tab 4: Fusion Apps User Access**
**Purpose**: Monitor Fusion Applications user activity and access patterns

| Widget | Description | Key Metrics | Query Focus |
|--------|-------------|-------------|-------------|
| **Oracle Fusion Apps: Login Events** | User login activity tracking | Login success/failure rates | `'Log Source' = 'Fusion Apps: Sign-in Sign-Out Activity'` |
| **Oracle Fusion Apps: Unique Users** | Active user count monitoring | User engagement metrics | `distinctcount('User ID') as 'Unique Users'` |
| **Oracle Fusion Apps: Successful Logins** | Successful authentication tracking | Login success trends | `Status != fail` |
| **Oracle Fusion Apps: Failed Login Attempts** | Failed login monitoring | Security and access issues | `Status = fail` |
| **Oracle Fusion Apps: Top Users** | Most active users analysis | User activity patterns | `stats count('User ID') as abc by 'User ID'` |
| **Oracle Fusion Apps: Failed Logins Top users** | Users with most failed attempts | Security risk analysis | `stats count('User ID') as 'Failed Logins' by 'User ID'` |

#### **Tab 5: ESS Jobs**
**Purpose**: Monitor Enterprise Scheduler Service job execution

| Widget | Description | Key Metrics | Query Focus |
|--------|-------------|-------------|-------------|
| **Fusion ESS Requests** | Total ESS job requests | Job volume metrics | `distinctcount('Request ID') as Requests` |
| **Fusion ESS States** | Job execution states | Job status distribution | `stats distinctcount('Request ID') as Requests by 'State Description'` |
| **Fusion ESS Applications** | Job distribution by application | Application workload analysis | `stats distinctcount('Request ID') as Requests by Application` |
| **Fusion ESS Jobs by Product Heatmap Schedule** | Job scheduling patterns | Resource utilization heatmap | `timestats count('Request ID') as logrecords by Product` |

#### **Tab 6: Transaction Performance**
**Purpose**: Analyze end-to-end transaction execution and performance

| Widget | Description | Key Metrics | Query Focus |
|--------|-------------|-------------|-------------|
| **Transaction Execution Times and Milestones Chronology** | Complete transaction timeline | Execution duration, milestone tracking | `link 'OPC Request ID', 'Transaction ID'` |
| **Fusion ESS Jobs Summary** | Comprehensive job performance analysis | Job execution metrics, performance trends | `link 'Request ID'` with detailed job analysis |

#### **Tab 7: Transaction Tracking Fields**
**Purpose**: Monitor business process tracking and correlation

| Widget | Description | Key Metrics | Query Focus |
|--------|-------------|-------------|-------------|
| **Tracking Fields and Values Grouped by Transactions** | Business process tracking | Transaction correlation, field mapping | `link 'Transaction ID', Key, Value, Integration` |
| **Transaction Details ERP-PO** | Purchase Order transaction details | PO-specific tracking fields | `link 'Transaction ID', Key, Value, Integration` |
| **Transaction Details ERP-PO-Sequence** | PO process sequence tracking | Process flow analysis | `sequence name = 'Sequence of Events'` |
| **RF: AIW25 OIC Integration Analysis** | Integration flow analysis | Flow execution patterns | `link 'OPC Request ID'` with flow analysis |


## Task 2: Comprehensive Monitoring Dashboard

### PO Flow Overview Dashboard

**Monitor Key Trends**:
- PO processing volume trends
- Error rate trends by system
- Performance degradation patterns
- Resource utilization trends

1. **PO Flow Timeline**: Shows the complete journey of a PO across all systems
2. **Status Distribution**: Pie chart showing PO status distribution
3. **System Performance**: Bar chart showing average response times by system
4. **Error Summary**: Table showing error counts by system and type
5. **Trading Partner Activity**: Chart showing B2B communication activity


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
