## Setting the Scene (Optional)
We have just instrumented our cutting-edge critical business application, Mythical Beasts, and now would like to use SLOs to help the organization decide on whether to innovate faster and develop new Mythical Beasts features, or work on Service Stability and Performance optimization.

Since we already have rolled out the application to early access customers, we are tracking application performance, errors, and overall load in the `Mythical Inc., Top Level Endpoints RED (MLT)` dashboard in our Grafana instance.

1. Log into your Grafana instance by going to the Grafana website using URL, login and password credentials you were sent.

1. In your Grafana UI, click on the magnifying glass to search for the dashboard mentioned above. Type in `myth`. Click on the dashboard name to open the dashboard.

   ![magnifying-glass](./images/magnifying-glass.png)
   ![dashboard-search](./images/dashboard-search.png)

1. Examine your dashboard, which is a "RED" dashboard with three key sections: Request rates (R) in the top left, errors (E) in the top right, and duration (D) or latency metrics in the center. Since this is a new service, the error rate percentages might be high. Therefore, our Service Level Objectives (SLOs) will initially focus on the error rates for each endpoint.
![red-dashboard](./images/mythical-beasts-RED-dashboard.png)

1. If you'd like to get a sense of what types of errors the application is experiencing, you can drill into the endpoint's transaction details by clicking on the graph for the endpoint target.

   a. For example, if you were to click on the endpoint `/login` in the upper right graph, a new tab with Grafana's "Explore" feature will appear. You will see that your Distributed tracing instance data source has been pre-populated in the top dropdown, and the "TraceQL" (Tempo's distributed tracing query language) field has been pre-populated with the name of your endpoint (/login) as the `.http.target` value, and the `status` field has been set to `error`.
    ![explore traces](./images/explore-traces2.png)

   b. Click on one of the distributed Trace IDs. This will add a second pane to your existing window with that trace's full transaction path, and shows you not only the sequence and durations of each span within the trace, but also provides span details such as tags, process metadata, and trace logs(if any were recorded).

   c. Since we are filtered on errored transactions, you will notice that one or more of the spans within your trace has a red exclamation mark next to it, signifying an errored span.  Click on that particular span and then click on `Attributes`.  While your particular error status message may be different, I have a `db.statement` field referencing a postgresql query.  I also see an attribute called `status.message` that is associated with our errored status.code. I have a "null value" error, signifying there is a problem with our postgresql query.
![span details](./images/span-details.png)

If you would like more details concerning the features of Grafana's tracing visualization in Explore, go here: https://grafana.com/docs/grafana/latest/explore/trace-integration/
