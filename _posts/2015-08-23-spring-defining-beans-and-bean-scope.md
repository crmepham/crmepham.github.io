In this tutorial I will be defining beans in a Spring Bean configuration file. This configuration file will be used to automatically instantiate and inject beans into relevant objects automatically. This tutorial assumes you have a new Spring project environment setup, which you can learn how to do <a href="http://chrismepham.co.uk/blog/guide/how-to-setup-your-eclipse-ide-for-your-first-java-spring-project/">here</a>.

<strong>Creating a bean configuration file.</strong>
In your "src/main/java" directory, create a new package called "com.crm.spring-beans". Now right-click this new package and click "New" -&gt; "Other..." -&gt; "Spring" -&gt; "Spring Bean Configuration File". Give it a name of "beans", click next, and select "beans" from the check-box list of possible namespace declarations.

This will generate a new Spring beans XML configuration file where I will define all of my beans.

<strong>Create application classes</strong>
For this example simply create a new package under "src/main/java" called "com.crm.spring-tutorial" and create the following classes:

<script src="https://gist.github.com/final60/0591d80c85b86a8975d8.js"></script>

<script src="https://gist.github.com/final60/9380837c8da2272b7dda.js"></script>

<script src="https://gist.github.com/final60/a4275ca442a3d28eb94b.js"></script>

<script src="https://gist.github.com/final60/f5387cc79a4b0166ceb2.js"></script>

<strong>Dependency Injection</strong>
One of the strongest features of the Spring framework is it's ability to automatically inject objects by either passing them into an objects constructor or by passing them via setter methods. This is great because it removes tight-coupling within a program. With Spring an object doesn't need to care where the object comes from or how it is configured because Spring takes care of that in the bean configuration file.

Here's the configuration file for our beans:
<script src="https://gist.github.com/final60/ae731b422dc2d3fff902.js"></script>
Like any other XML configuration file - properties are defined within opening and closing tags and are given an attribute name and value.

In this basic configuration file I am using the XML namespace for "beans" and a couple of other standard Bean configuration namespaces that all bean configuration files must have. Underneath you will see that I have defined each bean using the "< bean >< /bean >" tags. In the Human and Dog beans I have given them relevant id's so that they can reference each other, defined the fully qualified name for each class the beans represent and provided the constructor arguments that each object expects when it is instantiated. The Car bean represents a class with a default "no-argument" constructor so no constructor arguments need to be defined. But I have defined a property that will be set when the Car object is instantiated, setting the name of the Car. The key difference here is that this property isn't compulsory like the constructor arguments of the other two beans are.

<em>The general rule of thumb is that properties set by the constructor are mandatory, whereas properties passed by setters are not.</em>

You can have as many beans of the same class type as you want as long as they have attributes that prevent ambiguity, like a unique ID.

In future I will discuss other methods of selecting beans, for example: byType, and how to prevent ambiguity between the same bean classes.

Now for the main class that will run our program:
<script src="https://gist.github.com/final60/0d485518a3c64ee2f154.js"></script>
Output:

<blockquote>Mark
Mark</blockquote>

In the above example I am first setting the ApplicationContext. This is telling Spring where to look for the bean configuration file. Next I am getting a human bean from Spring and assigning it to the reference variable "human". Next I am getting what seems like another human bean from Spring, assigning it to human2 and then changing it's name from the default "John" to "Mark". But then why, when I print out both object names to the console, are they both called "Mark"?

The reason is because of the default bean scope behavior in Spring. Beans have a default scope of "singleton" unless otherwise specified. Which means that when the program first runs, Spring will create only 1 Human object, and no matter how many times the program wants a new Human object, Spring will only pass it a reference to the one object in memory. To change the scope of a bean you simply need to add the attribute <strong>scope="prototype"</strong> to the human bean in the bean configuration file. Now every time the program asks for a new Human object, Spring will actually make a new object in memory.

This covers a very simple implementation of Spring auto-wiring using the Spring XML configuration file. In another post I will discuss how to create a similar implementation using Spring annotations.
