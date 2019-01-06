---
ID: 120
post_title: >
  The three pillars of Object Oriented
  Programming
author: crm
post_excerpt: ""
layout: post
permalink: >
  http://chrismepham.co.uk/blog/programming/the-three-pillars-of-object-oriented-programming/
published: true
post_date: 2015-05-19 12:37:18
---
Object Oriented Programming (OOP) is a model for programming, whereby data and procedures are organised around objects. Where each object represents an entity or "thing" which contains data and procedures that are relevant to itself.

For example: A Cat can be modelled in OOP. A Cat is a thing. It has attributes including: age, name and mood. It also has logical actions such as: jump, eat and sleep.

Furthermore, a Cat is a mammal and a descendant of a Tiger and inherits many of a Tigers characteristics. There is also a lot of private information about a Cat that we didn't specify above, this information the Cat keeps to itself, such as: Blood Temperature and favourite sleeping spot.

Before OOP, programs were developed in a very linear way, by taking in data, processing it and outputting a result. Programs were written in a "step-by-step" or "top down" way, where the programmer would write every step of the program and the program would execute these steps line by line.

OOP, on the other hand, groups it's data and methods into objects and has those objects interact with one another. Programmers will work out which classes need to be created to contain which functionality of the program. This is known as "data modelling".

A class is basically a blue print for what an object should contain once it is instantiated.

OOP eliminates the duplication of code. By dividing the program up in to objects containing specific functionality. An objects methods can be called multiple times to reuse the containing logic. This greatly reduces the amount of code the programmer needs to write and, in turn, makes the program easier to read and easier to maintain.

The three main concepts of OOP are Inheritance, Polymorphism and Encapsulation.

<strong>Inheritance
</strong>Inheritance is when an object inherits attributes and functionality from one or more superclass (or parent class). There are two main types of inheritance: Singular and multiple. C# and Java both utilize singular inheritance.

Singular inheritance is when a class inherits properties from just one single super-class, and multiple inheritance is when a class can inherit properties from multiple classes. Although this approach is not common and regarded as very difficult to implement and maintain.

Multiple inheritance was implemented in older programming languages such as C++ and Python. Java and C# both decided to omit multiple inheritance because it didn't fit into their philosophy of a simplistic, easy to learn and familiar programming language.

Although C# and Java are both strictly singular inheritance, they both can implement multiple interfaces which enables them to utilize some of the functionality that multiple inheritance offers. For example: if you want to create an object to represent a talking dog - in multiple inheritance you would have been able to simply inherit from two super-classes - a dog class and a human class (to get the talking logic).
In Java and C#, however, you would only be able to inherit from one super class and then implement an interface that specifies logic to speak. So although you are strictly only inheriting from one class, you are getting the functionality from multiple sources.

[caption id="attachment_135" align="aligncenter" width="1087"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2015/05/inheritance.png"><img class=" wp-image-135" src="http://chrismepham.co.uk/blog/wp-content/uploads/2015/05/inheritance.png" alt="Inheritance diagram" width="1087" height="621" /></a> Inheritance Diagram[/caption]

Inheritance allows for re usability of code. Instead of writing the same code multiple times throughout a program, a developer can simply create a class containing a method with this functionality and call this method multiple times.

Inheritance also allows for extensibility. If a base class doesn't contain specific functionality that is required, a more specific class deriving from the original, more abstract class, can be created. Now the original functionality can still be used but more can be created in the new class.

<strong>Polymorphism</strong>

Polymorphism means "many forms". In the context of OOP it refers to an objects ability to derive from a general super-class and change the behaviour of that class to fit the objects more specific needs.

Take the following code as an example:
<script src="https://gist.github.com/final60/97db49eb8a6fdc68a2ff.js"></script>

Output:

<blockquote>
Woof!!! My name is Fred
Meow!!! My name is Jerry
Woof!!! My name is Fred
</blockquote>

In the above example, you can see that the Dog and Cat objects are considered polymorphic because they are both a Mammal and an Object. The rule of polymorphism states that an object is only polymorphic when it passes more than one "IS-A" test. In the above example the Dog object "IS-A" Mammal and it "IS-A" Object.

When instantiating a polymorphic object you can use the super-class Datatype to instantiate any sub-class. You can see this demonstrated in the above example when I instantiated an animal object using the super-class Object. Polymorphism is useful for writing less and cleaner code. 

In the above example I have used a simple "for" loop to iterate over the mammal array and execute each of the containing objects "speak" methods. Alternatively I would have had to a) know how many objects I have instantiated and b) call each of these objects speak methods individually. This becomes a very unreliable method when used in large systems where hundreds or thousands of different objects are being dynamically instantiated, and finally c) when using a super-class datatype we can call the speak method on any sub-class without knowing what objects will be instantiated.

<strong>Encapsulation</strong>

Encapsulation in OOP is the process of "data hiding". It prevents other developers, working on your code, from making mistakes, by making sure that they only ever have access to code they can use and nothing else. There are three types of encapsulation in OOP: Private, Protected and Public. 

When a field or method is marked as Private only the methods within that class can access the values of the private field.

When a field is marked as Protected only other classes in the same hierarchical class tree can access the values of those fields. That is, only an object that is inheriting from this class.

When a field is marked as Public all classes and methods in the same package/namespace can access the fields value.

In OOP each class will contain fields and methods relevant to itself. The other classes within a program should not need to know how the data within another class is being stored.

By default all fields and methods are package/namespace private and marked as public unless otherwise specified. It is, however, best practice to mark a classes fields as private and provide access methods known as "getters" and "setters" (or "properties" in C#) to be able to access the values of these private fields. The same goes for a classes methods. If the class is going to use a method internally then it should be marked private, and therefore hidden from the rest of the program which doesn't need to know that these private fields and methods exist.

<script src="https://gist.github.com/final60/b38c234a0cfbfc66092c.js"></script>

output:


<blockquote>Chris has ridden an average of 33 miles, per ride, this week.</blockquote>

By setting fields as private and providing access methods, we are further decoupling the object from the rest of the program which doesn't need to know the distance of each ride and how many rides he went on this week. It only needs to know the average distance he travelled. It is this kind of abstraction that makes Encapsulation and OOP very powerful.