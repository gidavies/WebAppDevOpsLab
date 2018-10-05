# Lab 7: Monitoring with Application Insights

DevOps doesn't stop at deployment into production. Monitoring and understanding your application provides valuble insight. 

1. In Visual Studio right-click on the WebApp project | Application Insights | Configure Application Insights
<img src="images/AI_1.png" width="624"/>

2. Update the SDK, if needed, and click Start Free.
<img src="images/AI_2.png" width="624"/>

3. Set the correct account, subscription and resource - for resource that will probably be a New resource. Also decide whether you want Application Insights to be capped at the free tier or allow it to exceed the free tier limits. If in doubt select to halt collection at the free limits.
<img src="images/AI_3.png" width="624"/>

4. Commit and push the changes. This will trigger another build and release.
<img src="images/AI_4.png" width="624"/>

5. When the release to QA has completed go to the [Azure portal](http://portal.azure.com) select the Application Insights service for the Web App (it may take a little while for data to show). Click on the Live Stream button.
<img src="images/AI_5.png" width="624"/>

6. Give it a few seconds for some baseline data to show.
<img src="images/AI_6.png" width="624"/>

7. Go to your deployed app and click on the Home, About and Contact pages, then return to the Live Stream to see the data showing.
<img src="images/AI_7.png" width="624"/>

8. Close the Live Stream and click on the Page View Load Time graph.
<img src="images/AI_8.png" width="624"/>

9. Take a look at data on page response time
<img src="images/AI_9.png" width="624"/>.

10. Close the Page response time blade and select Analytics.
<img src="images/AI_10.png" width="624"/>

11. Try some of the queries such as the Users query
<img src="images/AI_11.png" width="624"/>
<img src="images/AI_12.png" width="624"/>

This is just a tiny sample of what can be done with Application Insights, you can [read more here](https://docs.microsoft.com/en-us/azure/application-insights/)

>Optional: Add an Application Insights widget showing test results to the Lab Progress dashboard by:
>- Find and install the Application Insights widget in the [marketplace](http://marketplace.visualstudio.com/)
><img src="images/AI_13.png" width="624"/>

>- Searching for and adding the Application Insights Chart (and/or Metrics) widget:
><img src="images/AI_14.png" width="624"/>

>- Configure the widget following [these instructions](https://marketplace.visualstudio.com/items?itemName=ms-appinsights.ApplicationInsightsWidgets)
><img src="images/AI_15.png" width="624"/>

>- Save the changes, close the widget gallery and save the dashboard by clicking on the blue edit button in the bottom right hand corner.

This completes the DevOps labs.

[<- Lab 6: Automated Testing with Selenium](https://github.com/gidavies/WebAppDevOpsLab/blob/master/DevOpsLab6.md) | [Home](https://github.com/gidavies/WebAppDevOpsLab/blob/master/README.md)