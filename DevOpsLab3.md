# Lab 3: Create an Azure Web App

[Azure Web Apps](https://docs.microsoft.com/en-gb/azure/app-service/app-service-web-overview) is an Azure service for hosting web applications. In this lab you'll create the Azure Web App into which you will later deploy the web application using Continuous Deployment.

1. In a browser go to the Azure Portal at http://portal.azure.com.

2. Select Create a resource and enter web app into the search field:
<img src="images/WA-1.png" width="624"/>

3. Press enter and select Web App from the list:
<img src="images/WA-2.png" width="800"/>

4. Click Create:
<img src="images/WA-3.png" width="424"/>

5. Complete the highlighted fields as follows:

- App name: Choose a unique name that will be the URL for the web application such as WebApp plus your initials

- Subscription: If you have more than one subscription, ensure that you choose the correct one for this lab

- Resource Group: Create a new resource group for your web app

- OS: Leave this as the default of Windows.

- App Service Plan/Location: Click on this to create a new App Service Plan. Complete these fields:
    - App Service plan: Enter a name, such as WebAppPlan
    - Location: Select an Azure region close to you
    - Pricing tier: Click on this, and select the F1 Free tier

<img src="images/WA-4.png" width="800"/>

6. Click OK to save the App Service Plan.

7. Click Create to save and create the Web App.

8. After a short time (approx. 1-2 mins) you should see a notification that the Web App has been successfully created. You may want to pin the web app to your Azure dashboard for easy location later on:

<img src="images/WA-5.png" width="324"/>

9. Confirm that your Web App is created by selecting Go to resource.

10. Click on the URL:
<img src="images/WA-6.png" width="624"/>

11. Your Web App should open in the browser and you will see something like this:
<img src="images/WA-7.png" width="624"/>
 
This confirms that you have created a Web App in Azure. In the next lab we will deploy the web application into the newly created Azure Web App.

>Optional: Add an Embedded Webpage widget to the Azure DevOps Overview dashboard:
>- Add the Embedded Webpage widget
>- Add the URL for your web app created in the preceding steps:

[<- Lab 2: Continuous Integration](https://github.com/gidavies/WebAppDevOpsLab/blob/master/DevOpsLab2.md) | [Home](https://github.com/gidavies/WebAppDevOpsLab/blob/master/README.md) | [Lab 4: Continuous Deployment ->](https://github.com/gidavies/WebAppDevOpsLab/blob/master/DevOpsLab4.md)