---
ID: 218
post_title: 'OCAJP: embedded ternary operators with pre and post incremented variables'
author: crm
post_excerpt: ""
layout: post
permalink: >
  http://chrismepham.co.uk/blog/certification/ocajp-revision-embedded-ternary-operators-with-pre-and-post-incremented-variables/
published: true
post_date: 2015-07-01 17:57:31
---
I came across an amusing question whilst studying operators and constructs for an upcoming certification exam I am taking and thought I'd share and explain the process of evaluating the assignment of the output variable. It is one of those frustratingly time consuming questions that once broken down are relatively easy to answer.

<strong>The question: (courtesy of Enthuware)</strong>


<blockquote>What will the following code print?</blockquote>


<script src="https://gist.github.com/final60/1078c2deaebb9db37249.js"></script>


At first glance it may look like a confusing fusion of poorly formatted code. But when we start to break it all down and simplify it, it will become a lot clearer, so lets do that.

Before we start, though, I'll explain what pre and post increment/decrement operators are. 

Put simply, they are shorthand operators that increase or decrease the value by 1.

<script src="https://gist.github.com/final60/f71d6dc696190c859571.js"></script>

If you see a++ used during an evaluation, the current value of the variable will be used in the evaluation before incrementing the value by 1 after. If you see ++a used in an evaluation it means the value will first be incremented by 1 and then evaluated. The same goes for the - - (decrement operator).

First lets work out the values of the variables after each declaration.

On line 1 x is given the value of 1.
On line 2 y is given the value of 2.
On line 3 z is given the value of x first and then x is incremented by 1. So now x has the value of 2.
On line 4 y is pre decremented, so now has the value of 1. a is then given the value of y, which is 1.
On line 5 b is given the value of 1 first and then z is decremented to 0.
On line 6 z is first pre incremented by 1 so it has the value of 1. Next the value of z (1) is added to b, so b now has the value of 2.

So after all of the declarations have taken place the values are as follows:

<strong>x=2 y=1 z=1 a=1 b=2</strong>

That's the first part of the question out of the way!

Next, let's work out the ternary expression.

First a quick explanation. In it's simplest form, a ternary operator (also known as a conditional operator) is a shorthand way of writing an "if/else/then" expression. Compare the following ternary and if/else expressions:
<script src="https://gist.github.com/final60/4d23fb694d78282ca64a.js"></script>

You'll notice that the ternary operator uses a lot less syntax and can achieve the same result using only one line.

Firstly, the operator will evaluate the boolean operation within the parenthesis. In the above example it is evaluating if <strong>a</strong> is less than <strong>b</strong>. If the result is true then the expression following the ? will be executed, otherwise the expression after the colon will be executed. Both expressions must return a data type matching that of the variable being assigned, in this case an integer.

The next thing you need to know is that ternary operators can execute any code in either the true or false expressions. So the code can include another ternary operator. This is what is happening in the OCA question - the main ternary operator executes another ternary operator for both the true and false code sections.

Let's separate the three ternary operators:

<strong>1. (x>a) ? : ;
2. (y>b) ? y : b;
3. (x>z) ? x : z;</strong>

Let's simplify the separated ternary operators further by replacing the variables with their values:

<strong>1. (2>1) ? : ;
2. (1>2) ? 1 : 2;
3. (2>1) ? 2 : 1;</strong>

We can use parenthesis to separate the different sections of the ternary operator to make it more readable:
<script src="https://gist.github.com/final60/27267b917ef1d3017f6b.js"></script>

The first ternary operator wants to know if 2 is greater than 1. If it is then execute the left nested ternary operator, if it isn't, execute the right nested ternary operator.

Now, can you work out what value is assigned to <strong>answ</strong>?