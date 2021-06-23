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
- 🧑‍💻 **Tips & Tricks**
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
An environment variable is made up of a name/value pair, and any number may be created and available for reference at a point in time. 


This is be editing this.
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
- Install a module to load it (dotenv)

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

<div>

Command

```bash
./node_modules/.bin/@wdio 
```

</div>

<div>

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

</div>

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

<div>

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

<div>

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

<div>

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

---
name: Groups/tags (regression, smoke, etc) 
---
# Groups/tags (REGRESSION, smoke, etc) <MarkerProjectStructure />

Using features like groups or tags to create things like a regression or smoke suite that you can easily reference through a command. 

Each test framework implements this in their own way, but we'll use WebdriverIO as the example in this case. 

```bash
npm run test:regression
npm run test:smoke
```

<br/>

```js
// wdio.conf.js
exports.config = {
    // define all tests
    specs: ['./test/**/*.test.js'],
    // ...
    // define specific suites
    suites: {
        login: [
            './test/authentication/login.test.js',
        ],
        regression: [
            // ...
        ]
    },
    // ...
}
```

---
name: Smoke
---
# Groups/tags (regression, SMOKE, etc) <MarkerProjectStructure />

In the case of smoke tests, you might want to run multiple specific tests, not just a list of files

```bash
grep -r -l --include "*.js" "@smoke" | wdio wdio.conf.js
```
* Find all test that have the text `@smoke` in their title.

<br/>
<br/>

```js
it('Verify that I cam login @smoke'){ ... } 
it('Verify that the login button is blue') { ... }
it('Verify that I can make a payment @smoke'){ ... } 
```
---
name: Groups/tags Exercise
---
# Groups/tags Exercise <MarkerProjectStructure />

Create a regression suite and create a `test:regression` command for it

1. Edit the `wdio.conf.js` file to include your suite
2. Create a regression suite and only include the login test file
3. Edit the `package.json` file to include your script (test:regression)
4. Run your regression suite using the script in step 3

<br/>

```bash
wdio wdio.conf.js --suite regression
```
* how to reference your suite

---
name: Custom Assertion and Command
---
# Custom Assertions and Commands <MarkerProjectStructure />

There are times when you need to extend your test automation framework to do operations that are very common

These operations are normally around commands and assertions beyond what is built-in

<div v-click>

```js {all|1-5|6-10}
  waitThenClick: function (element) {
    element.waitForExist();
    element.waitForDisplayed();
    element.click();
  },
  verifyTextInPage: function (text) {
    const pageText = $("body").getText();
    const position = pageText.search(text);
    chai.expect(position).to.be.above(0);
  },
```

</div>

<!-- The difference between a custom assertion and a command is that the commands are just steps but the assertion have some comparison that's encapsulated 

  clearThenSetValue: function (element, value) {
    element.waitForDisplayed();
    element.clearValue();
    element.setValue(value);
  },

-->

---
name: Custom Assertion and Command Exercise
---
# Custom Assertions and Commands Exercise <MarkerProjectStructure />

Create a custom command to replace redundant code in your `loginUser` method in your page object

1. Edit the `commands.js` file in the support folder
2. Create a custom command called `clearThenSetValue` that accepts an element and value
3. Replace the redundant code in your page object with this new method
4. Usage `browser.clearThenSetValue(pageElement, 'value')` 

---
name: Custom Reporter 
---
# Reporters (custom, other types) <MarkerProjectStructure />

We can create our own custom reports, by either using the built-in support or parsing data

1. Create reports by either parsing/transforming a default report into anything that we might need. 

2. We also have the option to use another plugin if needs be. 

<div v-click>

- Email
- Test Case Management (QualityWatcher, Testrail)
- Communication Channels (Slack, Microsoft Teams)
- Just about anything that have a webhook integration

</div>

---
name: Customer Reporter (Slack) 
---
# Example: Slack Reporter for WebdriverIO <MarkerProjectStructure />

<div v-click>

<div class="content-center">
<img border="rounder" class="center" src="https://seetyah.s3.amazonaws.com/Screen%20Shot%202021-06-22%20at%208.57.40%20AM.png" />
</div>

</div>

<!-- 
Talk about explanation
 -->

---
name: Custom Reporter Skills
---

# Custom Report Skills

When making custom reporters you pull on different skills

Skills include: 
- Understanding and working with APIs
- Understanding and working with Markdown (formatting of results)
- Using webhooks
- JavaScript
---
name: Custom Reporter Exercise 
---
# Customer Reporter Exercise <MarkerProjectStructure />

Create your own custom reporter using the WebdriverIO built-in support

1. Edit the `customReporter.js` file in the `./support/utils/` folder
2. Uncomment the different handlers and and write an appropriate message to the console
4. Edit the `wdio.conf.js` file to include the reporter (import is already done for you)
3. Run your login test and see what happens

---
name: Test Data
---

# Test Data - Data retrievers <MarkerProjectStructure />

While testing we might need to use external data for setting up the test or for confirming some data. 

It could be  JSON, API, Database, CSV, Excel, etc ... but we normally have to code this.

<!-- 
  Look at the login tests, walk them through the excel read and import, talk about the API one
 -->

---
name: Test Data - Using API Exercise
---

# Test Data - Using API Exercise <MarkerProjectStructure />

1. Use the response from `https://tax-by-state.vercel.app/api/get-tax?cost=2000&state=California` to get the tax from an API
2. Use the response to verify that the application calculate the tax correctly (`https://tax-by-state.vercel.app/`)
3. Edit the `./tests/dataDriven/externalData.test.js` file to add the missing pieces to make the code work

<br/>
<br/>

> The `getTaxCalculation` is already interacting with the API, you just need to pass the correct values and get a response

---
name: Documentation (README.md)
---
# Documentation (README.md) <MarkerProjectStructure />

A README is a text file that introduces and explains a project. It contains information that is commonly required to understand what the project is about. 

<div v-click>

Some things to keep in mind when creating a README.md for your test automation

- should be short but detailed
- how to install and run your automation
- how to execute groups/tags/suites (if any)
- how to use different environments
- Your readme file is written using markdown (markdown is a plain text formatting syntax)

</div>

---
name: Linting
---
# Linting & Code Formatting <MarkerProjectStructure />

Linting helps to prevent some common issues when coding, while code formatting ensure that everyone on the team is using the same style 

Get Example: 

---
layout: center
class: text-center
name: Tips and Tricks
---

# <CustomHeader> Tips and Tricks for Automation gotchas! </CustomHeader>
Not all projects require you to use these techniques but knowing them is worth it

---
name: IFrames
---

# Tips & Tricks -  IFrame <MarkerTipsAndTricks />

An IFrame (Inline Frame) is an HTML document embedded inside another HTML document on a website

<div v-click>

How do we automate something in an IFrame? 
- Find out if you need to interact with an iframe (tag - `<iframe />`)
- Switch to the IFrame (supported by your automation framework)
- Remember to switch back to parent when you are done (if needed)

[IFrame examples](https://the-internet.herokuapp.com/iframe)

</div>

---
name: IFrame Exercise
---
# IFrame Exercise <MarkerTipsAndTricks />

Switch to the "MIDDLE" iframe and verify the text

Use the existing tests as examples in `tests/tipsAndTricks/iFrames.test.js`

---
name: Windows/Tabs
---

# Working with Windows <MarkerTipsAndTricks />

This is referring to a new tab in the same window, which can be confusing

How do we automation something in a new tab? 
- Similar like iframes, we need to do a switch to the tab we want to interact with
- Depending on the test framework, there are different methods for switching
- WebdriverIO gives you the option for using the URL or Title

---
name: Working with Windows <MarkerTipsAndTricks />
---

# Working with Windows Exercise

Switch to windows/tabs using the title on the page

Use the existing tests as examples in `tests/tipsAndTricks/windows.test.js`

---
name: Executing a script
---
# Executing a script <MarkerTipsAndTricks />

Any JavaScript that you can execute in the browser, you can from your automation

While this is a very rare case there are times when you need to manipulate a web page from your automation
- You would use JavaScript to do this
- An example would be to make a element visible for interaction

<div v-click>

```js
   // Executing JavaScript with WebdriverIO element
    browser.execute((refOfElement) => {

      // we are able to manipulate this element using the display property
      refOfElement.style.display = "block";

    }, actualElement);
```

</div>

<!-- Dive into chrome dev tools and then the code -->

---
name: Executing a Script Exercise
---
# Executing a Script Exercise <MarkerTipsAndTricks />

Change the `background-color` of the notification to `limegreen`

Use the existing tests as examples in `tests/tipsAndTricks/executingScript.test.js`

> Tip: When verifying that you have changed the color use `browser.getCSSProperty(element)` to get the value <br/> <br/> https://webdriver.io/docs/api/element/getCSSProperty/

---
name: Multiple elements
---

# Multiple Elements <MarkerTipsAndTricks />

Working with a list of data is perfect for getting multiple elements

Use Cases: 
- Checking the number of those elements that are on the page
- Checking that all items have a name and price
- Have no way to differentiate items (resort to using position, not ideal but a solution)

---
name: Multiple Elements Exercise
---
# Multiple Elements Exercise <MarkerTipsAndTricks />

Verify that there are 9 lamp cards on the QW Store Homepage

Use the existing tests as examples in `tests/tipsAndTricks/multipleElements.test.js`


<!-- 
    // assert the size of the elements array
    expect(listOfCardElements).toBeElementsArrayOfSize(9);
 -->

---
name: File Upload 
---
# File Upload <MarkerTipsAndTricks />

Uploading a file with automation should complex but it's very simple

When you use the mouse to upload a file, you have to interact with a file picker

Automation is very different, instead we are just setting the file path value to the `input` field

<div v-click>

```js
  const eleFileUploadInput = $("#file-upload");

  eleFileUploadInput.setValue(filePath);
```

</div>

---
name: File Upload Exercise
---
# File Upload Exercise <MarkerTipsAndTricks />

Verify that you can upload a file successfully from your computer

Use the existing tests as examples in `tests/tipsAndTricks/fileUpload.test.js`

> The assertion should verify the name of the file you uploaded (it could be a partial part of the name)

---
name: Basic Authentication 
---
# Basic Authentication <MarkerTipsAndTricks />

Some websites are gated for security reasons. Example, the FOX team have a gated QA website

The browser presents a popup for you to enter your username and password but there is no way to interact with it

<div v-click>

We can bypass this by adding the username and password to the URL in a specific format

```bash
http://username:password@example.com/
http://sharding:superStrongPassword2021@example.com/
```

* the browser will take this information and authenticate your script accordingly

Example: https://the-internet.herokuapp.com/basic_auth

</div>

---
name: Basic Authentication Exercise
---

# Basic Authentication Exercise <MarkerTipsAndTricks />

Verify that you can successfully use basic authentication 

Update the test in `tests/tipsAndTricks/basicAuthentication.test.js`

```js
 it("Verify that the user can enter gated website", () => {
    browser.url('https://the-internet.herokuapp.com/basic_auth');
    const header = $("h3");
    header.waitForDisplayed();
    expect(header.getText()).toEqual("Basic Auth");
  });
```

<br/>
<br/>

> Use variables for the username and password

---
name: Incorporating Different Testing Types
layout: center
class: text-center
---
# <CustomHeader> Incorporating Different Testing Types </CustomHeader>

Data-Driven Testing | Visual Testing | Cross-Browser Testing

---
name: Data-Driven Testing 
---
# Data-Driven Testing <MarkerOtherTestingTypes />

What is data-driven testing? 

<div>

<v-clicks>

- A way of executing tests dynamically based on data
- The data indicates what is to be tested and what is validated
- Does not have hard-coded inputs and assertions in the test script

<img class="object-contain mt-5 h-70 w-full rounded" src="https://seetyah.s3.amazonaws.com/Untitled%20Document.jpg" /> 

</v-clicks>


</div>

---
name: Data-Driven Testing - Pros/Cons
---
# Data-Driven Testing <MarkerOtherTestingTypes />

<div class="flex justify-between">

<div>

### Pros

- Changing test script or test data does not affect each other
- Performing regression on a large set of cases can be a breeze
- Ultimately increasing test coverage

</div>

<div>

### Cons

- Quality of the test is dependent on the programming skills of the implementer
- Debugging errors can be hard if the implementer is inexperienced in using the language

</div>

</div>

---
name: Data-Driven How to
---

# Data-Driven Testing (How to) <MarkerOtherTestingTypes />

The more you understanding the programing language you are using, the better it is

<div v-click> 

Let's go to the code!

</div>

---
name: Automated Visual Testing 
---

# Automated Visual Testing <MarkerOtherTestingTypes />

[What is automated visual testing?](https://applitools.com/blog/visual-testing/) 

<v-clicks>

- It's using software to compare visual elements across various screen combination to find visual bugs
- Automated visual testing evolved from functional testing (which is a simpler and more effective process)
- Good to use after unit testing, API testing, and before functional testing

<div class="mt-10">

- [applitools](https://applitools.com) - Cloud base visual tests.
- [percy.io](percy.io) - Continuous visual reviews for web apps.
- [Visual Regression Tracker](https://github.com/Visual-Regression-Tracker/Visual-Regression-Tracker) - Open Source selfhosted service for visual regression testing

</div>

</v-clicks>

---
name: Automated Visual Testing - 2
---

# Automated Visual Testing <MarkerOtherTestingTypes />

<div class="flex justify-between">

<div>

### Applitools

<img class="object-contain h-60 mt-10" src="https://seetyah.s3.amazonaws.com/Screen%20Shot%202021-06-22%20at%206.23.05%20PM.png" />



</div>

<div>

### [Percy.io](https://percy.io/62d281ae/qw-store/builds/11009248/changed/618305482?browser=edge&browser_ids=14%2C16%2C17&subcategories=approved&viewLayout=side-by-side&viewMode=new&width=1280&widths=375%2C1280)

<img class="object-contain h-60 mt-10"  src="https://seetyah.s3.amazonaws.com/Screen%20Shot%202021-06-22%20at%206.27.12%20PM.png" />

</div>

</div>

---
name: Automated Visual Testing (How to)
---

# Automated Visual Testing (How to) <MarkerOtherTestingTypes />

Automated Visual Testing is supported by most automation frameworks, you ony need to integrate with your current project

<div v-click> 

Let's go to the code!

What do we need: 
- API Key for whatever service will be using
- Plugin for the framework we are using

</div>

---

name: Automated Cross-Browser Testing
---

# Automated Cross-Browser Testing <MarkerOtherTestingTypes />

What is automated cross browser testing?

<v-clicks>

- Using automation to test web application compatibility with any browser (desktop, tablet, mobile)

</v-clicks>

---



