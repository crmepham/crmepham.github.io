This post describes a simple example for implementing sockets. Sockets allow two programs to communicate across a network. It does this by allocated a unique port number to the program. This enables multiple networked programs to run from a single operating system, and allows fully-duplex data transmission. This is opposed to the web-based "Client/Server" paradigm, which traditionally only allowed data communication to be instantiated by the client (Web browser) in the form of a HTTP request. The server (software on a networked computer) could then respond to the request. 

Only recently bi-directional communication within the web browser was made possible thanks to the <a href="http://chrismepham.co.uk/blog/programming/how-to-create-a-simple-super-fast-web-based-chat-program-using-java-websockets/">WebSocket </a>protocol.

The following is a simple example of how to network a piece of software, and how to receive and send data. In this example the server will wait for an instruction to perform a particular task, and then respond when the task is complete.
<script src="https://gist.github.com/final60/aa24894dd237e820496b.js"></script>
In the above code you will notice that a client has established a connection and sent a request "calculate_primes:2000000", this will be interpreted on the other node as "find all the prime numbers in 200000".

<script src="https://gist.github.com/final60/0e6addb6adc5d2c1cf7f.js"></script>
The server receives the request, performs the task and responds to the request when the task is complete.
