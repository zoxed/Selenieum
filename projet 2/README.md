# dotnet_selenium_lessontwo
Arrange, Act, and Assert
```C#
 [Fact]
        [Trait("Category", "Smoke")]
        public void LoadApplicationPage()
        {
            using (IWebDriver driver = new ChromeDriver())
            {
                //arrange
                driver.Navigate().GoToUrl(HomeUrl); 
                //act
                DemoHelper.Pause();
                //assert
                Assert.Equal(HomeTitle, driver.Title);
                
                Assert.Equal(HomeUrl, driver.Url);
            }
        }
```
In the code above Paus is inserted for demo purposes
Reading Browser's URL
```C#
 Assert.Equal(HomeUrl, driver.Url);
```
1. Web Driver Refresh Command
```C#
[Fact]
        [Trait("Category", "Smoke")]
        public void ReloadHomePage()
        {
            using (IWebDriver driver = new ChromeDriver())
            {
                driver.Navigate().GoToUrl(HomeUrl);

                DemoHelper.Pause();

                driver.Navigate().Refresh();

                Assert.Equal(HomeTitle, driver.Title);
                Assert.Equal(HomeUrl, driver.Url);
            }
        }
```



