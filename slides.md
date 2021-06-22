---
layout: cover
download: "https://github.com/dimitriharding/next-level-automation-workshop"
highlighter: shiki
info: |
  ## Next-level Test Automation Workshop

  Pattens and tips for creating a structured UI automation project (JavaScript edition)

  [Dimitri Harding](https://dimitriharding.com/)

  - [Source code](https://github.com/dimitriharding/next-level-automation-workshop)
---

# Next-Level Test Automation Workshop

Pattens and tips for creating a structured UI automation project (JavaScript edition)

<div class="uppercase text-sm tracking-widest">
Dimitri Harding
</div>

<div class="abs-bl mx-14 my-12 flex">
  <img src="https://seetyah.s3.amazonaws.com/QualityWorks-Logo-Symbol-1.jpg" class="h-8 rounded-full">
  <div class="ml-3 flex flex-col text-left">
    <div><b>QualityWorks</b> Automation Workshop</div>
    <div class="text-sm opacity-50">Apr. 25th, 2021</div>
  </div>
</div>

<a href="https://github.com/dimitriharding/next-level-automation-workshop" target="_blank" alt="GitHub"
  class="abs-br m-6 text-xl icon-btn opacity-50 !border-none !hover:text-white">
<carbon-logo-github />
</a>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
layout: 'intro'
---
# Dimitri Harding

<div class="leading-8 opacity-80">

- 👨🏽‍💻 I'm a Tester by Profession, but a marker by Passion
- 🏢 Lead QA Consultant at **QualityWorks** in 🇯🇲.
- ✨ What I do daily: **Cook**, **Eat**, **Work**, **Code**, **Listen Music**, **Hack on Something**, **Sleep**
- 🎭 Hobbies: **Photography**, **Creating something (physically or virtually)**
</div>

<div class="my-10 grid grid-cols-[40px,1fr] w-min gap-y-4">
  <ri-github-line class="opacity-50"/>
  <div><a href="https://github.com/dimitriharding" target="_blank">dimitriharding</a></div>
  <ri-twitter-line class="opacity-50"/>
  <div><a href="https://twitter.com/irtimid_harding" target="_blank">irtimid_harding</a></div>
  <ri-user-3-line class="opacity-50"/>
  <div><a href="https://antfu.me" target="_blank">dimitriharding.com</a></div>
</div>

<img src="https://dimitriharding.com/static/images/dimitri@2x.jpg" class="rounded-full w-40 abs-tr mt-16 mr-12"/>


---
name: Workshop Outline
layout: intro
---

# What will we be learning?

We'll be talking about structuring your test automation project, and we'll look at some automation practices that can make your life easier.

- 📤 **What are test frameworks made of?**
- 🛠 **Creating a structured test automation framework/project**
- 🧑‍💻 **Commands - Tricks & Tips**
- 🤹 **Incorporating different types of testing**

<br>
<br>

---
layout: center
class: text-center
name: What are test frameworks made of?
---

# <CustomHeader> What are test frameworks made of? </CustomHeader>

Hooks | Test Runner | Assertions | Reporter




<!-- > In general, a framework is a set of best practices, assumptions, common tools, and libraries that you can use across teams.


> Test frameworks provide some of the benefits of increase reusability of code, higher portability, reduce test script maintenance cost and so on. -->

---
name: Test Frameworks
---
# Test Frameworks

- Java: TestNG, JUnit
- JavaScript: Mocha, Jasmine, AVA

<br/>
<br/>

<div v-click>

> Fun fact - by default WebdriverIO uses Mocha as their test framework

</div>


---
name: Hooks - Before
---

# Hooks <Marker class="text-green-500">Test Framework</Marker>

Hooks are blocks of code that you can execute **before** or **after** your tests, suites, etc.

<div class="grid grid-cols-[100px,1fr,400px] gap-x-4" >

<div />

### Use Case

### Example

<v-clicks :every='3' >

<div class="my-auto leading-6 text-base opacity-75">
Before
</div>

<div>

- Starting a webdriver server (this is mostly done automatically)
- Setting up a database connection for getting test data
- Loading test data (local/remote)
- Navigating to a certain page
- or anything else that your test might need to be executed properly

</div>

```js


 before(function () {
    // runs once before the first test in this block
  });

  beforeEach(function () {
    // runs before each test in this block
  });
```

</v-clicks>

</div>

---
name: Hooks - After
---

# Hooks <Marker class="text-green-500">Test Framework</Marker>

Hooks are blocks of code that you can execute **before** or **after** your tests, suites, etc.

<div class="grid grid-cols-[100px,1fr,400px] gap-x-4" >

<div />

### Use Case

### Example

<div class="my-auto leading-6 text-base opacity-75">
After
</div>

<div>

- Shutting down webdriver server (again, mostly done automatically)
- Closing database connection
- Clearing test data
- Clearing browser cookies
- Taking a screenshot if there was an error
- Generating a report
- or post-action you would want to person after your tests are executed

</div>

```js


  after(function () {
    // runs once after the last test in this block
  });


  afterEach(function () {
    // runs after each test in this block
  });
```

</div>

---
name: Mocha Hooks
---

# Mocha Hooks <Marker> [->](https://mochajs.org/#hooks) </Marker>

Hooks can be used to set up preconditions and clean up after your tests.

```ts {all|2-4|6-8|10-12|14-16|all}
describe("hooks", function () {
  before(function () {
    // runs once before the first test in this block
  });

  after(function () {
    // runs once after the last test in this block
  });

  beforeEach(function () {
    // runs before each test in this block
  });

  afterEach(function () {
    // runs after each test in this block
  });

  // test cases
  it('Should pass all the time', () => {
    // some test code
  })
  //...
});
```

---
name: WebdriverIO Hooks
---

# WebdriverIO Hooks <Marker> [->](https://webdriver.io/docs/configurationfile/) </Marker>

Additional hooks outside of before and after, but they serve the same purpose

```js
    onPrepare: function (config, capabilities) {
    },
    /**
     * Gets executed before a worker process is spawned and can be used to initialize specific service
     * for that worker as well as modify runtime environments in an async fashion.
     */
    onWorkerStart: function (cid, caps, specs, args, execArgv) {
    },
    /**
     * Gets executed just before initializing the webdriver session and test framework. It allows you
     * to manipulate configurations depending on the capability or spec.
     */
    beforeSession: function (config, capabilities, specs) {
    },
    /**
     * Gets executed before test execution begins. At this point you can access to all global
     * variables like `browser`. It is the perfect place to define custom commands.
     */
    before: function (capabilities, specs, browser) {
    },
    /**
     * Gets executed before the suite starts.
     * @param {Object} suite suite details
     */
    beforeSuite: function (suite) {
    },
    /**
     * This hook gets executed _before_ every hook within the suite starts.
     * (For example, this runs before calling `before`, `beforeEach`, `after`, `afterEach` in Mocha.)
     */
    beforeHook: function (test, context/*, stepData, world*/) {
    },
    /**
     * Hook that gets executed _after_ every hook within the suite ends.
     * (For example, this runs after calling `before`, `beforeEach`, `after`, `afterEach` in Mocha.)
     */
    afterHook: function (test, context, { error, result, duration, passed, retries }/*, stepData, world*/) {
    },
    /**
     * Function to be executed before a test (in Mocha/Jasmine) starts.
     */
    beforeTest: function (test, context) {
    },
```

---
name: TestNG Hooks 
---

#  TestNG Hooks <Marker> [->](https://www.toolsqa.com/testng/testng-annotations/) </Marker>

```java
....
public class TestNG {
		@Test
		public void testCase1() {

			System.out.println("This is the A Normal Test Case");

		}

		@BeforeMethod

		public void beforeMethod() {

			System.out.println("This will execute before every Method");

		}

		@AfterMethod

		public void afterMethod() {

			System.out.println("This will execute after every Method");

		}

		@BeforeClass

		public void beforeClass() {

			System.out.println("This will execute before the Class");

		}

		@AfterClass

		public void afterClass() {

			System.out.println("This will execute after the Class");

		}

		@BeforeTest

		public void beforeTest() {

			System.out.println("This will execute before the Test");

		}

		@AfterTest

		public void afterTest() {

			System.out.println("This will execute after the Test");

		}

		@BeforeSuite

		public void beforeSuite() {

			System.out.println("This will execute before the Test Suite");

		}

		@AfterSuite

		public void afterSuite() {

			System.out.println("This will execute after the Test Suite");

		}

	}
```

---
name: Tests/Test Runner
layout: center
class: text-center
---

# <CustomHeader> Tests & the Test Runner </CustomHeader>

Look at the test runner and how tests relate to it

<!--
You can organize your tests by using different files or test suites.
-->

---
name: Tests
---

# Tests <MarkerTestFramework/>

Tests are blocks of code that contains the steps and assertion/s for your test scenarios. You can organize your tests by using different files or test suites.

<v-click>

```js {5-13|6-10|10-12|all}
const loginData = require("../../data/loginData");
const loginPage = require("../../pages/login.page");

describe("User Authentication", function () {
  it("Verify that a user can sign in", function () {
    loginPage.navigate();
    loginPage.enterUserEmail(loginData.validEmail);
    loginPage.enterPassword(loginData.validPassword);
    loginPage.clickLoginButton();

    browser.waitForUrlIncludes("myaccount");
    browser.verifyTextInPage("My Account");
  });
});
```

</v-click>

---
name: Tests (without assertion)
---
# Tests (without assertion/s) <MarkerTestFramework/>

A test without an assertion will always pass once there are no errors in any of the steps (your test should always have an assertion)

<v-click>

```js
const loginData = require("../../data/loginData");
const loginPage = require("../../pages/login.page");

describe("User Authentication", function () {
  it("Verify that a user can sign in", function () {
    loginPage.navigate();
    loginPage.enterUserEmail(loginData.validEmail);
    loginPage.enterPassword(loginData.validPassword);
    loginPage.clickLoginButton();
  });
});
```

</v-click>

---
name: Test Runner
---
# Test Runner <MarkerTestFramework/>

Tests are handled by a test runner

<v-click>

<div class="content-center">
<img border="rounder" class="center" src="https://seetyah.s3.amazonaws.com/test%20runner.jpg" />
</div>

</v-click>

---
name: Assertions
---

# Assertions <MarkerTestFramework/>

An assertion is a check to determine if something is true (correct). [Chai](https://www.chaijs.com/) is an assertion library for node that provides handy methods that can be used for different assertions needs.

<br/>
Below are 3 examples of the different types of assertions you can use. Most of us assert or expect
<br/>
<br/>
<img v-click border="rounded" src="https://seetyah.s3.amazonaws.com/Screen_Shot_2021-05-31_at_3.20.48_PM.png">

---
name: Assertion Examples
---

# Assertions <MarkerTestFramework/>

<div class="grid grid-cols-2 gap-x-4"><div>

## WebdriverIO.Expect

```js
browser.url("https://webdriver.io/");
expect(browser).toHaveUrlContaining("webdriver");
```

<div v-click>

### Pros

- Less code
- Comes built-in
- Sometimes more intuitive

### Cons

- Not easily understood without context

</div>

</div><div>

## Chai.Expect

```js
const chai = require("chai");

browser.url("https://webdriver.io/");
const currentUrl = browser.getUrl();
chai.expect(currentUrl).to.contain("webdriver");
```

<div v-click>

### Pros

- Can be used with any framework
- Easy to read/understand

### Cons

- More code
- Have to be installed to use

</div>
</div></div>

---
name: Reporting
---

# Reporting <MarkerTestFramework/>

Reporting is how the test results are shown to the user after the testing is completed. 

Test frameworks normally comes with a default reporter, could be an XML report or the results are printed to the terminal. 

<v-click>

In most cases you can either create your own or use other report plugins to see the results. 

Examples: 

- Allure report
- Mohawesome
- Spec Reporter
- HTML reporter

</v-click>

<!--
Creating your own report (custom report) can be easily since the framework would encourage it.
-->

---
name: Reporting (Spec)
---

# Reporter (Spec) <MarkerTestFramework/>


<div class="content-center">
<img border="rounder" class="center" src="https://seetyah.s3.amazonaws.com/Screen%20Shot%202021-06-16%20at%201.55.06%20PM.png" />
</div>

---
name: Reporter (XML)
---
# Reporting (XML) <MarkerTestFramework/>

<br/>

```xml
<?xml version='1.0'?>
<ns2:test-suite xmlns:ns2='' start='1623797599401' stop='1623797609879'>
    <name>User Authentication</name>
    <title>User Authentication</title>
    <test-cases>
        <test-case start='1623797599401' status='passed' stop='1623797609878'>
            <name>Verify that a user can sign in</name>
            <title>Verify that a user can sign in</title>
            <labels>
                <label name='language' value='javascript'/>
                <label name='framework' value='wdio'/>
                <label name='thread' value='0-0'/>
            </labels>
            <parameters>
                <parameter kind='argument' name='browser' value='chrome-91.0.4472.101'/>
                <parameter kind='environment-variable' name='BROWSER' value='chrome'/>
                <parameter kind='environment-variable' name='BROWSER_VERSION' value='undefined'/>
                <parameter kind='environment-variable' name='PLATFORM' value='undefined'/>
            </parameters>
            <steps/>
            <attachments/>
        </test-case>
    </test-cases>
</ns2:test-suite>
```

---
name: Reporting (Allure HTML)
---
# Reporter (Allure) <MarkerTestFramework/>


<div class="content-center">
<img border="rounder" class="center" src="https://seetyah.s3.amazonaws.com/Screen%20Shot%202021-06-16%20at%202.30.30%20PM.png" />
</div>

---
name: Structured Automation Project
layout: center
class: text-center
---
# <CustomHeader> Creating Structure in your Test Automation Framework/Project </CustomHeader>

Some best ways and best practices for structuring your automation project

<!-- You can organize your tests by using different files or test suites. -->

---
name: Project Structure
---
# Project Structure

```md
automation-project
|- data             # data to be used during testing
|- pages            # page objects
|- report           # empty folder for reports (reports should not be in source control)
|- support          # perfect for reusable code (commands, utils)
|- tests            # where all test live
|- .env             # environmental variables (local)
|- .gitignore       # list of files to be ignored (node_modules, .env)
|- environments.js  # list of environments for automation (production, stage, etc.)
|- package.json     # various metadata relevant to the project
```

<br/>

> You will be working in your project that you cloned as we go along in this section

---
name: Environmental Variables
---

# Environmental Variables <MarkerProjectStructure />

A variable whose value is set outside the program, typically through functionality built into the operating system or microservice.


Why are environmental variables important?

<div>

<v-clicks>

- **Security**: Things like API keys should not be in plain text in your code and thereby directly visible

- **Flexibility**: If you were interacting with an API and each team member has their own key, you would have to make code edits

- **Adoption**: Your CI/CD pipeline supports environmental variables

</v-clicks>

</div>

<!--
An environment variable is made up of a name/value pair, and any number may be created and available for reference at a point in time
-->

---
name: Environmental Variables Definition
---
# Environmental Variables Definition <MarkerProjectStructure />

<div class="grid grid-cols-2 gap-x-4"><div>

## Command Line

<br/>

```bash
API_KEY=zaCELgLim USERNAME=dharding npm run test
```

<div v-click>

### Pros

- Convenient
- No security risk

### Cons

- You have to actively remember all variables
- easy to makes typo
- long commands

</div>

</div><div>

## A `.env` file

<br/>

```bash
API_KEY=zaCELgLim
USERNAME=dharding
```

<div v-click>

### Pros

- Easy to manage
- One place to see all variables

### Cons

- Security risk (if you forget to add this file to a gitignore file)

</div>
</div></div>

---
name: Environmental Variables Exercise
---

# Environmental Variables Exercise <MarkerProjectStructure />

1. Go to the root of your project
2. Create a `.evn` file
3. Add `NAME` as a variable, and add your name as the `value` 
4. Run this command and observe what happened (____)

---
name: NPM Scripts
---
# NPM Scripts <MarkerProjectStructure />

These are a convenient way to store and reference common shell commands that you use in your project

<v-click>

Command

```bash
./node_modules/.bin/@wdio 
```

</v-click>

<v-click>

NPM script

```bash
npm test
```

```js
# package.json
....
"script": {
   "test": "@wdio",
   "test:smoke": "",
  }
  ....
  Specify window size, browser
}
....
// npm scripts understand that you want to access wdio binary 
// in your project so you don't have to use the full path, just the name of the module
```

</v-click>

---
name: NPM Script Exercise
---
# NPM Script Exercise <MarkerProjectStructure />

1. Go to `package.json`
2. Add your own script using the save command that you created before
3. Run your npm script and see what happens

---
name: Page Objects
---
# Page Object Model <MarkerProjectStructure />

Page Object is a Design Pattern for enhancing test maintenance and reducing code duplication.

<div v-clicks>

- A page object is an object-oriented class that serves as an interface to a page/part of a page (section) for your automaton.

- There is a clean separation between test code and page specific code such as locators

- There is a single repository for the services or operations offered by the page rather than having these services scattered throughout the tests.

- Page objects should never make verifications or assertions. Verification should should be in your tests.

- There are other design patterns that can be used like "Screen Play" (look it up)

</div>

---
name: Page Object Example
---
# Page Object Example <MarkerProjectStructure />

```js
const page = require("./page");

// LoginPage class extends the base page object
class LoginPage extends page {

  // Locators are defined as getters
  get txtUsername()  { return $("#email"); }
  get txtPassword()  { return $("#password"); }
  get btnLogin()     { return $(".segment button.button"); }

  // ...
  navigate() {
    super.navigate("/login");
    return this;
  }

  enterUsername(username) {
    this.txtUsername.waitForDisplayed();
    this.txtUsername.clearValue();
    this.txtUsername.setValue(username);
  }

  enterPassword(password) {
    this.txtPassword.waitForDisplayed();
    this.txtPassword.clearValue();
    this.txtPassword.setValue(password);
  }

  clickLoginButton() {
    this.btnLogin.waitForDisplayed();
    this.btnLogin.click();
  }

  // ....
}

module.exports = new LoginPage();
```
---
name: Test with Page Object
---

# Test with/out Page Object <MarkerProjectStructure />

<div class="grid grid-cols-2 gap-x-4"><div>

## Without

<br/>

<div v-click>

```js
// ...
it("Verify that a user can sign in", function () {
  browser.url('/login')

  const txtUsername = $('#email')
  txtUsername.waitForDisplayed();
  txtUsername.clearValue();
  txtUsername.setValue(loginData.validEmail);

  const txtPassword = $('#password')
  txtPassword.waitForDisplayed();
  txtPassword.clearValue();
  txtPassword.setValue(loginData.validPassword);

  browser.waitForUrlIncludes("myaccount");
  browser.verifyTextInPage("My Account");
});
// ...
```

</div>

</div><div>

## With

<br/>

<div v-click>

```js
// ...
it("Verify that a user can sign in", function () {
  loginPage.navigate();
  loginPage.enterUsername(loginData.validEmail);
  loginPage.enterPassword(loginData.validPassword);
  loginPage.clickLoginButton();

  browser.waitForUrlIncludes("myaccount");
  browser.verifyTextInPage("My Account");
});
// ...
```


</div>
</div></div>

---
name: Page Object Exercise
---

# Page Object Exercise <MarkerProjectStructure />

Improve the current Login page object `login.page.js` 

Objective: 
  - Create one function/method for logging in
  - Update test to use this new method/function
  - Run your test and ensure that they still work