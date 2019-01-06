---
ID: 349
post_title: 'OCAJP: Lambda Expressions and the Predicate interface'
author: crm
post_excerpt: ""
layout: post
permalink: >
  http://chrismepham.co.uk/blog/certification/ocajp-lambda-expressions-and-the-predicate-interface/
published: true
post_date: 2015-07-20 13:55:50
---
With the release of Java version 8, came the ability to write Lambda expressions, to be used with functional interfaces. Java 8 includes a few functional interfaces, including: Runnable, Callable, Comparator and <a href="https://docs.oracle.com/javase/8/docs/api/java/util/function/Predicate.html">java.util.function.Predicate</a>, to name a few. For the OCAJP exam you will only need to know how to write a valid Lambda expression for use with the Predicate interface.

<strong>What is a Lambda expression?</strong>
A Lambda expression is essentially functional programming that allows a developer to write short, clear and concise code to replace previously necessary anonymous classes to implement functionality. It is also very useful for preventing duplication in code and for sorting Collections.

In relation to the Predicate interface; Lambda Expressions can be used to evaluate an expression to return a boolean result, which is the datatype the Predicates test() method returns.

The basic building blocks of a Lambda expression are:
<strong>a)</strong> zero or more parameters to pass
<strong>b)</strong> the -> (arrow) that separates the parameters and the boolean expression.
<strong>c)</strong> the expression that must evaluate to either true or false when used with the Predicate interface

<strong>and the rules:</strong>

<strong>1)</strong> You can pass zero or more parameters, but when basic zero you must used empty parenthesis <strong>()</strong>.
<strong>2)</strong> If passing one parameter no parenthesis or datatype is required. If passing more than two parameters than you must wrap them in parenthesis.
<strong>3)</strong> If passing more than one parameter and they are of different datatypes, include the datatype declaration.
<strong>4)</strong> If you are using more than one expression, wrap all expressions in curly braces.
<strong>5)</strong> If you use the return keyword before the expression, you must include a semi-colon after the expression.

Some examples of valid Predicate Lambda expressions:
<script src="https://gist.github.com/final60/bb84a6b9d45f9395d232.js"></script>

<strong>What is a functional interface?</strong>
A functional interface is just a normal interface that has only one single abstract method (SAM). So that it can be used with a Lambda expression, where the Lambda expression is matched with the single interface method. A functional interface can have multiple static and default methods defined, but it can only have one abstract method. 

<strong>The Predicate interface</strong>
Java 8 includes a built in functional interface called <strong>Predicate </strong>which can be used with a Lambda expression and passed into a method, where its <strong>test()</strong> method can be used in a boolean statement to check a condition. Predicate permits Generics to be used, so that a boolean check can be performed on any datatype.

Here is an example without using Lamba and Predicate:
<script src="https://gist.github.com/final60/17fa9d71330cd0d41033.js"></script>
This program is used to sort our list of Dog's. We can currently sort them by either age, or name. The program works fine as it is but is using duplication for the <strong>getDogByAge()</strong> and <strong>getDogByName()</strong> methods, and what if we wanted to sort the list by more attributes or a combination of attributes? The code would soon become verbose, as more and more methods would be needed.

Let's improve the above code:
<script src="https://gist.github.com/final60/28ddedf9e9ae2fc5c985.js"></script>
In the above example, instead of passing the condition parameter into the method, we are passing the Predicate interface of Type Dog. We have gotten rid of the duplicating methods and replaced them with a more generic method, but crucially you will notice that we have removed the conditional check that sorts the list and replaced it with the predicates test() method, which allows us to use any Lambda boolean expression we wish to pass to the method.

So now we can get the same two lists from the first example by just using simple Lambda expressions and the Predicate interface that expects a Dog object, instead of writing specific methods. I have added a third method call, containing a Lambda expression that includes two conditional checks, to demonstrate that we can sort the list based on far more conditions now, using far less code, thanks to functional programming.