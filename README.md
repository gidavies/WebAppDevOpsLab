# Web App DevOps Lab

This lab will step through the key elements in setting up a DevOps pipeline for Azure using the DevOps tools for Azure - Visual Studio Team Services (VSTS).

>Background information

>[What is DevOps?](https://www.visualstudio.com/learn/what-is-devops/)

>[How Microsoft does DevOps](https://www.visualstudio.com/learn/devops-at-microsoft/)

# Overall flow

- Preparing for the lab
- Creating the project
- Working with Git
- Continuous Integration
- Create an Azure web app
- Continuous Deployment
- Infrastructure as Code
- Automated Testing with Selenium
- Monitoring with Application Insights

# Preparing for the lab

For this lab you will require:

- A Visual Studio Team Services account (free)
- An Azure subscription (your own or a free trial)
- Visual Studio 2017 installed (optional)

>VSTS supports any app and doesn't require the use of Visual Studio, .NET or other Microsoft languages. At the bottom of this page there are links to labs that work through implementing DevOps with Node, Java, Eclipse, IntelliJ and Docker.

If you don't have one, create a [VSTS account](http://www.visualstudio.com).

# Creating the project

## Task 1: Create the VSTS Team Project

1. Open a browser and navigate to your VSTS account https://*youraccountname*.visualstudio.com.
2. In your VSTS account select New Project.
<img src="images/L1_1.png" width="624"/>
3. Give the project a name, e.g. Web App. Make sure that version control is set to Git and click Create. 
<img src="images/L1_2.png" width="624"/>
4. Your VSTS team project has been created. You can add other people to the team if you want.
<img src="images/L1_3.png" width="624"/>

You now have a VSTS team project. The next step is to create a web application.

## Task 2: Creating the Visual Studio Web Application

1. To clone the (empty) Git repository into Visual Studio, click on the Clone in Visual Studio button.
<img src="images/L1_4.png" width="624"/>
2. You may be prompted to confirm that you want to open Visual Studio (exact look and feel will depend on the browser you're using). If so, agree to open Visual Studio.
<img src="images/L1_5.png" width="624"/>
3. Visual Studio will then prompt to clone the VSTS remote Git repo to your local machine. Change the local path as required and then click Clone.
<img src="images/L1_6.png" width="624"/>
4. If you now open the Team Explorer you will see that the repository has been cloned succesfully.
<img src="images/L1_7.png" width="324"/>
5. Select New in the Solutions area of Team Explorer.
<img src="images/L1_8.png" width="324"/>
6. Select Web | ASP.NET Web Application, change the name as required and click OK.
<img src="images/L1_9.png" width="524"/>
7. Ensure that MVC is selected, disable Enable Docker if checked and check Add unit tests. Click OK.
<img src="images/L1_10.png" width="624"/>
8. When the project has been created, click the run button (green arrow) or F5 to build and launch the web application locally.
<img src="images/L1_11.png" width="624"/>
9. The web application will launch locally. Take a quick look and then close the browser. To stop the debug session.
<img src="images/L1_12.png" width="624"/>
10. To stop the debug session click the stop button or Shift + F5 in Visual Studio.
<img src="images/L1_13.png" width="624"/>

You now have a web application. The next step is now to add this to Git so that it is under source control.

## Task 3: Committing the new Web App to source control

1. In the Visual Studio Team Explorer, select Changes.
<img src="images/L1_14.png" width="324"/>
2. Add a commit commment, such as Initial commit, then select Commit All and Push.
<img src="images/L1_15.png" width="324"/>
3. When completed you can go back to VSTS in the browser, select Code and you will see your web application. Take a look at the history to see your initial commit.
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
