Exceptions are thrown by a program when something goes wrong! It is Java's way of telling you something has happened that it wasn't expecting and it doesn't know how to handle the problem. So it just tells you, usually by printing out a stack trace of the error.

Exceptions fall into two main categories - <strong>checked</strong> exceptions and <strong>unchecked</strong> exceptions.

Both checked and unchecked exceptions are throw-able, and are all classes that extend from the super-class "Throwable".

[caption id="attachment_178" align="aligncenter" width="485"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2015/06/exceptionClassHierachy.gif"><img class="size-full wp-image-178" src="http://chrismepham.co.uk/blog/wp-content/uploads/2015/06/exceptionClassHierachy.gif" alt="exception Class Hierachy" width="485" height="385" /></a> Exception Class Hierarchy diagram by Pascal Thivent[/caption]

As you can see by the diagram above, unchecked exceptions ( exceptions not checked at compile time) are "RuntimeException" and its sub-classes, and "Error" and its sub-classes. Unchecked exceptions are exceptions generally caused <strong>internally</strong> to the program and are generally caused by poor programming, they are exceptions that a program can not reasonably be expected to recover from, but in some instances are (demonstrated in diagram below).

Some common examples of Runtime Exceptions include: Arithmetic exceptions - when dividing by zero, when attempting to access an object through a null reference (NullPointerException), and when attempting to access an array element that doesn't exist (ArrayIndexOutofboundsException).

Here are some code examples:
<script src="https://gist.github.com/final60/a71d08585006b4dbe585.js"></script>and some methods of dealing with the above run-time Exceptions:<script src="https://gist.github.com/final60/01987f28bc01802dde48.js"></script>
In the above example you will notice that in some cases you do not actually have to throw or handle a run-time exception. To prevent the ArrayIndexOutOfBoundsException, assuming we are attempting to get the last element in the array, I used a simple if statement to make sure that if the variable "num" was larger than the length of the array, then to set the value of num to the value in the last element of the array.

Checked exceptions are exceptions that are checked during compilation of a program, and require a programmer to declare them either using a <strong>throws</strong> clause in a method signature or by declaring them in a <strong>try-catch</strong> statement. They are generally recoverable problems which are caused <strong>externally</strong> to the program: e.g. reading data from a file, hard-drive disconnected, or a database being offline.

If a throws clause is used then the Exception does not have to be handled in the method body and will be passed back to the calling program, where it can either be handled or thrown further to its calling program, until it reaches the main method, where if it isn't handled the program will stop running. This is known as the <strong>"Catch or Declare"</strong> rule.

Here is an example, assuming incorrect syntax is used in an SQL SELECT query:
<script src="https://gist.github.com/final60/561f56b00a095fe28d93.js"></script>
In the above example I am attempting to contact an SQL database, this could potentially cause an <strong>SQLException</strong> which is a sub-class of <strong>Exception</strong> and <strong>NOT</strong> a sub-class of <strong>RuntimeException</strong> or <strong>Error</strong>. So it must be handled or declared. In this instance I decided to throw the exception to the calling method main(), where I handled it using the try-catch statement, which prints a stack trace log containing information of what specifically is wrong and on what line of code the error occurs.

<strong>Error</strong>

These are Exceptions that occur that should not be handled or declared at all. Errors are usually rare and are generally irrecoverable. One example is the "StackOverflowError" exception which is caused when a method calls itself causing an infinite loop of declaring local variables which sit on the stack ( a space in memory reserved for variables). During an infinitely recursive method call these method declarations will eventually fill up the stack and cause the program to run out of memory. The JVM is smart enough to spot when code is calling itself recursively and will throw a StackOverflowError.

&nbsp;

&nbsp;

&nbsp;
