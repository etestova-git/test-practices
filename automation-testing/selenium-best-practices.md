## 📐 Best Practices for Selenium Testing

### 1. **Use the Page Object Model (POM)**
- Separate page structure from test logic.
- Each web page is represented by a class.
- Web elements and methods for interaction go into the page class.

### 2. **Avoid Hard-Coding Waits**
- ❌ `Thread.sleep(5000)`
- ✅ Use **Explicit Waits** (`WebDriverWait`) to wait for specific conditions.

### 3. **Use Meaningful Locators**
- Prefer stable locators: `id`, `name`, or custom `data-*` attributes.
- Avoid brittle locators like `XPath` unless necessary.

### 4. **Keep Tests Independent**
- Each test should be self-contained.
- Use setup and teardown methods to manage preconditions and cleanup.

### 5. **Use Assertions Wisely**
- Validate key elements and outcomes.
- Keep one assertion per test case if possible for clarity.

### 6. **Log and Capture Screenshots**
- Use logs for better traceability.
- Capture screenshots on failure for debugging.

### 7. **Parameterize Your Tests**
- Use data-driven testing with external sources (CSV, Excel, JSON).
- Apply test frameworks like TestNG, NUnit, or JUnit.

### 8. **Run in Headless Mode for CI**
- Run tests in headless mode in CI/CD pipelines to save resources.

### 9. **Integrate with CI/CD Tools**
- Use GitHub Actions, Jenkins, GitLab CI, or Azure Pipelines.

### 10. **Maintain a Robust Test Suite**
- Continuously refactor.
- Remove flaky or obsolete tests.
- Prioritize tests for faster feedback.

---

## 🧱 Page Object Model (POM) Structure

### 📁 Project Example:
```
selenium-project/
├── pages/
│   ├── LoginPage.cs
│   └── DashboardPage.cs
├── tests/
│   └── LoginTests.cs
├── utils/
│   └── DriverFactory.cs
└── pom.config / package.json
```

### 🧩 Sample Page Class (C#)
```csharp
public class LoginPage {
    private IWebDriver driver;

    public LoginPage(IWebDriver driver) {
        this.driver = driver;
    }

    private IWebElement Username => driver.FindElement(By.Id("username"));
    private IWebElement Password => driver.FindElement(By.Id("password"));
    private IWebElement LoginButton => driver.FindElement(By.Id("login"));

    public void Login(string user, string pass) {
        Username.SendKeys(user);
        Password.SendKeys(pass);
        LoginButton.Click();
    }
}
```

### 🧪 Sample Test Class
```csharp
[TestClass]
public class LoginTests {
    private IWebDriver driver;

    [TestInitialize]
    public void SetUp() {
        driver = new ChromeDriver();
    }

    [TestMethod]
    public void TestValidLogin() {
        var loginPage = new LoginPage(driver);
        driver.Navigate().GoToUrl("https://example.com/login");
        loginPage.Login("user", "pass");
        Assert.IsTrue(driver.Url.Contains("dashboard"));
    }

    [TestCleanup]
    public void TearDown() {
        driver.Quit();
    }
}
```

---

## 📚 Resources
- [Selenium Documentation](https://www.selenium.dev/documentation/)
- [C# Selenium with NUnit](https://github.com/SeleniumHQ/selenium/wiki)
- [Page Object Pattern](https://www.selenium.dev/documentation/test_practices/encouraged/page_object_models/)

---
