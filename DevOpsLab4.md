# Lab 4: Continuous Deployment

Continuous Deployment is another key practice within DevOps to enable the continuous delivery of value (in this example the web application) to end users.

## Task 1: Create the release pipeline

1. In the Builds hub select the latest build, then click on the 3 dots and select Create release.
<img src="images/Lab4_T1_S1.png" width="624"/>

2. Select a template for the release pipeline. If you scroll through the list you'll see that there are many templates. As we are going to deploy a web application into an Azure App Service, select the Azure App Service Deployment template and click Apply.
<img src="images/CD_2.png" width="624"/>

3. A release pipeline may have many stages such as Dev, QA, UAT, pre-prod, prod. For now we will have one, and the first stage to deploy to is typically a shared development environment, so call it Dev or similar. Then click the close button.
<img src="images/Lab4_T1_S3.png" width="624"/>

4. Notice that there is already an Artifact to deploy. This has been configured automatically as the release was created from the build. Click on the Artifact to see the details.
<img src="images/CD_4.png" width="624"/>

5. This shows that the Artifact is the latest version of the output of the CI build that was created earlier. That output includes the zip file, which is the web application to be deployed. Close the window.
<img src="images/CD_5.png" width="624"/>

6. Click on the Artifact Continuous deployment trigger.
<img src="images/CD_6.png" width="624"/>

7. This is where you can enable or disable Continuous Deployment - i.e. whenever a new build is created, this release pipeline is triggered. Notice that it should already be set to Enabled (set it if not). Close the window.
<img src="images/CD_7.png" width="624"/>

8. Now click on the jobs and tasks in the Dev environment. This is where we will configure how to do the deployment into Azure.
<img src="images/Lab4_T1_S8.png" width="624"/>

9. The first areas to address in the environment are Azure settings.
<img src="images/CD_9.png" width="624"/>

10. In the Azure subscriptions list, choose the relevant subscription and click Authorize. This is to create an authorised connection to Azure using that subscription.
<img src="images/CD_10.png" width="624"/>

11. Having authorised the subscription you should be able to see and select the Web App that you created in the preceding step. This is the target Web App that we will deploy to.
<img src="images/CD_11.png" width="624"/>

12. Click the Run on agent step and confirm that the agent is set to the same as the build - the Hosted VS2017 agent.
<img src="images/CD_12.png" width="624"/>

13. Click Deploy Azure App Service task. You shouldn't need to change anything here but note that this uses the Azure subscription to deploy to the App Service, and the package to be deployed is a zip file, as created in the CI build. Click Save and accept the default location for the pipeline.
<img src="images/CD_13.png" width="624"/>

You have now created a Release Pipeline, configured to Continuously Deploy whenever there is a new build. The next step is to test the overall flow.

## Task 2: Test the release pipeline

1. Test the release pipeline by returning to Visual Studio and making a change. For example open the WebApp/Views/Home/Index.cshtml again and make another change such as changing the heading for the home page. Save the changes.
<img src="images/L2_13.png" width="624"/>

2. In the Team Explorer, return to the Changes hub (click the Home icon if needed to return to the hubs) to see the files you've changed, and add a comment and select Commit All and Push.
<img src="images/L2_14.png" width="324"/>

3. In Azure DevOps, navigate to the Builds (Pipelines | Builds) and you should now see a build in progress. Click on the build number to watch the build. 
<img src="images/Lab4_T2_S3.png" width="624"/>

4. Open the build log and when it's completed select the summary and scroll down to see the Deployments area. You should see that a release to the Dev stage is in progress and therefore Continuous Deployment has been successfully triggered.
<img src="images/Lab4_T2_S4.png" width="624"/>

5. Click on the Release link (it should be Release-1) in Deployments to see the release pipeline. Hover over the Dev stage and select Logs if you want to look at the detailed logs. Note that the zip file (artifact) is downloaded from the build (not rebuilt) and then deployed to Azure.
<img src="images/Lab4_T2_S5.png" width="624"/>

6. Go to the web app URL (as per Lab 3 Step 10 above) and refresh the page to see your newly deployed web application.
<img src="images/CD_16.png" width="624"/>

You have now deployed a web application into a live Azure site using a DevOps release pipeline triggered by committing a code change. If you want, make one or more other changes in the code, commit and push and see those changes built and deployed into your web application.

>Optional: Add a Release Definition Overview widget to the Overview dashboard by:
>- Add a Release Definition Overview widget.
>- In the configuration widget set the release definition to the release created in the lab above.
>- Save the changesto the dashboard.

[<- Lab 3: Create an Azure Web App](https://github.com/gidavies/WebAppDevOpsLab/blob/master/DevOpsLab3.md) | [Home](https://github.com/gidavies/WebAppDevOpsLab/blob/master/README.md) | [Lab 5: Infrastructure as Code ->](https://github.com/gidavies/WebAppDevOpsLab/blob/master/DevOpsLab5.md)