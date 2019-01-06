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
