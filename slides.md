---
# try also 'default' to start simple
theme: apple-basic
layout: statement
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
# class: "text-center"
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# some information about the slides, markdown enabled
info: |
  ## QualityWorks Internal Training.
---

# Next-level Test Automation

Scale your next test automation project.

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 p-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Let's Go! <carbon:arrow-right class="inline"/>
  </span>
</div>

<a href="https://github.com/dimitriharding" target="_blank" alt="GitHub"
  class="abs-br m-6 text-xl icon-btn opacity-50 !border-none !hover:text-white">
<carbon-logo-github />
</a>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---

# 💫 About Me

- 👨🏽‍💻 I'm a Tester by Profession, but a marker by Passion
- 🏢 Lead QA Consultant at **QualityWorks** in 🇯🇲.
- ✨ What I do daily: **Cook**, **Eat**, **Work**, **Code**, **Listen Music**, **Hack on Something**, **Sleep** <- Repeat
- 🎭 Hobbies: **Photography**, **Creating something (physically or virtually)**

---

# What will we be learning?

We'll be talking about structuring your test automation project, and we'll look at some automation practices that can make your life easier.

- 📤 **What are test frameworks made of?**
- 🛠 **Creating a structured test automation framework/project**
- 🧑‍💻 **Commands - Tricks & Tips**
- 🤹 **Incorporating different types of testing**

<br>
<br>

<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/guide/syntax#embedded-styles
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent; 
  -moz-text-fill-color: transparent;
}
</style>

---

# What are test frameworks made of?

> In general, a framework is a set of best practices, assumptions, common tools, and libraries that you can use across teams.

<br/>

> Test frameworks provide some of the benefits of increase reusability of code, higher portability, reduce test script maintenance cost and so on.

Testing Frameworks are normally compromised of the following:

- Hooks
- Test Runner
- Assertions
- Reporter

---

# Test Frameworks

- Java: TestNG, JUnit
- JavaScript: Mocha, Jasmine, AVA

> Fun fact - by default WebdriverIO uses Mocha as their test framework

---

# Test Frameworks - Hooks

> Hooks are blocks of code that you can execute **before** or **after** your tests, suites, etc.

---

# Examples of when hooks are used in your test automation

<div grid="~ cols-2 gap-4">
<div>

## Before

- Starting a webdriver server (this is mostly done automatically)
- Setting up a database connection for getting test data
- Loading test data (local/remote)
- Navigating to a certain page
- or anything else that your test might need to be executed properly

</div>
    
<div>

## After

- Shutting down webdriver server (again, mostly done automatically)
- Closing database connection
- Clearing test data
- Clearing browser cookies
- Taking a screenshot if there was an error
- Generating a report
- or post-action you would want to person after your tests are executed

</div>
</div>

---

# Mocha Hooks

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
});
```

---

# [WebdriverIO Hooks](https://webdriver.io/docs/configurationfile/)

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

# Tests / Test Runner

> Tests are blocks of code that contains the steps and assertion/s for your test scenarios. You can organize your tests by using different files or test suites.

<br/>

> A test without an assertion will always pass once there are no errors in any of the steps (your test should always have an assertion)

<br/>

> Tests are normally handled by a test runner

---

# Assertions

> An assertion is a check to determine if something is true (correct). [Chai](https://www.chaijs.com/) is an assertion library for node that provides handy methods that can be used for different assertions needs.

<br/>
Below are 3 examples of the different types of assertions you can use. Most of us assert or expect
<br/>
<br/>
<img border="rounded" src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6e40b922-2a6f-4ea2-9e35-efe571493358/Screen_Shot_2021-05-31_at_3.20.48_PM.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210610%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210610T154949Z&X-Amz-Expires=86400&X-Amz-Signature=4ac2f6bf02d9f666b9afe117ed3bb2efc2ed9c0141ea32bfad5a81e3cb83987b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Screen_Shot_2021-05-31_at_3.20.48_PM.png%22">

<!--

-->

---

layout: statement

---

# Thanks for coming!

[Slides]() / [GitHub Repo]()
