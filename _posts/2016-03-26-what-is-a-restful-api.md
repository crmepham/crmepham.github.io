<strong>What is an API?</strong>
An Application Programming Interface (API) is simply a way of exposing the internal functionality of a service in a safe way. This enables clients to be able to make use of a systems functions without the system having to compromise on security or requiring a client to learn the details of a systems implementation. 

One example is the <a href="https://developer.yahoo.com/weather/" target="_blank">Yahoo Weather API</a>. If I am building an application and want to include some weather information within it, I can simply request this information in the form of a HTTP parameterized query like this:

<blockquote>https://query.yahooapis.com/v1/public/yql?q=select * from weather.forecast where woeid = 44418</blockquote>

The above URI will return an XML response containing all of the weather information for Greater London. I can then parse this XML in my web app or desktop application to display the information I want. I don't need to know how the underlying system gets the weather information, I simply need to know the correct URI and query to make and let Yahoo take care of the rest.

<strong>What is REST?</strong>
REST stands for <strong>RE</strong>presentational <strong>S</strong>tate <strong>T</strong>ransfer, and is the underlying software architectural style of the World Wide Web (WWW). The term itself was introduced in 2000 by <a href="https://en.wikipedia.org/wiki/Roy_Fielding" target="_blank">Roy Fielding</a> and was used to design the HyperText Transfer Protocol (HTTP) 1.1 and the Uniform Resource Identifier (URI) protocol. Although it may sound like a relatively new buzzword, the concept of REST has actually been around as long as the Web. 

The simple process of entering a URI in to a web browser and receiving a web page is REST in its fundamental form. Whats actually happening underneath is a GET request is sent containing the resource path, the protocol (HTTP 1.1 etc.) and the content type (text/html). A response is then returned (HTTP 1.1 200 OK) containing the resource that was requested in text/html format. If the user previously requested this resource then it is likely it was cached on one or more intermediary devices between the user and the server.

The amazing thing about the Web is that a client does not need to know the underlying structure of a remote system to be able to communicate with it. It simply needs to know the URI of a particular remote resource, the corresponding HTTP verb to use, and the content type it should expect to receive in the response from the server (typically web browsers take care of the last two for us).

<strong>What are HTTP verbs?</strong>
The most commonly used HTTP verbs (methods) are <strong>GET</strong> and <strong>POST</strong>, but there are a few lesser known verbs: OPTIONS, DELETE, PUT etc. 

<em>I should point out that web browsers typically only support the GET and POST verbs. Although JavaScripts XMLHTTPRequest Object accepts PUT and DELETE also. These verbs can be implemented through the use of JQuery's <strong>$.ajax()</strong> method.</em>

In a RESTful API these verbs will correspond to a specific action the client can take against a particular resource that an API is exposing and should directly correlate to a database operation in the following way:

<table style="width:100%;text-align:center;">
<tr><th>HTTP Verb</th><th>CRUD operation</th></tr>
<tr><td>POST</td><td>Create</td></tr>
<tr><td>GET</td><td>Read</td></tr>
<tr><td>PUT</td><td>Update</td></tr>
<tr><td>DELETE</td><td>Delete</td></tr>
</table>

<strong>What makes an API RESTful?</strong>
At its simplest, an API is RESTful when it adheres to the principles of REST. That is, it must not require the client to know anything about the structure of the API, the server must provide any necessary information the client needs to interact with its API. 

A good example of this is a HTML form. The server provides the form to the clients web browser which will contain the resource URI and the data it requires as form fields. The client doesn't know in advance what information it should provide in the form or the resource location to submit it too, this information was provided entirely by the server.

An API is also RESTful when it adheres to HTTP standard verbs and resources, as described above. The resource location will usually correlate to an entity, upon which actions can be performed through the use of HTTP verbs and specified parameters.

<strong>What about SOAP?</strong>
Simple Object Access Protocol (<a href="https://en.wikipedia.org/wiki/SOAP">SOAP</a>) is an alternative API framework that REST has all but replaced. SOAP is more restrictive than REST because it only permits the XML data format, it is not cache-able, and REST performs faster through its support of JSON which also makes it a better fit for browser-based clients where JSON parsing is easiest.

<strong>RESTful API example</strong>
In this example I will demonstrate how to implement a basic RESTful API to manipulate User data using the <a href="https://jersey.java.net/" target="_blank">Jersey JAX-RS</a> Java framework.

User request/response.
<table style="width:100%;">
<tr><th>URI</th><th>HTTP verb</th><th>Response</th></tr>
<tr><td>/user</td><td>GET</td><td>201</td></tr>
<tr><td>/user</td><td>POST</td><td>201 User successfully created.</td></tr>
<tr><td>/user/delete</td><td>POST</td><td>201 User successfully deleted.</td></tr>
<tr><td>/user/update</td><td>POST</td><td>201 User successfully updated.</td></tr>
</table>

<script src="https://gist.github.com/final60/f55b54f4df7c2c188714.js"></script>
In the above example you will notice that the <strong>getUser()</strong>and <strong>createUser()</strong> methods are mapped to the same URI, but respond to different HTTP verbs. Because we have to rely on the POST(not DELETE) verb to call our <strong>deleteUser()</strong> method we have to assign an extension to the URI to differentiate it to the createUser() mapping.

<strong>Summary</strong>
<ul>
<li>An API is a way of exposing the functionality of a system so it can be utilised by other programs.</li>
<li>An API is RESTful when it use URI's, HTTP verbs and response codes.</li>
<li>Web browsers only allow the GET and POST verbs to be used.</li>
<li>The same URI can be used to perform different operations on an entity, provided different verbs are used.</li>
