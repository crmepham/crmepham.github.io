This was a neat little problem I came across today during my OCA studies and thought it might be worth sharing a solution.

The problem:



<blockquote>Write a function that computes the list of the first 100 Fibonacci numbers. By definition, the first two numbers in the Fibonacci sequence are 0 and 1, and each subsequent number is the sum of the previous two. As an example, here are the first 10 Fibonnaci numbers: 0, 1, 1, 2, 3, 5, 8, 13, 21, and 34.Write a function that computes the list of the first 100 Fibonacci numbers.</blockquote>

Firstly, here is the code:
<script src="https://gist.github.com/final60/790e31d4c058adcaa654.js"></script>

Outputs:


<blockquote>0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987, 1597, 2584, 4181, 6765, 10946, 17711, 28657, 46368, 75025, 121393, 196418, 317811, 514229, 832040, 1346269, 2178309, 3524578, 5702887, 9227465, 14930352, 24157817, 39088169, 63245986, 102334155, 165580141, 267914296, 433494437, 701408733, 1134903170, 1836311903, 2971215073, 4807526976, 7778742049, 12586269025, 20365011074, 32951280099, 53316291173, 86267571272, 139583862445, 225851433717, 365435296162, 591286729879, 956722026041, 1548008755920, 2504730781961, 4052739537881, 6557470319842, 10610209857723, 17167680177565, 27777890035288, 44945570212853, 72723460248141, 117669030460994, 190392490709135, 308061521170129, 498454011879264, 806515533049393, 1304969544928657, 2111485077978050, 3416454622906707, 5527939700884757, 8944394323791464, 14472334024676221, 23416728348467685, 37889062373143906, 61305790721611591, 99194853094755497, 160500643816367088, 259695496911122585, 420196140727489673, 679891637638612258, 1100087778366101931, 1779979416004714189, 2880067194370816120, 4660046610375530309, 7540113804746346429, 12200160415121876738, 19740274219868223167, 31940434634990099905, 51680708854858323072, 83621143489848422977, 135301852344706746049, 218922995834555169026</blockquote>



..and to explain a couple of things!

First, it is not possible to use primitive datatypes to store the values of the Fibonacci sequence because at some point, right around the 90th Fibonacci number, the value is greater than the maximum permissible value, that the largest non-decimal primitive datatype allows. 

<strong>long</strong> allows the maximum value of <strong>92233720368547758070</strong>. So to store extremely large values I had to use <strong>BigInteger</strong> which is an immutable object (similar to String), that allows arbitrary-precision integer values.

Next, as the problem explains: the Fibonacci consists of the sum of the previous two numbers. So I need to temporarily store the previous two numbers (num1 and num2) plus the sum of these two numbers (sum). After each iteration the values of num2 and sum are shifted left so num1 now holds the value of num2 and num2 holds the value of sum in the previous iteration.

For example:

<strong>Iteration 1</strong>

num1 = 0;
num2 = 1;
sum = 1; // 0 + 1 = 1

<strong>Iteration 2</strong>

num1 = 1; // the value of num2
num2 = 1; // the value of sum
sum = 2; // 1 + 1 = 2

So after the second iteration the list would contain the following Fibonacci numbers: <strong>0, 1, 1, 2</strong>.

Finally, it is simply a matter of adding the sum to the list of Fibonacci numbers at the end of each iteration, and output them as normal.
