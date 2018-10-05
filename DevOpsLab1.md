# Lab 1: Creating the project

## Task 1: Create the Azure DevOps Team Project

1. Open a browser and navigate to your Azure DevOps organisation - either https://*youraccountname*.visualstudio.com or https://dev.azure.com/*youraccountname* (the new URL and default for new organisations).
2. In your Azure DevOps organisation select New Project.
<img src="images/L1_1.png" width="624"/>
3. Give the project a name, e.g. Web App. Make sure that version control is set to Git and click Create. You could equally choose to use TFVC but this lab has documented the steps for using Git.
<img src="images/L1_2.png" width="624"/>
4. Your VSTS team project has been created. You can add other people to the team if you want.
<img src="images/L1_3.png" width="624"/>

You now have a VSTS team project. The next step is to create a web application.

## Task 2: Creating the Visual Studio Web Application

1. To clone the (empty) Git repository into Visual Studio there are two main options - cloning from within the browser or from within Visual Studio. 
    ### Cloning from within the browser. 

    1. Click on the Clone in Visual Studio button.
    <img src="images/L1_4.png" width="624"/>

    2. You may be prompted to confirm that you want to open Visual Studio (exact look and feel will depend on the browser you're using). If so, agree to open Visual Studio.
    <img src="images/L1_5.png" width="624"/>

    3. Visual Studio will then prompt to clone the VSTS remote Git repo to your local machine. Change the local path as required and then click Clone.
    <img src="images/L1_6.png" width="624"/>

    If this doesn't work then follow the Cloning from within Visual Studio steps.

    ### Cloning from within Visual Studio

    1. Open the Team Explorer view (bottom left hand side next to the Solution Explorer). Then select Manage Connections and Connect to Project.
    <img src="images/L1_A2.png" width="424"/>

    2. Select the Web App project (you may only have one project listed) expand it to show the Web App repository and then click Clone.
    <img src="images/L1_A3.png" width="424"/>

    ### Signing in to Visual Studio

    If you haven't used Visual Studio on the machine before you will be prompted to sign in when Visual Studio starts. Sign in with the account that you are using for VSTS.
    <img src="images/L1_A1.png" width="324"/>
    
2. If you now open the Team Explorer (bottom right hand corner) you will see that the repository has been cloned succesfully.
<img src="images/L1_7.png" width="324"/>
3. Select New in the Solutions area of Team Explorer.
<img src="images/L1_8.png" width="324"/>
4. Select Web | ASP.NET Web Application, change the name as required and click OK.
<img src="images/L1_9.png" width="524"/>
5. Ensure that MVC is selected, disable Enable Docker if checked and check Add unit tests. Click OK.
<img src="images/L1_10.png" width="624"/>
6. When the project has been created, click the run button (green arrow) or F5 to build and launch the web application locally.
<img src="images/L1_11.png" width="624"/>
7. The web application will launch locally. Take a quick look and then close the browser.
<img src="images/L1_12.png" width="624"/>
8. To stop the debug session click the stop button or Shift + F5 in Visual Studio.
<img src="images/L1_13.png" width="624"/>

You now have a web application. The next step is to add the application to Git so that it is under source control.

## Task 3: Committing the new Web App to source control

1. In the Visual Studio Team Explorer, select Changes.
<img src="images/L1_14.png" width="324"/>
2. You may be prompted to enter or confirm your Git User Information. Just click Save and you won't be prompted again.
<img src="images/L1_14a.png" width="424"/>
3. Add a commit comment, such as Initial commit, then select Commit All and Push.
<img src="images/L1_15.png" width="324"/>
4. When completed you can go back to VSTS in the browser, select Code and you will see your web application. Take a look at the history to see your initial commit.
<img src="images/L1_16.png" width="624"/>

You now have a web application, committed to source control in VSTS. The next step is to add Continuous Integration to the VSTS project.

>Optional: Create a new Dashboard in VSTS:
>- In your VSTS project, select Dashboard and then New:
><img src="images/L1_17.png" width="624"/>

>- Name the new Dashboard Lab Progress:
><img src="images/L1_18.png" width="624"/>

>- Select the pencil icon in the bottom left, followed by the plus button:
><img src="images/L1_19.png" width="624"/>

>- Search for and select the Markdown widget:
><img src="images/L1_20.png" width="624"/>

>- Configure the Markdown widget and add the names of your team, project vision and/or any other info that might be useful:
><img src="images/L1_21.png" width="624"/>

>- Save the changes, close the widget gallery and save the dashboard by clicking on the blue edit button in the bottom right hand corner.

[<- Intro](https://github.com/gidavies/WebAppDevOpsLab/blob/master/README.md) |[Lab 2: Continuous Integration ->](https://github.com/gidavies/WebAppDevOpsLab/blob/master/DevOpsLab2.md)