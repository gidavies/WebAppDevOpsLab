# Lab 2: Continuous Integration

Continuous Integration is a key DevOps practice to build, test and create the software to later deploy.

## Task 1: Set up the Continuous Integration definition

1. Navigate to the VSTS project Code hub, and select Set up build.
<img src="images/L2_1.png" width="624"/>
2. There are a range of build templates available, including non-Microsoft technologies but for this example select the ASP.NET template and click Apply.
<img src="images/L2_2.png" width="624"/>
3. The template creates a build definition with a number of tasks added. Select the Process task which states that some settings need attention. You need to select the build agent where you want to run this build. You can choose to run the builds using an on-premise agent or use the agents hosted on Azure. We will use the Hosted VS2017 agent as it has the .NET framework and all other components that are required to build the app. Check that the agent is set to Hosted 2017.
<img src="images/L2_3.png" width="624"/>
4. The Get sources task will be showing red to indicate that something needs completing. Click on the Get sources task, and set the source to VSTS Git. This is telling the build that it will get the source code to build from Git hosted in VSTS, although there are many other options. Keep the default settings for VSTS Git. 
<img src="images/L2_31.png" width="624"/> 
5. The template restores any dependencies using NuGet, builds the solution, runs any unit tests and then publishes the output. This should be ready to use, so for now test the build by clicking Save & Queue.
<img src="images/L2_4.png" width="624"/>
6. The next window allows you to change some inputs into the build, but just click Save & Queue.
<img src="images/L2_5.png" width="424"/>
7. You should now see that a build has been queued. Click on the build number to watch the build in progress.
<img src="images/L2_6.png" width="624"/>
8. Observe the build progressing. It will typically take a few minutes.
<img src="images/L2_7.png" width="624"/>
9. When the build completes click on the build number to see the build log. The summary tab shows who made what changes and when, as well as unit test results.
<img src="images/L2_8.png" width="624"/>
10. Click on the artifacts tab and the Explore button to look at the output of the build.
<img src="images/L2_9.png" width="624"/>
11. Expand the drop folder and notice that there is a zip file created from the build task in the build definition. This is the web application, packaged as a zip file, which is an easy way to deploy to Azure. Click Close.
<img src="images/L2_10.png" width="424"/>

You now have a working build definition for the web application. The next step is to set it up with a Continuous Integration trigger and test it.

## Task 2: Enable Continuous Integration

1. Hover your mouse over the build definition and you will see three dots. Click on the dots and select Edit.
<img src="images/L2_11.png" width="624"/>
2. Select Triggers and check Enable continuous integration. Save (but not queue).
<img src="images/L2_12.png" width="624"/>
3. Test the Continuous Integration trigger by returning to Visual Studio and making a change. For example open the WebApp/Views/Home/Index.cshtml and make a change such as changing the heading for the home page. Save the changes.
<img src="images/L2_13.png" width="624"/>
4. In the Team Explorer, return to the Changes hub to see the files you've changed, and add a comment and select Commit All and Push.
<img src="images/L2_14.png" width="324"/>
5. In VSTS, navigate to the Builds (Build & Release | Builds) and you should now see a build in progress. If you want to click on the build number to watch the build. 
<img src="images/L2_15.png" width="624"/>

You now have a build triggered whenever you make a change to the code and push that change to Git in VSTS - Continuous Integration is in place for the project.

>Optional: Add a Build History widget to the Lab Progress dashboard by:
>- Searching for and adding the build history widget:
><img src="images/L2_22.png" width="624"/>

>- Ensuring that it is configured to the build definition created in the preceding steps:
><img src="images/L2_23.png" width="624"/>

>- Save the changes, close the widget gallery and save the dashboard by clicking on the blue edit button in the bottom right hand corner.

[<- Lab 1: Creating the project](https://github.com/gidavies/WebAppDevOpsLab/blob/master/DevOpsLab1.md) | [Home](https://github.com/gidavies/WebAppDevOpsLab/blob/master/README.md) | [Lab 3: Create an Azure Web App ->](https://github.com/gidavies/WebAppDevOpsLab/blob/master/DevOpsLab3.md)