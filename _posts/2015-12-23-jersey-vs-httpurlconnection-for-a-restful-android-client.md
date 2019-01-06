Since Google officially <a href="http://developer.android.com/about/versions/marshmallow/android-6.0-changes.html">deprecated the HTTPClient</a> and related methods after Android API 22. I thought it would be interesting to compare their recommended alternative (HttpURLConnection) with my preferred RESTful client; <a href="https://jersey.java.net/">Jersey</a>.

The following example is an implementation of <a href="https://docs.oracle.com/javase/7/docs/api/java/net/HttpURLConnection.html">HttpURLConnection </a>to query a RESTful Webservice to return a String.
<script src="https://gist.github.com/final60/f5bddebc361286a1d9bd.js"></script>

The following is a small class implementation of the Jersey client framework, I decided to include the whole class for context.
<script src="https://gist.github.com/final60/50abdddaed608d153227.js"></script>

Here is how you would query for a String result within an Android AsyncTask:
<script src="https://gist.github.com/final60/d282bc3a45dd2641cef1.js"></script>

The biggest difference is the verbosity of HttpURLConnection. Here are a few other more obscure differences:

1. HttpURLConnection has a poorly designed API. It is very verbose, with a large library of methods and boilerplate required to achieve even the smallest transactional logic.

2. HttpURLConnection is very well documented. It is easy to find examples of whatever logic you are trying to implement.

3. Comparative performance is negligible. Especially when Jersey uses HttpUrlConnection as a fall-back API.

4. The Jersey client is Android-specific. It has been optimised specifically for RESTful requests. Whereas HttpUrlConnection is a general purpose, standalone API that can be used in any Java environment.

5. Jersey is merely a wrapper API. It has a number of fall-backs (HttpUrlConnection  being one of them). Its biggest strength is its API design, for extremely light-weight implementation requirements.
