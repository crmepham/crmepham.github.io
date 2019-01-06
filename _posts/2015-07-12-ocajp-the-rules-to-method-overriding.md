I will explain many of the rules that must be adhered to when overriding a method in Java, and explain some of the key terms surrounding the process of overriding.

First to explain a couple of things!

<strong>Static methods</strong>
A static method is a method that belongs to the class, as opposed to an instance of the class, which is when an object of the class is created - where the object has it's own copy of the class methods and fields that are unique to itself.

You would make a method static when the method does not relate to a single instance of the class. For example: say you have a bicycle class and want to output the name of an instance bike.
<script src="https://gist.github.com/final60/4a01ce24fafe76998d1c.js"></script>
You could argue that the "printBicycleName()" method belongs to the class because it is not doing anything that would be considered unique to an instance of that class. Notice also how static methods are called using the class name and dot notation, as opposed to using an object reference.


<strong>Virtual methods</strong>
A virtual method is a instance method that can be overridden in a sub-class. In Java all methods are considered "virtual" as long as they are not marked static, final or private. 

<strong>a)</strong> Static methods are not considered virtual because the original method is merely shadowed, or hidden by the new method in the sub-class.

<strong>a)</strong> final methods are not considered virtual because the final keyword is explicitly used to identify a method that should never be overridden.

<strong>c)</strong> private methods are not considered virtual because they belong only to the class they are created in and cannot be inherited in a sub-class. Therefore they are hidden.


<strong>Why would I override a method?</strong>
Overriding a method is an important aspect of Polymorphism. When a subclass is instantiated and you want to change the body of a method in a more generic superclass, to one that more accurately describes the more specific behavior of a subclass.
<script src="https://gist.github.com/final60/8998d5d0a636671f284d.js"></script>
In the above example I have overridden the method "speak()" in the generic abstract superclass. To more accurately depict the behavior of a dog.

And to the rules:

1. If overriding a <strong>non-private static</strong> method, the overriding method must also be static(<strong>hiding</strong>). Conversely, neither method should be static (<strong>overriding</strong>).

2. If the superclass method if marked as private the method can only be hidden and not overriden.

3. The return type of the overriding method must be a covariant (same class, or a subclass) of the overridden method return type. If the return type is a primitive datatype, it must match exactly.

4. If the overridden method throws a checked exception (any exception that is not a subclass of runtimeException), the overriding method does not need to re-declare the exception and it can declare a subclass of the overridden methods exception. It CAN'T declare a broader exception than the overridden method exception however. Conversely it can declare any unchecked (runtime) exception.

5. The overriding method cannot declare a more restrictive access modifier than the overridden method.

6. A method marked as final cannot be overridden or hidden.

7. A constructor cannot be overridden.

<strong>In summary:</strong>
Remember that member variables and static methods are <strong>NOT </strong>overridden <strong>ONLY </strong>virtual methods are, so access to them is determined at compile time based on the type of the reference variable. Virtual methods are determined based on the object type at runtime.
