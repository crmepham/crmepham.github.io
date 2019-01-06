---
ID: 297
post_title: 'OCAJP: When to use an abstract class or interface'
author: crm
post_excerpt: ""
layout: post
permalink: >
  http://chrismepham.co.uk/blog/certification/ocajp-when-to-use-an-abstract-class-or-interface/
published: true
post_date: 2015-07-13 15:42:26
---
The Java programming language provides both abstract classes and interfaces that, to a newcomer, appear to provide very similar functionality to a class, but they should be implemented for different reasons. 

An interface should be seen as a contract. Any class that implements that interface is promising to implement the declared methods, those methods must be public and any declared variables are final and cannot be changed (Since Java SE 8 Oracle has realized that C++ was correct - that multiple inheritance has valid uses and thus allows interfaces to now provide a default body to a method, which helps with backwards compatibility, whereby a method can be added to an existing interface without legacy code having to be altered to implement the new method declaration, provided the method is marked as static or default).

An abstract class should be used as a base class for classes that contain similar polymorphic behaviors, and is generic enough that it doesn't need to be instantiated itself. An abstract class is less strict about its implementation, given that it can contain a range of encapsulation choices, a default method body can be provided, it can contain methods that are not abstract and therefore do not need to have a concrete implementation, and although it can contain static final fields, it doesn't have to.

<strong>So when would you use an abstract class instead of an interface?</strong>
Let's use our trusty old, simple Mammal example.
<script src="https://gist.github.com/final60/e4cefaaee75b151119cf.js"></script>
In the above example you will notice that you can declare concrete declarations of variables that don't have to be declared in a concrete subclass. All methods marked as abstract must be implemented in a subclass. Currently we have an abstract class that defines generic attributes and behaviors of a Mammal. This is the best use of an abstract class.

So currently in our hypothetical program lets assume that only certain types of Mammal can speak. That would mean our abstract implementation of the speak method in the abstract class could be redundant in some cases, where a subclass will not want to implement it, even though it has too be.

So lets improve the code a bit.
<script src="https://gist.github.com/final60/d0ee3a533ceb0d50ace9.js"></script>
In the above example we still have our abstract class which defines the base characteristics of the Mammal. What a Mammal is - it's core identity. But now we have separated the abstract speak method into its own interface. This is more appropriate because interfaces are good for defining things that classes can do, rather than it's full identity. So as you can see above we now have a dog, with an identity, but it can also do something, which in this case is speak. Now not all animal classes that descend from the Mammal class can speak, only our special, super hero dog can speak.

<strong>Some key things to remember:</strong>
<strong>1.</strong> A class can implement multiple interfaces, but only a single abstract class.

<strong>2.</strong> An abstract class cannot be directly instantiated, nor can an interface.

<strong>3.</strong> An abstract class can provide default behavior and values. In interfaces, fields are marked as <strong>static final</strong> by default and so their value cannot be changed. Since version 8 of Java, interfaces can provide a body to a method, provided it is marked <strong>default</strong> or <strong>static</strong>.

<strong>4.</strong> An interface can extend another interface, and an abstract class can extend another abstract class, but one cannot extend the other.

<strong>5.</strong> An abstract class that implements an interface does not have to implement the interfaces methods. This is the job of the first concrete class that extends the abstract class.


<strong>To summarize:</strong>

You would use an abstract class instead of an interface when you want to establish the base identity of a class hierarchy with the intention of producing sub-classes for polymorphic overriding of the base classes methods.

You would only use an interface to define specific actions that entirely unrelated classes can do. For example a talking dog is entirely different from a human, except for that fact that both can speak.