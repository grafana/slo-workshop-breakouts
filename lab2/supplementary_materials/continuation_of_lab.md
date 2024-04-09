### Import more SLOs

Now that we understand how to (a) properly format a Sloth file; (b) use Sloth to generate our rules file; and (c) import those rules using Mimirtool, it is time to add import more SLOs to save ourselves some time as the process is repetitive.  We will now import two sets of SLOs: availability and latency-based.  We will import both

#### Generate and import the remainder of your SLOs

1. We are now ready to run Sloth.  From command line, run the following two commands:
    ```
    ./sloth/sloth generate -i ./sloth/examples/slo-config-availability-only.yml > ./SLO-availability.yml
    ./sloth/sloth generate -i ./sloth/examples/slo-config-latency.yml > ./SLO-latency.yml
    ```

    We can now import your SLO rules into Grafana Cloud.  We will re-use your API key for the import process.

2. If you do not have them already, get the relevant credentials for Grafana Cloud:
    ```bash
    ./get-credentials.sh
    ```

3. Using your two SLO rule files, your mimirtool executable, slug name, tenant ID and api key, import your SLO recording rules and alerts with the following two commands:
    ```bash
    ./mimirtool rules load ./SLO-availability.yml --address=<slug> --id=<tenantId> --key=<apiKey>
    ./mimirtool rules load ./SLO-latency.yml --address=<slug> --id=<tenantId> --key=<apiKey>
    ```
    Be sure to use the full value for each, including the inverted commas (`"`).

3. Assuming there were no errors, go to your Grafana UI browser tab, and on the left side menu, hover over **Alerting** and then click on **Alert rules**.  You should see your recording rules as well as your alerts listed.  

4.  View the dashboards and observe that the latency SLOs now appear.  To do this, in the left side menu, hover over **Dashboards** and then click on **Browse** and search for the two dashboards that were imported earlier:

    - On the **High level Sloth SLOs** dashboard, `mythical-beasts-login-latency` should appear in the SLO burn rate timeline and the Budget remaining 30 day window.
    - On the **SLO / Detail** dashboard, you should see a row of panels for `mythical-beasts/login-latency`.
