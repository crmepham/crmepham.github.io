In this tutorial I will explain what Unit and Integration testing are and the differences between them in JUnit 4. 

Testing is an important aspect of software development. During the development of an application, a lot of changes may occur, over a large period of time, and mistakes can happen regularly. As changes are made to software it is necessary to test the new functionality and make sure that this change hasn't had a negative effect on any existing code in the application.

<strong>What is Test Driven Development?</strong>
Test-driven development (TTD) is a development process with a short development life cycle, in which a developer will write a piece of logic using the least amount of code necessary to fail a unit test. The developer will then improve the code by the least amount possible to pass the test and then continue to re-factor the code whilst continuing to pass all test's.

<strong>What is JUnit?</strong>
JUnit is an open source testing framework written for the Java programming language. It comes pre-installed with "Eclipse for Java EE developers", and provides a convenient user interface that developers can use to quickly reference and locate failing tests, and a large suite of classes and test suites.

<strong>What is the difference between a unit test and an integration test?</strong>
Unit tests are used by programmers to test that specific logic is working as intended. Unit tests are generally used to test small pieces of code and should not be dependent on any outside system. For example: if you have written a method that instantiates and populates an objects properties, then a successful test case would be that the object is not null, and another would be that the properties are equal to what the programmer expects. Conversely, a successful fail test would be that the object is null. Unit testing is also referred to as "Black box" testing. This infers that the test method doesn't worry about any dependencies or how it is passed it's data. It is only concerned with testing the state or logic within the method itself.

An integration test is used when you want to test that different parts of a system are working together correctly, or this bit of code works well with other parts of the application code. For example: you may want to test that some data created and sent from a GUI is successfully processed and stored in a database. This is known as "White box" testing.


<strong>Unit test class example:</strong>
<script src="https://gist.github.com/final60/aea11b27afc0861615c5.js"></script>
In the above example we have a DogTest class containing unit tests that each test a specific thing about either a dog or the dog list. When creating a JUnit test class it must first extend the JUnit "TestCase" class so it can access the many assert methods that the class provides.

Next you will notice the "setUp()" method. This method is run before each test is run. In the above example we are using this method to populate a list. But do we need to do this again every time we want to run a Unit test? Perhaps not in this case. In which case we could change the method annotation to "BeforeClass". In this case, however, we would have to make the method static, because it will be run before the class has been invoked.

Next you will notice that each test method has a prefix of "test" and contains the word "Should". The "test" prefix is mandatory, the "should" isn't. But it follows good naming convention. Also each method is annotated with "@Test".

<strong>Integration test class example:</strong>
<script src="https://gist.github.com/final60/294f5c4bcd9372d42453.js"></script>
In the above example the "setUp" and "tearDown" play important roles in setting up the conditions for the test, and then cleaning up the database after the test has finished. As you can see, we create a new Dog object with the name "TEST", so we can easily reference it in our test. Next we attempt to persist it to the database. But now we want to be sure that a) the Dog object was created successfully and B) it was persisted to the database.

In the test method we simply instantiate a new Dog object, using an object passed back from the result of querying a database for a row containing the value "TEST" in the "name" column. If the object returned from the query is not null then it found a row containing the name "TEST" and returned that row as an object.

Finally in the "tearDown" method we are simply deleting the row in the database that contains the name "TEST". This returns the state of the database back to how it was before we started testing. 

This integration test has tested that the applications database access object integrates with the database to persists Dog objects. We proved that it does by getting the Dog object back from the database after previously storing it there.

<strong>Test Suite</strong>
<script src="https://gist.github.com/final60/d07a06d9766ab39927b6.js"></script>
During the development of a large scale application you may build up many unit tests and integration tests in multiple class files. JUnit allows you to define a single class as a Test suite that will list all your unit tests.

<strong>Test Runner</strong>
<script src="https://gist.github.com/final60/2e88915ae4e73b26d0d8.js"></script>
Next is the Test Runner class which will load and run the tests from the TestSuite class and return a result of failures. Pretty simple, yet powerful stuff. Now we have one single application we can run when we want to run all of our applications tests.
