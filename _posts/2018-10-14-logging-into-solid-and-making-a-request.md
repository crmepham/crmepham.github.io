---
classes: wide
tags: [solid]
---
I should preface this post by mentioning that SOLID appears to still be in the early stages of development, and so this post may become out of date quickly. Currently the initial login step actually requires the username and password be sent in clear text.

If you don't know about SOLID please head over to <a href="https://solid.inrupt.com">https://solid.inrupt.com</a> to learn all about it.
<h2>Logging into SOLID</h2>
If you haven't logged in previously then you will need to login manually by supplying your username and password. The response to a successful login request will contain the <strong>connect-id</strong> cookie which will be used in future requests and login requests:

```java
POST /login/password HTTP/1.1
Host: solid.community
Content-Type: application/x-www-form-urlencoded
username=crmepham2password=testing
```

The response will contain the header <strong>set-cookie</strong> with a value similar to:

```java
connect.sid=s%3AowbxP8Nztfz3zzVoeK7pPRNT7sdiuUrU.szxTieghJaJO2WZeZjR348gxyNQgLVp%2BZoUu3FsNLYs; 
Domain=.solid.community; Path=/; Expires=Mon, 15 Oct 2018 11:15:54 GMT; HttpOnly; Secure
````

<h2>Sending an authenticated request</h2>
With the cookie now set you can make authenticated requests. In this example we will update my cards first name property:

```java
PATCH /profile/card HTTP/1.1
Host: crmepham2.solid.community
Content-Type: application/sparql-update
DELETE DATA { &lt;https://crmepham2.solid.community/profile/card#me&gt; &lt;http://www.w3.org/2006/vcard/ns#fn&gt; "Chris" .
 } 
 ; INSERT DATA { &lt;https://crmepham2.solid.community/profile/card#me&gt; &lt;http://www.w3.org/2006/vcard/ns#fn&gt; "Chris Mepham" .
 }
```

Which returns the response "Patch applied successfully." And can be seen in the SOLID UI.

<img class="aligncenter size-full wp-image-1070" src="http://chrismepham.co.uk/blog/wp-content/uploads/2018/10/Screen-Shot-2018-10-14-at-12.55.49.png" alt="" width="620" height="483" />

&nbsp;

&nbsp;

Read more about the body of the request <a href="https://solid.inrupt.com/docs/expressing-ld-with-turtle">here</a>.
