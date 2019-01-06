[caption id="attachment_317" align="aligncenter" width="1941"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2015/07/IMG_20150716_1610531.jpg"><img src="http://chrismepham.co.uk/blog/wp-content/uploads/2015/07/IMG_20150716_1610531.jpg" alt="chat program" width="1941" height="1193" class="size-full wp-image-317" /></a> chat program[/caption]

I have been tinkering with a relatively new HTML5 technology called WebSockets, which allows for super fast text and blob communication. 

In this post I'll explain a bit about the technology and why it was introduced and give a simple example of how to setup a server to listen in on a port number and send and receive communication.

Traditionally, web-based communication was very slow and always initiated by the client by loading a webpage, usually by clicking on a link. Content was delivered from the server to the clients web browser along with the website markup data. Then AJAX came along and improved on this by making a webpage feel more dynamic by performing Asynchronous calls to a server, these calls could be triggered by a JavaScript event, like clicking on a button on the webpage. A webpage could update it's content without the user needing to reload the page. This was a great step forward, but communication was still being initiated from the client side, usually with periodic polling, using some interval-based JavaScript function to give the illusion that a server is initiating communication. So communication could never be considered instant or bi-directional.

The other problem with traditional techniques like AJAX is that they produce a lot of overhead, because they have to use the HTTP protocol that relies on request/response cycling and incorporates a lot of unnecessary data in it's header, this introduces latency. Also with AJAX interval polling for new data from a server, there is a lot of requests that are being sent to the server which result in no data coming back.

Instead of polling a server, couldn't there be a way of just letting the server send the client new data when it is received? and couldn't it do this using a far smaller packet size protocol?

The HTML5 WebSockets protocol was introduced to solve the above issues. It is the first protocol of it's kind to allow true bi-directional communication between a client and a server, where both sides can initiate communication. After the initial HTTP handshake, the protocol used for the open connection is upgraded to the WebSocket protocol which has significantly less overhead. With the socket connection remaining open, both the client and the server are free to send WebSocket frames to one another whenever they like.

<strong>WebSocket methods</strong>
WebSocket uses just 4 eventHandler methods which are:

<strong>onopen</strong> - This method indicates that a successful connection has been made between the server and the client.
<strong>onclose</strong> - This is the method that is called when the connection is closed from either side.
<strong>onmessage</strong> - This is the method that is called when a message is received at either end of the connection.
<strong>onerror</strong> - This is the method that is called when there is an error in connecting to the server.

Here is a simple example of a client side WebSocket implementation:
<script src="https://gist.github.com/final60/acaba7329d34736f9f47.js"></script>
In the above example you can see that we have instantiated a new WebSocket object which attempts to connected to the server. Then we have implemented the 4 main methods. In this example, when the connection to the server is successfully accomplished, the onopen method will be called and prints "connection established" on the webpage. Also when we click on the submit button, the send() method is called which in turn calls the send method on the WebSocket object, containing a text message we want to send to the server.


Now for the server side implementation:
<script src="https://gist.github.com/final60/a5c681db160eeed58230.js"></script>
When on the server side of the WebSocket communication, the onopen method indicates that a new client has successfully connected to the server, and the onclose method indicates that a client has closed a connection with the server. The onmessage method is called when a message is received from a client, and in the example above, the message that is received is sent to all other connected clients.

<strong>In summary:</strong>
The WebSockets protocol specification was introduced in HTML5 to solve the problem of truly bi-directional communication between a client and a server. Previously techniques such as AJAX merely gave the illusion of dynamic communication and still had the large overhead of full HTTP frames being transmitted between a client and server. WebSockets provides a light weight, low latency protocol that a HTTP packet upgrades to after an initial handshake. For instant communication that can be initiated at either end, transmitting data live and not database driven.

Try out a Live demo <a href="http://crmepham.no-ip.biz:8080/WebSocketChat/">here</a>.
