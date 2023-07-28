# SLO Workshop Breakout 2 - SLO Creation in Grafana Cloud

## Introduction
Grafana SLO is a tool designed to assist in building and managing Service Level Objectives. In this workshop, we'll explore how to establish an SLO for a web application, and how to set up SLO alert rules to keep us informed of any discrepancies in our targets.

Those who have not yet implemented SLOs could find value in this hands-on experience. Once incorporated, SLOs can help manage alert volumes and provide useful insights into the trade-off between innovation and reliability.

Follow the below steps to generate SLOs for your first SLO using [Grafana SLO](https://grafana.com/docs/grafana-cloud/alerting-and-irm/slo/).

## Part 1 - Initializing Grafana SLO
```Step 1:``` Login to Grafana Cloud

```Step 2:``` On the left-side menu, expand out 'Alerts & IRM' and select 'SLO'

![Navigation Menu IRM](img/breakout_2/navigation_menu_irm.png)

This should take you to the SLO application within Grafana.

```Step 3:``` Click 'Initialize Grafana SLO' 

*note: If you do not see this button your Grafana SLO is already initialized, and you can advance to the next step.*

![Initialize SLO App](img/breakout_2/initalize_slo_app.png)

## Part 2 - Creating and Configuring SLOs with Grafana SLO
In this section you will walk through the process of creating your SLOs.

```Step 1:``` click 'Create SLO'

![Create SLO button](img/breakout_2/create_slo_button.png)

### 2.1 - Define SLI
We will start by defining your time window. The default time window is set to 28 days, which captures the same number of weekends regardless of the day of the week. This is a better way to account for traffic variation over weekends than a 30-day SLO. In this lab we will leave the time window to the default.

Once we have input our time window, it is time to choose a metric-based query type. In Grafana SLO, there are two types of metric-based queries: Ratio and Advanced.

- *Ratio queries* are the simplest type of metric-based query. They consist of two metrics: a success metric and a total metric. The success metric is the number of events that meet a certain condition, such as HTTP requests without errors. The total metric is the total number of events. The ratio query then calculates the percentage of successful events as a number between 0 and 1.

- *Advanced queries* are more complex than ratio queries. They can use a variety of functions and operators to calculate the SLI. For example, an advanced query could calculate the mean time to first byte (TTFB) for HTTP requests.

The main difference between ratio and advanced queries is the complexity of the calculation. Ratio queries are simpler and easier to understand, but they may not be as flexible as advanced queries. Advanced queries can be used to calculate more complex SLIs, but they can be more difficult to understand and debug.

```Step 2:``` Under the section Start querying select 'Ratio'

```Step 3:``` Set 'Success Metric' to
```
traces_spanmetrics_calls_total{status_code!="STATUS_CODE_ERROR", service="mythical-server"}
``` 
This metric accounts for all HTTP calls without errors.

```Step 4:``` Set 'Total Metric' to 
```
traces_spanmetrics_calls_total{service="mythical-server"}
```
This metric accounts for all HTTP calls for the mythical app, regardless of errors.

```Step 5:``` Set 'Grouping' to
```
http_target
```
This label will be used to distinguish between different types of HTTP endpoints (/account, /cart, /fastcache, /health, /payment, /login, etc.).

```Step 6:``` Click 'Run queries'
You should see a auto-generated SLI query and its visual representation.

![Define SLI Tab](img/breakout_2/define_sli_tab.png)

```Step 7:``` Click 'Set target and error budget'

### 2.2 - Set target and error budget
```Step 8:``` Set the desired SLO target as 95%, resulting in an error budget of 5%

![Define Error Budget Tab](img/breakout_2/define_error_budget_tab.png)

```Step 9:``` Click 'Add name and description'

### 2.3 - Add name and description
```Step 10:``` Set SLO name to
```
MB-Error-Free-HTTP-Request-Success-Rate
```
```Step 11:``` Set SLO description to
```
Success rate target for error-free HTTP requests in the 'Mythical Beasts'
```
![Add Name Tab](img/breakout_2/add_name_tab.png)

```Step 12:``` Click 'Add SLO alert rules'

### 2.4 - Add SLO alert rules

```Step 13:``` Check the ‘Add SLO alert rules’ checkbox

![Alert Rule Tab](img/breakout_2/alert_rule_tab.png)

This auto generates 2 types of alerts based upon the configured SLO:
- *Fast-burn* - When we are depleting through our error budget extremely fast as compared to our targets set in step 3b. This would typically mean relevant teams would get notified in an expedient manner and they’d need to focus on increasing the reliability of the service.
- *Slow-burn* - When we are depleting through our budget slowly. It still requires attention but we don’t need to deprioritize everything else and work on a fix.

*Note: you can configure these alerts to be routed to various [contact points](https://grafana.com/docs/grafana/latest/alerting/alerting-rules/manage-contact-points/configure-integrations/). For fast-burn alert rules, we suggest using a paging service, such as Grafana OnCall or Pagerduty. For slow-burn alert rules, we suggest opening a ticket in Jira, ServiceNow, Github, or another ticketing system.*

```Step 14:``` Click 'Review SLO'

### 2.5 - Review SLO
```Step 15:``` Once you have ensured everything is accurately configured. Click 'Save and view all SLOs'

![Review SLO](img/breakout_2/review_slo.png)

## Part 3 - Monitoring SLO Performance and Error Budget Depletion
Once the newly configured SLO is in place, give it around 2-4 minutes. This pause allows the Grafana dashboard to start populating with data specific to the SLO, reflecting in most, if not all, panels.

```Step 1:``` refresh page and then click 'View dashboard'

![SLO Dashboard](img/breakout_2/slo_dashboard.png)

```Step 2:``` change the time window to be 'Last 5 minutes'

![SLO Dashboard TW](img/breakout_2/slo_dashboard_tw.png)

Based upon the http_target selection in the top left, you would see different SLI, error budget and corresponding burn rate values for each endpoint or the aggregate (all).

![SLO Dashboard 1](img/breakout_2/slo_dashboard_1.png)


In the snapshot below, /account endpoint is not adhering to the target SLO of 95% at the moment and thereby depleting through the error budget faster than we’d like. This information is appropriately color coded in these dashboards to help interpret the current state quickly.

![SLO Dashboard 2](img/breakout_2/slo_dashboard_2.png)

That’s the end of this breakout. Thank you for participating.
