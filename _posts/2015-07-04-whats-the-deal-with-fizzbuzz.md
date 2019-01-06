<blockquote>Write a program that prints the numbers from 1 to 100. But for multiples of three print “Fizz” instead of the number and for the multiples of five print “Buzz”. For numbers which are multiples of both three and five print “FizzBuzz”</blockquote>

Okay, first I'll refactor the question into a list of constraints:

1. Print out numbers 1 to 100.
2. Multiples of 3 should print "Fizz" instead of the number.
3. Multiples of 5 should print "buzz" instead of the number.
4. Multiples of 3 and 5 should print "FizzBuzz" instead of the number.


Next, Ill write some psuedo-code to give me an idea of the program structure:

<strong>// loop 100 times

// if multiple of 3 print Fizz

// else if multiple of 5 print Buzz

// else if multiple of 3 and 5 print FizzBuzz

// else print the number</strong>

Here's the code:
<script src="https://gist.github.com/final60/90a418468b4e09d6e827.js"></script>

The program works as it should, but the code can be improved in a few different ways. Firstly we are doing a check on i to skip the number 0, because the first constraint wants us to print only numbers between 1 and 100. Also the code looks verbose. Perhaps we could shorten the number of if/else statements somehow. So let's do some refactoring.

<script src="https://gist.github.com/final60/00acc8f233a1acfb6f49.js"></script>
In the above code you can see that I have reduced the lines of code considerably. Firstly I initialized the variable i to 1. This means we no longer need to check if the value is 0. Next I have used a ternary operator (<a href="http://chrismepham.co.uk/blog/certification/ocajp-revision-embedded-ternary-operators-with-pre-and-post-incremented-variables/">more on this from a previous blog post</a>) to check whether the current value of i is divisible by any of the required combinations of numbers and assigning the correct String value. Finally we have a single output call to display the variable value.

So by refactoring I have:
1. removed the check on 0
2. removed all continue calls
3. reduced 4 output calls to just 1
4. reduced 5 lines of boolean operator checks to just 1.
