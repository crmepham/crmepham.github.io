Java enables developers to both <strong>override</strong> and <strong>overload</strong> methods in sub-classes. I will briefly describe the differences between the two and the process of method hiding when overriding a static method.
<h2><strong>Overriding</strong></h2>
Overriding is useful when you want to change the body of a method that is inherited from a super-class. Take the following example:

<script src="https://gist.github.com/final60/929b367acddf1a84b497.js"></script>Output:

<blockquote>
3

9
</blockquote>

In the above diagram you can see that I created a class called <strong>Dog</strong> which extends <strong>Animal</strong>. In the Dog class I overrided the <strong>getAge</strong> method, so that it converts the dogs age from a primitive integer to a short before returning the value to the calling program.

In the main method I created two object references of type Animal. At run-time ( when the program is run) the first one will reference the Dog object, and the second will reference the Animal object.

Finally, when the getAge method is called on each object, the version of the method in the object that the reference points to, is called. There are a few rules to overriding methods, for it to work though:

1. The overriding method must specify the same number of parameters and the parameters must be of the same type, and in the same order.

2. The return type in the sub-class must be a co-variant of the return type in the super-class. This means that the return type must be a sub-class of the return type in the super-class. In the example above Short is a sub-class of Number. If I was to specify a String or any primitive as the return type or any Object that does not extend from Number, the program would not compile.

3. The access level of the sub-class cannot be more restrictive than that of the super-class. For example: if the sub-class was set to private and the super-class' method is public, the code would not compile.

4. If the method in the super-class is marked as final than it cannot be overriden.

5. Static methods cannot be overrided, but they can be re-declared in the sub-class (more on this later).

There are more rules, covering accessibility and Exceptions, but these five cover the main bones of contention.

<strong>Overriding a Static method</strong>

It is not possible to override a method that is marked as static. But it can be re-declared in the sub-class. This means that when you are doing what looks like overriding in the sub-class, you are actually hiding the super-class version of the method all together, and do not have access to it during run-time.

<h2><strong>Overloading</strong></h2>

Overloading is useful when you want to provide different versions of a method. This will provide the option of passing different numbers of arguments to the method at different times. Take the following example:<script src="https://gist.github.com/final60/971a3138b739766bd8a5.js"></script>

&nbsp;

In the above example you can see that I have specified multiple constructor methods, each expecting different parameters to be passed. This is useful in instances where someone doesn't know certain details of a dog. For example: in a program that a vet might use to register a stray dog that has been brought in. Because there is a no-argument constructor specified. The vet can still record the dog in the system, without knowing its age or name.

<strong>Primitive promotion</strong>

Take the following example:

<script src="https://gist.github.com/final60/9fc31e135cecf5ba3f86.js"></script>
In the above example you will notice that when I instantiate a Dog object I pass it the byte variable dogAge. But in the Dog object there is no constructor that expects a byte to be passed to it. One constructor expects an int, and the other expects a float.

Because there is no constructor that expects a byte, Java will automatically use one of the available overloaded methods with the "least widening"  datatype. A byte datatype can hold a value between -128 and 127 which can fit inside an int ( which can hold a value between -2<sup>31</sup> and a maximum value of 2<sup>31</sup>-1). A float can hold an even greater range of number. So the compiler will select the constructor expecting an int and convert the byte to an int automatically. If the int constructor didn't exist, the compiler would choose the constructor expecting a float, again, because a byte value can fit inside a float type.
