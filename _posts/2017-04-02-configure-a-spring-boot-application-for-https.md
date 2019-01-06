<h2>Generate a self-signed certificate using Keytool</h2>
Use the following command to generate a self-signed RSA certificate that can be used during development to test your application under HTTPS.
<pre class="EnlighterJSRAW" data-enlighter-language="null">keytool -genkey -alias tomcat -storetype PKCS12 -keyalg RSA -keysize 2048 -keystore keystore.p12 -validity 7300</pre>
<em>For production, you will want to create a certificate via a Certificate Authority. Read <a href="http://chrismepham.co.uk/blog/guide/how-to-convert-a-web-application-from-http-to-https/">How to convert a web application from HTTP to HTTPS</a> for more information on how to create a production-ready HTTPS certificate.</em>
<h2>Modify your application.properties file</h2>
To configure Spring Boot for HTTPS, all you need to do is add the following properties to the application.properties file in <strong>/src/main/resources/application.properties</strong>.
<pre class="EnlighterJSRAW" data-enlighter-language="null">server.port: 443
server.ssl.key-store: keystore.p12
server.ssl.key-store-password: password
server.ssl.keyStoreType: PKCS12
server.ssl.keyAlias: tomcat</pre>
Now, when you run your application make sure that the "keystore.p12" file that you generated is in the same directory as your application, or you must specify the path to it in your application.properties. Note: it must be in the same directory as your deployed application (jar), <strong>not</strong> in the same directory as the application.properties file.

You will now be able to access your application from <strong>https://localhost</strong>.
<h2>Redirect HTTP to HTTPS (optional)</h2>
It may be necessary to redirect an existing HTTP request to use the new HTTPS protocol, especially if you are changing an existing application. Read <a href="http://chrismepham.co.uk/blog/guide/how-to-convert-a-web-application-from-http-to-https/">How to convert a web application from HTTP to HTTPS</a> for more information on how to do this.
