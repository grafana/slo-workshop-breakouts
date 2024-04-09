# Lab 2 - Leveraging OSS Tooling (Sloth) to Define and Implement SLOs in Grafana

In this lab, we will create SLO yaml defintion files, use [Sloth](https://sloth.dev/) to generate recording rules for Mimir, import them into Mimir using [Mimirtool](https://grafana.com/docs/mimir/latest/manage/tools/mimirtool/), and then finally track our SLOs using Grafana dashboards.

## Pre-requisites

- Familiarity with Linux shell and editors like vim or Nano/Pico. The workshop involves editing files in the WebTerminal using `pico` (recommended for simplicity) or `vim`.
- Access to the WebShell via the link in your workshop email (username and password provided).

## Lab Steps
### Part 1 - Login into the Webterminal

1. Navigate to the webterminal url and then when prompted input your provided username and password. 

Once you are successfully logged in, you will be able to view your home directory by running the command `ls`. Your directory will include a few things:
   * A `sloth` directory containing its executable and a example file.  This was created on your behalf by copying the relevant files from the Sloth repo at [`https://github.com/slok/sloth.git`](https://github.com/slok/sloth.git); downloading the sloth executable from [here](https://github.com/slok/sloth/releases/tag/v0.11.0), and then performing a `chmod +x` to the executable file and renaming the file to `sloth`.
   * A `mimirtool` binary. We downloaded Mimirtool from the Assets section of [Mimir's latest release page](https://github.com/grafana/mimir/releases). Mimir documentation can be found [here](https://grafana.com/docs/mimir/latest/operators-guide/tools/mimirtool/).

as well as some other files that will be used during the lab.

### Part 2 - Create SLO files based on existing examples from Sloth

Now we are going to modify [sloth's getting started template](https://sloth.dev/examples/default/getting-started/).

1. In the WebShell, run:
   ```bash
   cp ./sloth/examples/getting-started.yml ./sloth/examples/mythical.yml
   pico ./sloth/examples/mythical.yml
   ```

1. In this source file, we need to edit many of the definitions.

   a. **version**: `prometheus/v1` -> We will keep this definition as our application metrics are Prometheus-based.

   b. **service**: `myservice` -> Let's change this value to our service name, `mythical-beasts`

   c. **labels**: `owner`, `repo`, and `tier`.  These labels are added to our recording rules.
      - For now, let's delete the `repo` line.
      - Keep the line with `tier` as-is (as mythical beasts is a tier 2 application).
      - Change the value of `owner` from `myteam` to your first initial and last name.
      - Add a new label-value pair called `type: "slo"`(horizontally indented the same as your existing labels).  This will allow us to find our SLO definitions in production more easily in the Grafana Alerting UI.

   d. Next are the **slos**.  Like with this example, we are going to stick with just one SLO - a request/error rate SLO - but our SLO target is going to be much lower.
      - Change the comment from `We allow failing (5xx and 429) 1 request every 1000 requests (99.9%).` to: `We allow failing (5xx and 429) 1 of every 20 requests (95%).`.
      - Since this SLO will be for the login endpoint only, change the name from "requests-availability" to `login-availability`
      - Change the objective from 99.9 to `95.0`.
      - Keep the **description** as-is.  This description does not generate any output.

1. We now get to the two **sli** values driving the SLO. 

Sloth is a ratio-based SLO tool, and we need to define two SLIs: (1) our error count and (2) our total count.  The ratio of these two SLIs is our error or failure rate.

   a. We must edit the formula `sum(rate(http_request_duration_seconds_count{job="myservice",code=~"(5..|429)"}[{{.window}}]))` to match how our application is capturing error percentages today. We are using the [metrics generator](https://grafana.com/docs/tempo/latest/metrics-generator/span_metrics/) in tempo to generate RED metrics off our span data.
   
   b. Let's start with the `/login` http_target first. In the WebShell copy and paste this formula into the **error_query** field:

      ```
      sum by (http_target)(increase(traces_spanmetrics_calls_total{service_name="mythical-server",http_target=~"/login", status_code="STATUS_CODE_ERROR"}[{{.window}}]))
      ```

   - If you are curious, we leave the `sum by http_target` in the formula because we have multiple pods supporting the application, and so those metrics need to be aggregated.
   - We also use a `[{{.window}}]` notation for the time range because it is a variable in Sloth. Sloth fills this value in for each of the recording rules it creates for each of our time windows: 5m, 30m, 1h, 2h, 6h, 1d, 3d, 30d.

   c. Copy and paste this formula into the **total_query** field. Notice the only difference between this formula and the error_query formula is the status_code NOT(!) empty:

      ```
      sum by (http_target)(increase(traces_spanmetrics_calls_total{service_name="mythical-server",http_target=~"/login", status_code!=""}[{{.window}}]))
      ```

1. Now that our SLIs are defined, we need two minor edits to our alerting section:

    a. Change the alerting **name** to ```MythicalBeastsHighErrorRate-login```

    b. For alerting labels, keep the existing `category: "availability"` key value pair.  Add a new label-value pair called `type: "slo"` (horizontally in line with your existing label).  This will allow us to find our SLO definitions in production more easily in the Grafana Alerting UI.

    c. Change the alert annotations **summary** from `"High error rate on 'myservice' requests responses"` to `"High error rate on Mythical Beast login request responses"`

    d. Delete the last 8 lines (a 4-line `page_alert` block and a 4-line `ticket_alert` block). This allows you to set custom tags for "page" versus "ticket" types of alerts as mentioned in the presentation.  You will see that page versus ticket alert types are automatically defined and appropriately tagged with the label, `sloth_severity`, without adding extra labels to our definition.

1. Finally, save the code you’ve just added by typing **Ctrl-O** and then quit Pico with **Ctrl-X**. If you don’t save, you’ll be first asked if you want to save the file if you just hit **Ctrl-X**.

7. We are now ready to run Sloth.  From command line, run the following command:
    ```bash
    ./sloth/sloth generate -i ./sloth/examples/mythical.yml > ./mythical-beasts-SLO-rules.yml
    ```

Assuming you have no errors, your output file (`mythical-beasts-SLO-rules.yml`) will look similar to the structure (but not content) found in Sloth's online documentation [here](https://sloth.dev/examples/default/getting-started/) (click on the "Generated" tab).
![sloth-documentation](./images/sloth-documentation.png)
We can now import your SLO rules into Grafana Cloud!  But first, we need to download an API key for data transmission.

### Import SLO Alerts and Recording rules into Grafana Cloud

We have supplied credentials for you so you can import the SLO alerts and recording rules into Grafana Cloud. You can also use mimirtool to upload this to your self hosted prometheus instance. 

1. Run the `get-credentials.sh` script:
      ```bash
      ./get-credentials.sh
      ```
      This will give you three fields with associated values:
      * `slug` - The slugname
      * `tenantId` - The metrics tenant ID for Grafana Cloud
      * `apiKey` - The API key to use with Grafana Cloud

2. Using your slo rules file, your mimirtool executable, slug name, tenant ID and api key, import your SLO recording rules and alerts:
    ```bash
    ./mimirtool rules load ./mythical-beasts-SLO-rules.yml --address=<slug> --id=<tenantId> --key=<apiKey>
    ```
    Be sure to use the full value for each, including the inverted commas (`"`).

 3. Assuming there were no errors, go to your Grafana UI tab, and on the left side menu, hover over **Alerting** and then click on **Alert rules**.

    a. You should see your recording rules as well as your alerts listed.  To see your recording rules, use the "Search by label" capability by typing in `label:sloth_slo=login-availability`.  Results similar to the picture below should appear. (You may need to click the **>** next to each rule group to view all the rules.) You have two sets of recording rules:
    - `sloth-slo-meta-recordings-mythical-beasts-login-availability` - the meta recording rules
    - `sloth-slo-sli-recordings-mythical-beasts-login-availability` - the SLI/SLO recording rules

    While the meta recording rules are fairly simplistic, expand the first SLI/SLO recording rule by clicking on the **>** next to it.  As you can see in the picture below, Sloth created this complex formula on your behalf.

    ![recording-rules](./images/recording-rules.png)

    b. As for alerts generated, two multi-time window, multi-burn rate alerts are generated.  To see your alert rules, use the "Search by label" capability by typing in ```label:category=availability```.  Results similar to the picture further below should appear. Click the **>** next to the rule group to see the rules, and expand each rule to see its detail.

    One rule is for slow burns over longer periods of time, which has a tag of ```sloth_severity=ticket```. The second alert is for higher burn rates over shorter periods of time and has a tag of ```sloth_severity=page```.  These tags can be used to route your SLO alerts to say, Slack, for an SRE to investigate immediately if you are experiencing high burn rates, and then route your slow burn rate alerts to your ticketing system for scheduled analysis.

    ![slo-alerts](./images/slo-alerts.png)

 ### Import an SLO dashboard into Grafana Cloud

 If we'd like to visualize this data over time and see how we are doing against our objectives, we can import a dashboard into Grafana Cloud.

Steps to Import:

1. Go to the Dashboards (4 squares) icon in the left menu and click on **+ Import**.

2. In the Import via grafana.com field, type in `14348` and then click *Load*.  For the `prometheus` data source, select `grafanacloud-<username>-prom` where `<username>` is the username for your instance, and then select "Import".
 If you were to add more SLOs for our application, the dashboard would look similar to this below.

    ![dashboard](./images/slo-dashboard.png)

__Note__: These are the out-of-box dashboards provided by Sloth [here](https://sloth.dev/introduction/dashboards/). There are two details to be aware of:
* You will see no burn rates in the top graphs if you do not enter in a value.  If you enter a burn rate of `0.01` into the field `Min Burning Rate` like is shown in the picture above, you will see all of the burn rates for your SLOs.

* You will likely see a graph that says `No Data` in one of the graphs like this (in red):
![dashboard](./images/no-data.png)
If you click on the top of the No Data panel and then click `Edit`, you will see a complicated formula that uses a time range of `32d`.  In the picture below, I have changed that SLO window to `31d`, and now you see that the data is populating correctly for this panel.  After editing your SLO window to *31d*, click on `Apply` in the top right to apply your change.
![dashboard](./images/no-data-fix.png)

3. An overview dashboard is also available. Go to the Dashboards (4 squares) icon in the left menu and click on **+ Import**.

4. In the Import via grafana.com field, type in `14643` and then click **Load**. For the `prometheus` data source, select `grafanacloud-<username>-prom` where `<username>` is the username for your instance, and then select "Import".

An example representation is below where a second SLO has been added for effect.  The reason I find the overview valuable is that it visualizes a state timeline on your behalf for all of your services. So, you can see exactly when your burn rates were running hot.  One thing that can be adjusted on this dashboard is that while we have a datasource variable dropdown at the top of the dashboard, that variable is not propagated to its panels.  This is an easy fix, but not something that we will cover in this workshop.
![dashboard](./images/slo-overview.png)

**[END OF HANDS-ON PORTION OF THE WORKSHOP]**

#### Optional Activities for Early Finishers:
- **Explore More:** If you're interested in learning more about the application used in this lab, [click here](./supplementary_materials/setting_the_scene.md) for additional information.

- **Extra Credit Challenge:** For students who like to work ahead and have already completed the current lab tasks, consider testing your skills with Sloth configuration files. You can create additional Service Level Objectives (SLOs) for other application endpoints such as `/account`, `/health`, `/cart`, `/fastcache`, and `/payment`. Don't worry if you don't complete this during class time. You can refer to an example configuration file [here](./supplementary_materials/examples/slo-config-availability-only.yml). For further instructions, [click here](./supplementary_materials/continuation_of_lab.md).
