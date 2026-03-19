# SLO Workshop Breakout 3 - Using Grafana Assistant with SLOs

## Introduction
Grafana SLO makes it easy for teams to create, manage, and scale SLOs, SLO dashboards, and error budget alerts, all within Grafana Cloud.

**Why use Assistant?**
1. **Beginner-friendly** - Grafana SLO supports first-time users while creating meaningful SLIs/SLOs with a guided UI that then abstracts managing the backend queries as SLOs continue to be refined.
2. **Supervise the state of your services’ health** - Gain service state visibility through overview visualizations and automated reporting and alerting capabilities.
3. **Scale SLOs as code** - Avoid the daunting task of building hundreds of SLOs completely by UI, Grafana SLO supports provisioning as-code via an API or Terraform.

## Part 1 - Understanding your SLOs with Assistant
Part 3 of lab 2 shows us how to view and monitor SLOs. However, we can also use our friendly neighbourhood Assistant to help here too. Assistant can look at the SLOs and provide a clear breakdown of what each SLO is, how it's performed, group the, explain why they are in their current state and so much more. The options are limited by your imagination.

Go to Grafana, open Assistant and ask it something like:

`What are my SLOs? Give me a breakdown of each SLO, it's remaining error budget and general status`

Note, Assistant is powered by LLMs, it is not deterministic so everyone will get slightly different formatted responses.

### 2.1 - Creating an SLO with Assistant
As mentioned above, Assistant doesn't have a Tool to help you directly create an SLO within the Assistant experience, but it is aware of SLOs, best practices and the SLO app. 
This means we can use Assistant to help guide us. Let's say I want to create a new SLO based on cart conversion of orders, I know I have my two metrics `checkout_orders_total` and `app_cartservice_new_carts_created_total`. Let's ask Assistant to help guide us to create this SLO.
We can ask Assistant something like 

`I'd like to create an SLO of cart conversion to orders group by geography. My metrics are checkout_orders_total and app_cartservice_new_carts_created_total`

![alt text](./images/creating_an_slo.png)

You should get a warning about `geography` labels having a value of `Not Set - Default`. This is totally fine and expected, the reason we use this example here is to show how you can follow up with Assistant. Sometimes it will fix the queries in the numerator and denominator to filter out `Not Set - Default` - sometimes it doesn't.

If yours doesn't, just copy in the queries as is to the SLO UI and it will say something like `Some values in the query exceed 100% (1.0) from the generated query. SLI ratios should typically be between 0-1 (success/total). This may indicate that the query can be finetuned or optimized.`
![alt text](./images/create_slo_error.png)

Copy that error into the Assistant chat and ask it to help you! That is why it's there, to help you. It will then recommend filtering out that label value and all will work.

**That’s the end of this breakout. Thank you for participating.**
