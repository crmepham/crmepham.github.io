---
ID: 998
post_title: Create OkHttp3 Response for testing
author: crm
post_excerpt: ""
layout: post
permalink: >
  http://chrismepham.co.uk/blog/programming/create-okhttp3-response-for-testing/
published: true
post_date: 2018-06-20 09:27:19
---
Use a variation of the following code to create a Response to test with:
<pre class="EnlighterJSRAW" data-enlighter-language="java">private Response createResponse()
    {
        HttpUrl mHttpUrl = new HttpUrl.Builder()
                .scheme("https")
                .host("example.com")
                .build();
        Request mRequest = new Request.Builder()
                .url(mHttpUrl)
                .build();

        Response.Builder builder = new Response.Builder()
                .request(mRequest)
                .protocol(Protocol.HTTP_1_1)
                .message("message")
                .code(302);

        return builder.build();
    }</pre>
&nbsp;