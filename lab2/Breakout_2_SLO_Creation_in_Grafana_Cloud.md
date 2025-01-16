# SLO Workshop Breakout 2 - SLO Creation in Grafana Cloud

## Introduction
Grafana SLO makes it easy for teams to create, manage, and scale SLOs, SLO dashboards, and error budget alerts, all within Grafana Cloud.

**Problem Statement:**
It’s hard to find an organization today that doesn’t struggle with alerting. Having too many alerts can make it difficult to tell which ones are actually indicating a customer problem. Alert fatigue can also contribute to engineer burnout and increase attrition.

We also see managers and developers struggling to decide on whether to fix bugs or work on that new feature. This can lead to a bad customer experience and it is also why we’re seeing most teams shift away from traditional alerting, towards being SLO driven, where teams get direct visibility into the services that most affect their customer health, and know that if someone is being woken up in the middle of the night, it’s probably for a good reason.

Achieving mature SLO adoption is deceptively difficult though and can require both having the right tools as well as building a collaborative culture around them. 

**Grafana SLO Value Proposition:**
Grafana SLO simplifies SLO management with a Guided UI and Prometheus-less queries, so users can set them up without needing to know PromQL. It auto-generates dashboards and multi-window, multi-burn alerts and supports as-code provisioning by API and Terraform.
Grafana SLOs can tell you that not only tell us that something important is happening, but why. 

**Why would  a user choose to use this feature?**
1. **Beginner-friendly** - Grafana SLO supports first-time users while creating meaningful SLIs/SLOs with a guided UI that then abstracts managing the backend queries as SLOs continue to be refined.
2. **Supervise the state of your services’ health** - Gain service state visibility through overview visualizations and automated reporting and alerting capabilities.
3. **Scale SLOs as code** - Avoid the daunting task of building hundreds of SLOs completely by UI, Grafana SLO supports provisioning as-code via an API or Terraform.

Follow the below steps to generate SLOs for your first SLO using [Grafana SLO](https://grafana.com/docs/grafana-cloud/alerting-and-irm/slo/).

## Part 1 - Initializing Grafana SLO
```Step 1:``` Login to Grafana Cloud

```Step 2:``` On the left-side menu, expand out 'Alerts & IRM' and select 'SLO'

![Navigation Menu IRM](./images/navigation_menu_irm.png)

This should take you to the SLO application within Grafana.

```Step 3:``` Click 'Initialize Grafana SLO' 

*note: If you do not see this button your Grafana SLO app is already initialized, and you can advance to the next step.*

![Initialize SLO App](./images/initalize_slo_app.png)

## Part 2 - Creating and Configuring SLOs with Grafana SLO
In this section you will walk through the process of creating your SLOs.

```Step 1:``` click 'Create SLO'

![Create SLO button](./images/create_slo_button.png)

### 2.1 - Define SLI
We will start by defining your time window. The default time window is set to 28 days. With 28 days instead of 30 days, it will standardize the SLO over a four-week period so we can compare month to month and account traffic variation as you release your feature into production. It is also a good practice and standard to be followed by your SRE organization. In this lab we will leave the time window to the default.

Once we have input our time window, it is time to choose a metric-based query type. In Grafana SLO, there are two types of metric-based queries: Ratio and Advanced.

- *Ratio queries* are the simplest type of metric-based query. They consist of two metrics: a success metric and a total metric. The success metric is the number of events that meet a certain condition, such as requests which complete without errors. The total metric is the total number of events. The ratio query then calculates the percentage of successful events as a number between 0 and 1.

- *Advanced queries* are more complex than ratio queries. They can use a variety of functions and operators to calculate the SLI. For example, an advanced query could calculate the mean time to first byte (TTFB) for HTTP requests.

The main difference between ratio and advanced queries is the complexity of the calculation. Ratio queries are simpler and easier to understand, but they may not be as flexible as advanced queries. Advanced queries can be used to calculate more complex SLIs, but they can be more difficult to understand and debug.

```Step 2:``` Under the section Start querying select **Ratio**

```Step 3:``` Set 'Success Metric' to
```
traces_spanmetrics_calls_total{service="productcatalogservice", status_code!="STATUS_CODE_ERROR", span_kind="SPAN_KIND_SERVER"}
``` 
This metric stores the number of requests handled by our product catalog service, which completed without errors.

```Step 4:``` Set 'Total Metric' to 
```
traces_spanmetrics_calls_total{service="productcatalogservice", span_kind="SPAN_KIND_SERVER"}
```
This metric stores the **total** number of requests handled by our product catalog service, errors included.

```Step 5:``` Set 'Grouping' to
```
span_name
```
This label distinguishes between the different operations being handled by the product catalog service. This is a big differentiator of Grafana SLO: the capability to provide a "group by" label in our SLI definition, which will give us deep insight into which parts of our application are contributing the most to our error burn rate.

```Step 6:``` Click 'Run queries'.  
You should see an auto-generated SLI query and its visual representation.

![Define SLI Tab](./images/bookstore.png)

```Step 7:``` Click 'Set target and error budget' to move to the next step.

### 2.2 - Set target and error budget
```Step 8:``` Set the desired SLO target to **95%**, resulting in an error budget of 5%

![Define Error Budget Tab](./images/define_error_budget_tab.png)

```Step 9:``` Click 'Add name and description'

### 2.3 - Add name and description
```Step 10:``` Set SLO name to
```
<username>-Product-Catalog-Service-Errors
```
```Step 11:``` Set SLO description to
```
Success rate target for error-free requests to the product catalog service
```
Also set the `team_name` to **your username** (then hit Enter to add your entered value.)

And set the `service_name` to **productcatalogservice**.

Choose the folder **Grafana SLO**, or optionally, create your own folder.

These labels allow you to categorize and filter your SLOs in the main SLO list, and do the same for your alerts. The folder option allows you to organize SLO dashboards into folders, for easier viewing by users.

![Add Name Tab](./images/bookstore-slo.png)

```Step 12:``` Click 'Add SLO alert rules' to continue to the next step.

### 2.4 - Add SLO alert rules

```Step 13:``` Check the ‘Add SLO alert rules’ checkbox

![Alert Rule Tab](./images/alert_rule_tab.png)

This auto generates 2 types of alerts based upon the configured SLO:
- *Fast-burn* - When we are depleting through our error budget extremely fast as compared to our targets set in step 3b. This would typically mean relevant teams would get notified in an expedient manner and they’d need to focus on increasing the reliability of the service.
- *Slow-burn* - When we are depleting through our budget slowly. It still requires attention but we don’t need to deprioritize everything else and work on a fix.

*Note: you can configure these alerts to be routed to various [contact points](https://grafana.com/docs/grafana/latest/alerting/alerting-rules/manage-contact-points/configure-integrations/). For fast-burn alert rules, we suggest using a paging service, such as Grafana OnCall or Pagerduty. For slow-burn alert rules, we suggest opening a ticket in Jira, ServiceNow, Github, or another ticketing system.*

```Step 14:``` Click 'Review SLO'

### 2.5 - Review SLO
```Step 15:``` Once you have ensured everything is accurately configured and checked that you have set the target to 95%, click 'Save and view all SLOs'. 

![Review SLO](./images/bookstore-review.png)

## Part 3 - Monitoring SLO Performance and Error Budget Depletion
Once the newly configured SLO is in place, give it around 2-4 minutes. This pause allows the Grafana dashboard to start populating with data specific to the SLO, reflecting in most, if not all, panels.

```Step 1:``` Find your newly-created SLO in the list, and click 'View dashboard'

The dashboard will open. 

```Step 2:``` As the SLO is new and is still recording data, we will change the dashboard time range to ensure we're looking at a time period with complete data. At the top right, use the time picker to **change the time window to _Last 5 minutes_.**

![SLO Dashboard for Product Catalog Service](./images/slo_dashboard.png)

In the dashboard on the left, we have quick visual cues to let us know the current status of our alerts. We also get an overview of the time window and SLO object value, as well as our current SLI, remaining error budget and current burn rate.

```Step 3:``` Use the `span_name` dropdown in the top left, to see the SLI, error budget and corresponding burn rate values for each operation handled by the product catalog service, or you can view the aggregate (all). 

For example, try selecting the `ProductCatalogService/GetProduct` span.

![SLO Dashboard 1](./images/routes.png)

In the screenshot below, the `ProductCatalogService/GetProduct` span may not be adhering to the target SLO of 95% at the moment and thereby depleting through the error budget faster than we’d like. This information is appropriately color coded in these dashboards to help interpret the current state quickly.

A burn rate of 1.0 will consume the entire error budget allotted for our given period (28 days). So we might need to take action, to investigate and fix the errors.

![SLO Dashboard 2](./images/finalec.png)

```Step 4:``` Now try selecting the `ListProducts` span from the span name dropdown. Notice how this service, by constrast, is healthy and free from errors. It has its own, separate error budget and burn rate.

```Step 5:``` Finally, from the span name dropdown, select **all** the options. Notice how the SLI, error budget and panels are recalculated to show the SLO for the service as a whole.

With Grafana Cloud SLO, by simply selecting a metric with appropriate labels, you can easily create both high-level and granular SLOs for all of your services. This gives you immediate visibility into your service health, and lets you focus on what matters most - delivering great experiences to your users, while maintaining a budget for innovation.

**That’s the end of this breakout. Thank you for participating.**
