# SLO Workshop | Breakout 2 | NB | V2


# Prerequisites



* Grafana Cloud account
* Ensure you see the SLO (preview) under ‘Alerts & IRM’ \
 \


<p id="gdcalert1" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image1.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert2">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image1.png "image_tooltip")



# Breakout

Organizations who have yet to put SLO’s into effect can benefit from Grafana’s guidance and specialized tooling. Once implemented the benefits of SLOs are extensive, from alleviating alert fatigue to providing executives/managers/engineers data-driven insights on innovation vs. reliability prioritization. \
 \
Follow the below steps to generate SLOs for your mission critical applications or services, using a simplified point & click UI - \




1. Click on the SLO (preview) and then click on ‘Initialize Grafana SLO’, if not done so already. See the snapshot below - \
 \


<p id="gdcalert2" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image2.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert3">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image2.png "image_tooltip")
 \

2. Next, click on the ‘Create SLO’ button. See the snapshot below - \


<p id="gdcalert3" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image3.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert4">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image3.png "image_tooltip")
 \
 \

3. See the below steps to create an SLO -
    1. **Define SLI **- This step has the most amount of required user input. You would start by choosing the right SLI’s, which are a proxy for end user experience. An SLI query should return a number between 0 and 1. For example - Successful events (HTTP requests without any errors) divided by total events (all HTTP requests) as a way to measure the health of that service. \
 \
Default time window is set to 28 days, because it always captures the same number of weekends, no matter what day of the week it is. This accounts better for traffic variation over weekends than a 30 days SLO. It is still configurable. \
 \
Next, choose a metric-based query type. There are 2 options currently - **‘Ratio’** and **‘Advanced’**. We will define ‘Ratio’ based query in this workshop. Configure traces_spanmetrics_calls_total{status_code!="STATUS_CODE_ERROR", service="mythical-server"} as your success metric. This metric accounts for all HTTP calls **without errors**. Choose traces_spanmetrics_calls_total{service="mythical-server"} for total metric. This metric accounts for all HTTP calls for the mythical app, regardless of errors. We will use http_target as the ‘Group by labels’ to distinguish between different types of HTTP endpoints (/account, /cart, /fastcache, /health, /payment, /login etc.). \
 \
Click on the “Run Queries” button right underneath to see the auto generated SLI query and its visual representation. \
 \
See the snapshot below - \
 \


<p id="gdcalert4" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image4.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert5">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image4.png "image_tooltip")
 \
 \

    2. Next, click on ‘Set target and error budget’. Set the desired SLO target as 95%, resulting in an error budget of 5%. See the snapshot below - \
 \


<p id="gdcalert5" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image5.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert6">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image5.png "image_tooltip")
 \
 \

    3. Next, click on ‘Add name and description’. Give a meaningful name and an associated description. See the below snapshot - \
 \


<p id="gdcalert6" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image6.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert7">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image6.png "image_tooltip")
 \

    4. Next, click on ‘Add SLO alert rules’. Check the ‘Add SLO alert rules’ checkbox. See the snapshot below - \
 \


<p id="gdcalert7" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image7.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert8">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image7.png "image_tooltip")
 \
 \
This auto generates 2 types of alerts based upon the configured SLO -
        1. **Fast-burn** - When we are depleting through our error budget extremely fast as compared to our targets set in step 3b. This would typically mean relevant teams would get notified in an expedient manner and they’d need to focus on increasing the reliability of the service.
        2. **Slow-burn** - When we are depleting through our budget slowly. It still requires attention but we don’t need to deprioritize everything else and work on a fix. \
 \

    5. Last step in this bullet, click on ‘Review SLO’. Ensure everything is accurately configured. Click on ‘Save and view all SLOs’. See the snapshot below - \
 \


<p id="gdcalert8" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image8.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert9">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image8.png "image_tooltip")
 \
 \
 \

4. Let the newly configured SLO sit there for at least a couple of minutes. After about 2-4 minutes, you would start seeing data in the auto generated Grafana dashboard for that SLO ((in most panels if not all)). See the snapshot below for instance - \
 \


<p id="gdcalert9" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image9.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert10">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image9.png "image_tooltip")
 \
 \
Based upon the http_target selection in the top left, you would see different SLI, error budget and corresponding burn rate values for each endpoint or the aggregate (all). \
In the snapshot below, /account endpoint is not adhering to the target SLO of 95% at the moment and thereby depleting through the error budget faster than we’d like. This information is appropriately color coded in these dashboards to help interpret the current state quickly. \
 \


<p id="gdcalert10" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image10.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert11">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image10.png "image_tooltip")
 \
 \
 \
