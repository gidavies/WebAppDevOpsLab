# Lab 5: Infrastructure as Code

The ability to treat infrastructure (machines, networks, configuration) in the same way as code brings many benefits, but in particular allows you to create infrastructure on demand and include that in your DevOps pipeline.

Azure Resource Manager (ARM) templates are the native approach and this lab adds using ARM into the flow. The example here will allow you to create an environment in Azure on demand as part of the flow.

This lab will create a new test environment in Azure without needing to manually create it (via the Portal or the  Command line etc.).

## Task 1 - Create the ARM template for a Web App

1. In Visual Studio, with the Web App solution open in Solution Explorer, right click the solution and select Add | New Project.
<img src="images/IC_1.png" width="624"/>

2. Select Cloud | Azure Resource Group and name the project e.g. WebApp.ARM.
<img src="images/IC_2.png" width="624"/>

3. There are a range of ARM templates to create a wide variety or resources in Azure. In this case from the Visual Studio Templates select Blank Template and click OK.
<img src="images/IC_3.png" width="624"/>

4. You now have a project in your solution containing a blank ARM template (azuredeploy.json) and a blank parameters file (azuredeploy.parameters.json).
<img src="images/IC_4.png" width="324"/>

5. Now replace the content of the files created in the previous step with pre-prepared content:
- View (or download) [this azuredeploy.json file](/ARM/azuredeploy.json), select all the contents of the file, and then copy and paste over the content of the azuredeploy.json file in Visual Studio.
- Do the same with this [azuredeploy.parameters.json file](/ARM/azuredeploy.parameters.json). 
- Save the files in Visual Studio.

6. In Visual Studio, select the Team Explorer | Changes. Add a commit comment and select Commit All and Push. Save if prompted.

The ARM template is now added to source control, although there is no need for it to be in the same repository as the code, this is just for convenience in this lab. Note that adding the new files to source control will trigger a build and release in the background. You could temporarily turn off the CI trigger but just let it run in the background while completing the next task.

## Task 2 - Update the release pipeline to provision the Web App using the ARM template.

1. In VSTS select Build and Release | Releases | your release definition and Edit.
<img src="images/IC_5.png" width="624"/>

2. Add a new artifact to the release pipeline. This means the release will get the application from the build (as a zip file) and the ARM templates directly from source control (as they don't need to be compiled or packaged).
<img src="images/IC_6.png" width="624"/>

3. Set the Source type to Git, the Project and Source (repository) to the Web App project, the Default branch to master and the default version to Latest from default branch. Then click Add (you may need to scroll down).
<img src="images/IC_7.png" width="624"/>

4. In the Pipeline view hover over the Dev environment and select Clone.
<img src="images/IC_8.png" width="624"/>

5. Select the cloned environment Copy of Dev and change the name to QA and close the Environment window.
<img src="images/IC_9.png" width="624"/>.

6. Select the QA environment (by clicking on the "1 phase, 1 task" link inside the QA environment) and in Tasks click the plus sign and then search for the Azure Resource Group Deployment task. Select Add.
<img src="images/IC_10.png" width="624"/>

7. Set the Azure Details. Select the Azure subscription set up previously, Ensure that the Action is Create or update resource group, Enter a new resource group name for the QA environment e.g. WebAppQA-RG and set the location.
<img src="images/IC_11.png" width="624"/>

8. In the Template section set the Template (using the ... button) to Web App (Git) WebApp.ARM/azuredeploy.json and click OK.
<img src="images/IC_12.png" width="624"/>

9. Set the Template parameters field (using the ... button) to WebApp (Git) WebApp.ARM/azuredeploy.parameters.json and click OK.
<img src="images/IC_13.png" width="624"/>

10. Set the Override Template parameters field (using the ... button) to WebAppQAPlan, the webSiteName to the same as the Dev website but with QA appended (e.g. WebApp-GJAD-QA)and click OK.
<img src="images/IC_14.png" width="624"/>

11. Move the Azure Deployment: Create or Update Resource Group task to be before the Deploy Azure App Service task by dragging and dropping the task.

12. In the QA deployment process settings set the App service name to the name you used in step 10 above. Save your changes. 
<img src="images/IC_15.png" width="624"/>

13. Test the changes by making another code change (e.g. changing the heading again), committing and pushing, and observe the build and release.
After a few minutes you should see that both the Dev and QA environments have been successfully deployed to.
<img src="images/IC_16.png" width="624"/>

17. Explore the [Azure portal](http://portal.azure.com) to find the resource group WebApp-QA-RG and the web app provisioned using ARM in the QA environment. Confirm that the App service has been deployed and open it using the URL in the App service overview.
<img src="images/IC_17.png" width="624"/>

You have now created a DevOps pipeline that deploys to multiple environments, and provisions the QA environment on demand without a manual process.

[Lab 4: Continuous Deployment](https://github.com/gidavies/WebAppDevOpsLab/blob/master/DevOpsLab4.md) | [Lab 6: Automated Testing with Selenium](https://github.com/gidavies/WebAppDevOpsLab/blob/master/DevOpsLab6.md)