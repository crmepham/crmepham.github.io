In Java, the <a href="http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html">java.lang.Object</a> defines an equals() method for comparing another object to itself to determine if they are the same type of Object. The String class is a subclass of Object (like every other class) and overrides its equals() method to mean something completely different, as I'll explain further down. 

We can use the equals() method and the == operator to compare objects. But what is the difference between them?

Let's looks at the String object (which is a subclass of Object) and apparent string literals to explain the two methods of boolean comparison.

Firstly, what is the "string pool"?
<script src="https://gist.github.com/final60/35025bd2cdf820f11562.js"></script>
In the above example we have declared two Strings with literal values. Now, during compilation of a program, the compiler will optimize the string literals by looking for those literals that are exactly the same. If they are then only one String Object is created. So the term "string pool" merely represents the idea that before a new String object is created, the compiler checks if the string is already defined as the value of an existing String object, if it is then they will share the String object reference that points to the object containing that value.

So is the output of the following example <strong>true</strong> or <strong>false</strong>?
<script src="https://gist.github.com/final60/288fd1e7d8d81baebae0.js"></script>
The output is <strong>true</strong>.
Even though it seems like we have created two distinctly separate String objects, they have the same value, so the compiler optimizes them by making them point to the same String object (the same string literal in the hypothetical "string pool").

So what happens when we do this?
<script src="https://gist.github.com/final60/c9ce61f3a1e71fd3c60f.js"></script>
The output is <strong>false</strong>.
When we declare String b, we assign it the reference value that points to the location of the new String object we have just created in memory when we used the <strong>new String("a");</strong> statement. So even though the new object contains the value "a" it is not the same object as a. The compiler will only optimize Strings with literal assignments to point to the same object.

Next, let's compare two String objects.
<script src="https://gist.github.com/final60/5ab6d44ec04892601af7.js"></script>
The output is <strong>false</strong>.
In this example we have instantiated two distinctly different String objects. Variable a contains the reference pointing to the location of one String object in memory, and variable b contains the reference pointing to the location of an entirely different String object in memory. When comparing object references using the == operator, it is checking if both variables are pointing to the same object in memory. Not whether the objects they point to contain the same value.

So how can we check whether two String objects have the same value?
<script src="https://gist.github.com/final60/68120613b10b7ab20843.js"></script>
The output is <strong>true</strong>.
In Java the super class "Object" contains an equals() method that defines whether an object is the same type as itself. String is a subclass of Object and it has overridden the equals() method to return true if an object passed to it contains the same value that this String object contains. 


Finally, let's try comparing a string literal with a String object.
<script src="https://gist.github.com/final60/61f47ecd6632328f6c43.js"></script>
The output is <strong>true</strong>.
You might wonder why the output is true if we are passing what appears to be a string literal into a method that expects an object. During compilation the string literal is converted to a String object, so it can call the equals() method and compare another String object against itself.

In summary:
In Java there is no such thing as a primitive string datatype. So, unlike other primitive datatypes (int, short, float etc.), you cannot use the == operator to check for String value equality, because that operator is used only for reference equality. String overrides Objects equals() method to return true if the sequence of a String objects value exactly matches the sequence of its own value.
