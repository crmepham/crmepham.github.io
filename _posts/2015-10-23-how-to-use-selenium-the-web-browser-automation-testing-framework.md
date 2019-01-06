<a href="http://www.seleniumhq.org/" target="_blank">Selenium</a> is a framework that can be used to automate tasks on a Web front-end. It provides a set of browser specific WebDrivers that integrate well with existing Unit tests, and supports many language-specific bindings to control what happens in the web browser.

The idea behind having an integration testing suite is to gradually build up a set of tests that can be ran every time a new feature or code change is introduced to a product. These tests are run to ensure robustness in a system; by making sure existing functionality is not broken when new features are introduced. 

Similar tests should also exist to ensure that the existing work-flows in a system are not broken in anyway after new features are added.

<strong>What is a work-flow?</strong>

In terms of the front-end, a work-flow is simply a set of actions the user must perform within the web browser to complete a certain task.

For example:

<em>Accepting a friend invitation on Facebook.</em>
This work-flow would consist of the following:

1. Navigate to the Facebook login webpage
2. Enter your username and password
3. Click the login button
4. Click the friend notification button
5. Click on the Accept friend invitation button

When you break down this work-flow in to its individual actions, you realise that there are a number of points where the work flow could potentially be broken if new functionality is introduced. So this is one workflow you might automate and include as part of a test suite that is ran every time a new feature is introduced.

Next, I'll create the test which will automate the above workflow and then check that it was successful by checking that the friend I accepted is in my friends list.

<script src="https://gist.github.com/final60/04dad9e7d9ba61731561.js"></script>
In the above example you can see that in the JUnit setup method I have instantiated a new Firefox web driver, because I want to use the Firefox browser for the automation. But other browsers are also supported.

Next I send myself a friend invitation using a test account so that when the test runs I will have something to validate against.

In the testLogin() method I am opening a new Firefox browser and navigating to Facebook using the get method. I am then inputting my email address and password, and then logging in.

Next I need to validate that I did indeed successfully login. I can do this next by attempting to get my name from the value of the link at the top of the list of navigation elements on the left of the screen I should now be on. If the resulting String is null or doesn't match "Chris Mepham". The we can safely assert that the login was unsuccessful.

The next test will test whether the accepting of a friend functionality is working. This is done my automating the process of clicking on the friends notification icon at the top of the screen, waiting for the subsequent submenu to appear, and clicking Accept on the first friend invitation that is listed. Next I need to validate that this action did infact accept the friend invitation. I do this by navigating to the friends section of my profile and searching for "Joe Bloggs" in my friends list. If a list element exists with the value of "Joe Bloggs" then the test passes.

<strong>Selenium IDE</strong>
Selenium provides an IDE that allows you to record the work flow you wish to test and export it to the relevant programming language/Unit testing framework of your choice. Here is a great little <a href="https://addons.mozilla.org/en-US/firefox/addon/favorites-selenium-ide/" target="_blank">Firefox plugin</a>. This method allows non-technical people the ability to contribute to front end testing by generating the relevant Unit tests containing the automation code without having to actually code any of it. The slight down side to this, however, is that it tends to include a lot of boiler-plate code and ambiguous element identifiers.
