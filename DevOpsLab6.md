# Lab 6: Automated Testing with Selenium

Integrating automated tests into your DevOps pipeline can help drive quality whilst deploying more frequently. This lab integrates [Selenium](http://www.seleniumhq.org/), a popular automated functional testing framework, into your pipeline. Selenium allows you to automate the testing of your web application using all the main browsers, reducing the manual testing required. 

Selenium drivers are already installed on the Hosted agents being used in this pipeline. You can use the drivers to run tests in IE, Chrome or Firefox. For this example Chrome will be used, but you could follow the same steps and switch the driver to another browser, or repeat tests using multiple browsers. 

## Task 1: Create the Selenium tests

1. In Visual Studio, Solution Explorer, select the solution and Add | New Project. Then select the Test category and Unit Test Project. Give the project a name, such as WebApp.UITest, and click OK.
<img src="images/S_1.png" width="624"/>

2. The Selenium libraries need to be added to the project. Right-click on the test project and select Manage NuGet Packages. 
<img src="images/S_2.png" width="624"/>

3. Select Browse, search for Selenium and install the latest (default) versions of Selenium.WebDriver and Selenium.Chrome.WebDriver
<img src="images/Lab6_T1_S3.png" width="624"/>

4. Close the NuGet page.

5. Replace the entire contents of UnitTest1.cs with the following:

```c#
using System;
using Microsoft.VisualStudio.TestTools.UnitTesting;
using OpenQA.Selenium.Remote;
using OpenQA.Selenium.Chrome;

namespace WebApp.UITest
{
    [TestClass]
    public class UITests
    {
        private static RemoteWebDriver _webDriver = null;
        private static string _webAppBaseURL;

        [ClassInitialize()]
        public static void ClassInit(TestContext context)
        {
            // The hosted agent env variable for IE is IEWebDriver, Firefox is GeckoWebDriver
            // If you switch the driver you'll need the corresponding nuget package.
            _webDriver = new ChromeDriver(Environment.GetEnvironmentVariable("ChromeWebDriver"));

            // Allow for web app compilation and startup post deployment 
            _webDriver.Manage().Timeouts().ImplicitWait = TimeSpan.FromSeconds(15);

            _webAppBaseURL = "https://<your qa web site>.azurewebsites.net/";
        }

        [ClassCleanup()]
        public static void Cleanup()
        {
            if (_webDriver != null)
            {
                _webDriver.Quit();
            }
        }

        [TestMethod]
        [TestCategory("Selenium")]
        public void HomePageFoundTest()
        {
            _webDriver.Url = _webAppBaseURL;

            string actualPageTitle = _webDriver.Title;
            string expectedPageTitle = "Home Page - My ASP.NET Application";

            Assert.AreEqual(expectedPageTitle, actualPageTitle);
        }

        [TestMethod]
        [TestCategory("Selenium")]
        public void AboutPageFoundTest()
        {
            _webDriver.Url = _webAppBaseURL + "/Home/About";

            string actualPageTitle = _webDriver.Title;
            string expectedPageTitle = "About - My ASP.NET Application";

            Assert.AreEqual(expectedPageTitle, actualPageTitle);
        }

        [TestMethod]
        [TestCategory("Selenium")]
        public void ContactPageFoundTest()
        {
            _webDriver.Url = _webAppBaseURL + "/Home/Contact";

            string actualPageTitle = _webDriver.Title;
            string expectedPageTitle = "Contact - My ASP.NET Application";

            Assert.AreEqual(expectedPageTitle, actualPageTitle);
        }

        [TestMethod]
        [TestCategory("Selenium")]
        public void SupportEmailAddressChromeTest()
        {
            string supportEmailAddress = "Support@example.com";

            _webDriver.Url = _webAppBaseURL + "/Home/Contact";
            RemoteWebElement supportEmailElement = (RemoteWebElement)_webDriver.FindElementByLinkText(supportEmailAddress);

            Assert.AreEqual(supportEmailAddress, supportEmailElement.Text);
        }

        [TestMethod]
        [TestCategory("Selenium")]
        public void MarketingEmailAddressTest()
        {
            string marketingEmailAddress = "Marketing@example.com";

            _webDriver.Url = _webAppBaseURL + "/Home/Contact";
            RemoteWebElement marketingEmailElement = (RemoteWebElement)_webDriver.FindElementByLinkText(marketingEmailAddress);

            Assert.AreEqual(marketingEmailAddress, marketingEmailElement.Text);
        }

        [TestMethod]
        [TestCategory("Selenium")]
        public void IndexTitleTest()
        {
            string expectedTitle = "Your heading";

            _webDriver.Url = _webAppBaseURL + "/Home/Index";
            RemoteWebElement titleElement = (RemoteWebElement)_webDriver.FindElementByTagName("H1");

            Assert.AreEqual(expectedTitle, titleElement.Text);
        }
    }
}
```
6. This code contains six tests that will be executed against the web application using the Selenium PhantomJS driver. The tests check that pages and content on those pages exist. Note:
    - You need to add your QA web app url into line 24 (the one you can find as per the last step in Lab 5 above):
    ```c
    _webAppBaseURL = "https://<yourwebapp>.azurewebsites.net/";
    ```
    - The final test (IndexTitleTest) checks the heading on the home page that you have been changing in the previous labs. Make sure that the expected value is correct for your web app (line 100).
    ```c
    string expectedTitle = "Your heading";
    ```
    - The [TestCategory] property which will be used later to filter which tests to run

7. Save all files.

You now have some Selenium tests in the project. Before committing these to source control the next step is to amend the Azure DevOps pipeline to incorporate the tests into the flow.

## Task 2: Add the tests into the pipeline

1. First the build definition needs to ensure that the tests are available in the build output, so that they can be run in the release. Open the build definition (Pipelines | Builds | Edit).

2. In Agent Job 1, click + select the Utility tab and select the Copy Files task. This task will ensure that the tests are avaiable in the build output to be used in the release.
<img src="images/Lab6_T2_S2.png" width="624"/>

3. Set the following values in the Copy Files task:
    - Source Folder: $(build.sourcesdirectory)
    - Contents: \*\*\bin\\$(BuildConfiguration)\\*\*
    - Target Folder: $(build.artifactstagingdirectory)
    - The Display name will update as you make changes.
<img src="images/S_5.png" width="624"/>

4. Move (drag and drop) the Copy Files task to be immediately after the Build solution task. The compiled tests will now be available in the build output the next time the build runs, and therefore availble to the release pipeline. 

5. In this example we want the CI build to continue to only run unit tests and not the new Selenium tests, which require a deployed application. Therefore update the Test Assemblies task and add TestCategory!=Selenium in the Test filter criteria field. This uses the TestCategories in the test code to filter the tests to be run, in this case excluding the Selenium tests.
<img src="images/Lab6_T2_S5.png" width="624"/>

6. Save (but not queue) the build.

7. The next step is to execute the tests as part of the release. Open the Release definition (Pipelines | Releases | Edit) and click on the tasks for the QA environment. Click the + button, select the Test tab and select the Visual Studio Test task. The Selenium tests are within a unit test so this task can execute them.
<img src="images/S_6.png" width="624"/>

8. Select the test task. In the Test filter criteria field add TestCategory=Selenium. This will only execute tests that have the matching [TestCategory] property in the code and provides control over which tests to run. In this example we have decided not to run the Selenium tests in the CI build but want to run them against the deployed application in the QA environment.
<img src="images/Lab6_T2_S8.png" width="624"/>

9. Ensure that the test task is the last task and save the release.

10. Now return to Visual Studio and the Team Explorer. You may need to click the back arrow or home button in Team Explorer. Then commit and push the changes. This will trigger the CI build, which will now include the tests in the output, and then trigger the CD release, which will execute the tests found in the build output. Wait for the build and release into QA to complete and then open the release pipeline summary. You should see that there are tests in the QA environment and that they have passed.
<img src="images/Lab6_T2_S10.png" width="624"/>

11. Click on the 100% pass link for the QA environment and you will see the individual test results. By default the view is filtered to only show failed tests, select Outcomes and clear the filters to see the individual test results.
<img src="images/Lab6_T2_S11.png" width="624"/>

You now have automated UI tests being executed everytime a new version of your application is deployed.

>Optional: You might want to see what happens when a test fails. You could change the heading for the web app again, but not update the tests (or the other way around), and commit the change. You should then see a successful CI build (as the UI Tests aren't run in the build), a successful release to Dev (as the Selenium tests aren't run in that stage) but a failed release to QA, as that's the stage the Selenium tests are run in.

>Optional: Add a Deployment status widget showing test results to the Lab Progress dashboard by:
>- Searching for and adding the Deployment status widget.
>- Configure the widget for the build and release pipelines including all environments.

[<- Lab 5: Infrastructure as Code](https://github.com/gidavies/WebAppDevOpsLab/blob/master/DevOpsLab5.md) | [Home](https://github.com/gidavies/WebAppDevOpsLab/blob/master/README.md) | [Lab 7: Monitoring with Application Insights ->](https://github.com/gidavies/WebAppDevOpsLab/blob/master/DevOpsLab7.md)