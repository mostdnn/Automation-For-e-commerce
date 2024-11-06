Selenium Test Automation Framework
Overview
This is a Selenium Test Automation Framework designed to automate web application testing using the Page Object Model (POM) design pattern, TestNG for test management, Allure Report for test reporting, and Data-Driven Testing for parameterized test cases. The framework is compatible with IntelliJ IDEA as the primary Integrated Development Environment (IDE).

Key Features:
TestNG for test execution and reporting
Page Object Model (POM) design pattern for better maintainability
Data-Driven Testing using Excel or CSV files
Allure Reports for visual and interactive test reports
Built with Selenium WebDriver for cross-browser testing
JUnit for assertions and running tests (optional)
Configuration files for different environments (optional)
Prerequisites
Before you begin, make sure you have the following installed:

Java JDK 8+
Maven (for dependency management)
IntelliJ IDEA (or your preferred IDE)
Allure Commandline (for generating Allure reports)
Selenium WebDriver libraries
TestNG and Allure TestNG Adapter dependencies
Steps to Set Up the Project
Clone the Repository:

bash
نسخ الكود
git clone <repository_url>
cd <project_directory>
Import the Project into IntelliJ IDEA:

Open IntelliJ IDEA.
Go to File > Open and select the project directory.
IntelliJ will automatically import the project if Maven is used.
Install Dependencies: The project uses Maven to manage dependencies. Simply build the project using:

bash
نسخ الكود
mvn clean install
This will download the necessary libraries like Selenium, TestNG, and Allure.

Configuration Files:

You can set up configuration files for different environments in the src/main/resources folder (e.g., config.properties).
The configuration can include environment-specific details like the base URL, browser options, and more.
Project Structure
bash
نسخ الكود
├── pom.xml                # Maven project file with dependencies
├── src
│   ├── main
│   │   └── java
│   │       └── com
│   │           └── yourcompany
│   │               └── testautomation
│   │                   ├── pages             # Page Object Model classes
│   │                   ├── tests             # Test classes (TestNG)
│   │                   ├── utils             # Utility classes
│   │                   └── config            # Configurations (BaseClass, etc.)
│   └── resources
│       ├── testdata        # Data files (e.g., Excel, CSV)
│       └── config.properties # Configuration file for environment setup
├── target                  # Allure and test output will be stored here
└── README.md               # Project documentation (this file)
Framework Components
1. Page Object Model (POM)
The framework follows the Page Object Model design pattern, which helps separate the test logic from the page-specific actions.
Each web page has its own corresponding page object class where elements and actions are defined.
For example, the LoginPage.java will have locators for username, password fields, and the login button along with methods to interact with them.
2. TestNG
TestNG is used for test management and execution. The tests are defined as TestNG test methods in the tests package.
Each test method is annotated with @Test, and TestNG's annotations like @BeforeMethod, @AfterMethod, etc., are used for setup and teardown.
Example:

java
نسخ الكود
@Test
public void loginTest() {
    LoginPage loginPage = new LoginPage(driver);
    loginPage.enterUsername("testuser");
    loginPage.enterPassword("password123");
    loginPage.clickLoginButton();
    Assert.assertTrue(loginPage.isLoginSuccessful());
}
3. Data-Driven Testing
The framework supports Data-Driven Testing using Excel or CSV files.
TestNG provides the @DataProvider annotation, which reads test data from external files and runs the test multiple times with different inputs.
Example:

java
نسخ الكود
@DataProvider(name = "loginData")
public Object[][] loginData() {
    return new Object[][] {
        { "user1", "password1" },
        { "user2", "password2" }
    };
}

@Test(dataProvider = "loginData")
public void loginTest(String username, String password) {
    LoginPage loginPage = new LoginPage(driver);
    loginPage.enterUsername(username);
    loginPage.enterPassword(password);
    loginPage.clickLoginButton();
    Assert.assertTrue(loginPage.isLoginSuccessful());
}
4. Allure Reports
Allure is used to generate attractive and interactive reports after tests are executed.
You can configure TestNG to generate Allure reports by using the Allure TestNG Adapter.
Steps to generate Allure report:

After running the tests, generate the Allure report with:
bash
نسخ الكود
allure serve target/allure-results
Allure will open the report in the default browser.
5. IntelliJ IDEA
IntelliJ IDEA is the recommended IDE for developing and running tests.
You can run TestNG tests directly from IntelliJ and view the results in the IDE.
Running Tests
To run the tests, follow these steps:

Run from IntelliJ:

Right-click on the Test class or TestNG.xml file and select Run.
Run from Command Line:

bash
نسخ الكود
mvn test
This will run the tests using Maven and generate reports in the target directory.

Reporting
Allure Reports: After running tests, Allure generates a report that can be opened in the browser to view detailed results, including test status, logs, and screenshots.
To generate the Allure report, use:

bash
نسخ الكود
allure serve target/allure-results
Dependencies in pom.xml
Here are some of the dependencies included in the pom.xml:

xml
نسخ الكود
<dependencies>
    <!-- Selenium WebDriver -->
    <dependency>
        <groupId>org.seleniumhq.selenium</groupId>
        <artifactId>selenium-java</artifactId>
        <version>3.141.59</version>
    </dependency>

    <!-- TestNG -->
    <dependency>
        <groupId>org.testng</groupId>
        <artifactId>testng</artifactId>
        <version>7.4.0</version>
        <scope>test</scope>
    </dependency>

    <!-- Allure TestNG Adapter -->
    <dependency>
        <groupId>io.qameta.allure</groupId>
        <artifactId>allure-testng</artifactId>
        <version>2.16.1</version>
        <scope>test</scope>
    </dependency>

    <!-- Apache POI (for Data-Driven Testing) -->
    <dependency>
        <groupId>org.apache.poi</groupId>
        <artifactId>poi</artifactId>
        <version>5.2.3</version>
    </dependency>
</dependencies>
Conclusion
This Selenium Test Automation Framework offers a robust, maintainable approach to automating web application testing using the Page Object Model (POM), TestNG, Allure for reporting, and Data-Driven Testing for flexible test cases. With IntelliJ IDEA as the IDE and Maven for dependency management, it is easy to set up and extend for various testing needs.
