I thought this might be a good opportunity to share some of my learning by solving some programming problems I have found online.

<strong>The Problem</strong>


<blockquote>Write three functions that compute the sum of the numbers in a given list using a for-loop, a while-loop, and recursion.</blockquote>

<strong>Recursion</strong>
Recursion, in the context of programming, is when a method calls itself repeatedly while a certain condition is met.
<script src="https://gist.github.com/final60/3bd723d87e0436725044.js"></script>
In the above example I want to compute the sum of the elements in the integer Array using recursion. To do this I need to set a counter to the size of the array and use it to access each element in the array. Because indexes are zero-based I must identify an element in the array by taking 1 away from the value of counter, otherwise the program will throw a ArrayIndexOutOfBoundsException. This counter will be reduced by 1 every time the recursive method is called. When the counter reaches zero the recursion will stop because we have added up all of the integers in the array.

The recursion comes from "recursiveMethod" calling itself to add the next element in the array to the value of "sum" which it passes to itself each time it calls itself.

<strong>While-Loop</strong>
<script src="https://gist.github.com/final60/e713c3fefae59a44cce0.js"></script>
The above example is perhaps a little easier to follow. The computation only happens while the value of "run" is true. Again the "counter" is used to select the elements in the array and add them to the value of "sum". "counter" is then decremented once per iteration of the while loop. When "counter" has been decremented to 0 we set the value of "run" to false, which stops the while loop iterating.

<strong>For-Loop</strong>
<script src="https://gist.github.com/final60/de87ae472bea068f439c.js"></script>
We can shorten the code further using a for loop. Instead of creating a variable "counter" to use to access the indexes of the array. A for loop allows us to instantiate an iterator "i". Then, while the value of "i" is less than the length of the int array (5 [0-4]), we will get the value that's in the array at the index that is equal to "i". After adding the value to "sum" it will then increment "i". So we can access the value of the next index in the array. The iteration will continue until the boolean statement returns false, because "i" equals 5 which is not less than the length of the array, which is also 5. So it breaks out of the for loop.
