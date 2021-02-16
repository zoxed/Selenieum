# Selecting and Manipulating HTML Elements
### Selecting and HTML Element by ID
```C#
   IWebElement generationTokenElement =
                    driver.FindElement(By.Id("GenerationToken"));
```
Navigate to the browser, use HTML element picker and element you want to find 
Update  public void ReloadHomePageOnBack()
```C#
        [Fact]
        [Trait("Category", "Smoke")]
        public void ReloadHomePageOnBack()
        {
            using (IWebDriver driver = new ChromeDriver())
            {
                driver.Navigate().GoToUrl(HomeUrl);
                //New Code
                 IWebElement generationTokenElement =
                    driver.FindElement(By.Id("GenerationToken"));
                string initialToken = generationTokenElement.Text;
                DemoHelper.Pause();
                driver.Navigate().GoToUrl(AboutUrl);
                DemoHelper.Pause();
                driver.Navigate().Back();
                DemoHelper.Pause();

                Assert.Equal(HomeTitle, driver.Title);
                Assert.Equal(HomeUrl, driver.Url);
                //New Code
                 string reloadedToken = driver.FindElement(By.Id("GenerationToken")).Text;
                Assert.NotEqual(initialToken, reloadedToken);
 
            }
        }
```
### Find Html Elements by name and text HTML attributes
1. Add new Xunit class file CreditCardApplicationShould
   Test to see if a credit card application can be initiated from the home page by 
   clicking on the ApplyLowRateButton
```C#
        [Fact]
        public void BeInitiatedFromHomePage_NewLowRate()
        {
            using (IWebDriver driver = new ChromeDriver())
            {
                driver.Navigate().GoToUrl(HomeUrl);
                DemoHelper.Pause();

                IWebElement applyLink = driver.FindElement(By.Name("ApplyLowRate"));
                applyLink.Click();

                DemoHelper.Pause();

                Assert.Equal("Credit Card Application - Credit Cards", driver.Title);
                Assert.Equal(ApplyUrl, driver.Url);
            }
        }
```
### Find Html Elements by link text
2. Look for a page object by link text
Find link text on the second page of the carousel. 
We have to wait for the carousel changes. 
```C#
 [Fact]
        public void BeInitiatedFromHomePage_EasyApplication()
        {
            using (IWebDriver driver = new ChromeDriver())
            {
                driver.Navigate().GoToUrl(HomeUrl);
                DemoHelper.Pause(11000);

                IWebElement applyLink = driver.FindElement(By.LinkText("Easy: Apply Now!"));
                applyLink.Click();

                DemoHelper.Pause();

                Assert.Equal("Credit Card Application - Credit Cards", driver.Title);
                Assert.Equal(ApplyUrl, driver.Url);
            }
        }
```

#### Find HTML Element Using CSS Selector
Update existing test class to click on a button instead of waiting for an element to appear
```C#
   [Fact]
        public void BeInitiatedFromHomePage_EasyApplication()
        {
            using (IWebDriver driver = new ChromeDriver())
            {
                driver.Navigate().GoToUrl(HomeUrl);
                DemoHelper.Pause();

                IWebElement carouselNext = 
                    driver.FindElement(By.CssSelector("[data-slide='next']"));
                carouselNext.Click();
                DemoHelper.Pause(1000);// allow carousel time to scroll

                IWebElement applyLink = driver.FindElement(By.LinkText("Easy: Apply Now!"));
                applyLink.Click();

                DemoHelper.Pause();

                Assert.Equal("Credit Card Application - Credit Cards", driver.Title);
                Assert.Equal(ApplyUrl, driver.Url);
            }
        }
        ```
### Find HTML Element by class anme

```C#
  [Fact]
        public void BeInitiatedFromHomePage_CustomerService()
        {
            using (IWebDriver driver = new ChromeDriver())
            {
                driver.Navigate().GoToUrl(HomeUrl);
                DemoHelper.Pause();

                IWebElement carouselNext = 
                    driver.FindElement(By.CssSelector("[data-slide='next']"));
                carouselNext.Click();
                DemoHelper.Pause(1000);// allow carousel time to scroll
                carouselNext.Click();
                DemoHelper.Pause(1000);// allow carousel time to scroll

                IWebElement applyLink = 
                    driver.FindElement(By.ClassName("customer-service-apply-now"));
                applyLink.Click();

                DemoHelper.Pause();

                Assert.Equal("Credit Card Application - Credit Cards", driver.Title);
                Assert.Equal(ApplyUrl, driver.Url);
            }
        }
```
### Select an element by the tag name

The home page has a table which can be identified by TD tag

