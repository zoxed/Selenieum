# Lesson One
## Why Automate? 
Gain increased confidence in a thing we are delivering to an end user. 
Automated tests give us breadth, faster to execute, and can be ran any time we want. 

## What kind of errors we may find?
Errors in Views, Models, DTOs
Errors in client side/server side validation mismatch

## Difference between Selenium IDE and Selenium Web Driver
If we split them, Selenium IDE records scripts
Selenium webdriver code-first apprached

## Test Framework components
Test Code
Test Framework
WebDriver Library
Browser Specific Driver
Browser
Web Server

## Which Scenarios to Automate
"Follow the money"
Focus on risk and legal implications

1. Run application in debug mode
2. Add a new class library and delete the default class file
3. Right click on the Dependencies in the Solution explorer and select manage nuget packages
4. Add following packages:
   1. xunit
   2. xunit.runner.visualstudio
   3. selenium.webdriver
   4. selenium.webdriver.chromedriver (when running locally ensure your browser version matches your chromedriver version)
5. Add a new class to the project CreditCardApplicationShould.cs
6. Import Xunit library
7. Add first script:
 ```c#
        [Fact]
		[Trait("Category", "Smoke")]
		public void LoadApplicationPage()
		{
			using (IWebDriver driver = new ChromeDriver())
			{
				driver.Navigate().GoToUrl(HomeUrl);

				DemoHelper.Pause();

				Assert.Equal(HomeTitle, driver.Title);
				Assert.Equal(HomeUrl, driver.Url);
			}
		}
```
8. Add following constants on the class level
```C#
        private const string HomeUrl = "http://localhost:44108/";
		private const string AboutUrl = "http://localhost:44108/Home/About";
		private const string HomeTitle = "Home Page - Credit Cards";
```
9. Add the DemoHelper class to the project
    ```C#
    internal static class DemoHelper
    {
        ///// <summary>
        ///// Brief delay to slow down browser interactions for
        ///// demo video recording purposes
        ///// </summary>
        public static void Pause(int secondsToPause = 3000)
        {
            Thread.Sleep(secondsToPause);
        }
    }
    ```
   