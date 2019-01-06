<h2>Introduction</h2>
I will describe how to convert a web application using the HTTP protocol to HTTPS. I will explain what the protocols and relevant technologies are and how they are implemented, and the difference between a self-signed SSL certificate and one signed by a Certificate Authority(CA).

<h2>Pre-requisits:</h2>
Apache2
Ubuntu 14.04

<h2>What is HTTP/HTTPS?</h2>
HyperText Transfer Protocol(HTTP) is the protocol used by the World Wide Web(WWW) to define how a web browser and a web server must format and transmit data packets so that they can understand each other. For example; when you visit a website, you put a URL into the address bar which is a HTTP GET request <em>( < protocol > :// < server.ip.address > /path/to/resource )</em> to the server specified in the address string. The request will take a specific form of bits in packets that will be sent to the server, the server will then be able to assemble the packets and understand the request it received from the browser because both parties used the same HTTP protocol.

HyperText Transfer Protocol Secure(HTTPS) is the secure version of the HTTP protocol and focuses on securing the packets that are sent between the browser and the server by encrypting the data within them. This prevents "man in the middle" attacks by preventing hackers from reading the information within the packets once they have been intercepted. HTTPS will use either Secure Socket Layer(SSL) or Transport Layer Security(TLS) for the encryption, and both work on the premise of private and public keys. The public key is used by the browser to encrypt the data it sends to the web server. The private key is kept secure on the web server, and is used to decrypt the secure packet to process the request inside it.

When a web browser first initiates a HTTPS handshake (by putting the URL in the address bar) the server will respond with a SSL certificate containing the public key that the browser will use for the rest of the data exchange between the browser and the web server. The certificate will have been generated and stored on the web server and can be either "Self-signed" or signed by a "Certificate Authority". Both methods will generate a valid SSL certificate which will enable a HTTPS connection between a browser and the web server. The difference comes in that a certificate signed by a certificate authority will activate the green padlock in the web browser, and the webpage you are requesting will not be automatically blocked. This is because the certificate authority is a trusted third party that has confirmed the identity of the server owner matches that of the domain owner.

By default all web browsers use port 80 for HTTP requests and port 443 for HTTPS requests. Unless you explicitly append a specific port number to the end of the URL.

<h2>Generate a self-signed certificate using openssl</h2>


<blockquote>
openssl req -newkey rsa:2048 -nodes -keyout <em>< domain-name ></em>.key -x509 -days 365 -out <em>< domain-name ></em>.crt
</blockquote>


The above command can be run to generate a SSL private key/certificate pair. The domain-name is the domain name or website name that you want to secure. This is not so important for a self-signed certificate, but some CA's only generate a certificate that is valid for a single domain and will only work for that domain. Self-signed certificates are good for personal websites or intranet sites - where you aren't concerned that it is being blocked for the general public.

<h2>Generate a certificate signing request (CSR)</h2>


<blockquote>
openssl req -newkey rsa:2048 -nodes -keyout <em>< domain-name ></em>.key -out <em>< domain-name ></em>.csr
</blockquote>


The above command will generate a private key and a CSR. The text within the .csr file will be copied and pasted in to the relevant form when applying for a CA certificate. Depending on the type of certificate you want (more expensive ones do more validity checks) the CA will usually send you your certificate within 10 minutes.

<h2>Configure Apache with your SSL certificate(s)</h2>

<blockquote>
< VirtualHost *:80 >
        ServerName example.com
        ServerAlias www.example.com
        Redirect permanent / https://example.com
< /VirtualHost >

< VirtualHost _default_:443 >
        ServerName socket.chat

        DocumentRoot /var/www/example.com

        SSLEngine On
        SSLCertificateFile /etc/apache2/ssl/48748798787545ab.crt
        SSLCertificateKeyFile /etc/apache2/ssl/socket.chat.key
        SSLCertificateChainFile /etc/apache2/ssl/gd_intermediate.crt
        SSLCertificateChainFile /etc/apache2/ssl/gd_bundle.crt

# self-sign key/certificate below
#       SSLCertificateFile /etc/apache2/ssl/example.crt
#       SSLCertificateKeyFile /etc/apache2/ssl/example.key

< /VirtualHost >
</blockquote>

<h3>Converting the HTTP request to HTTPS</h3>
You will notice that the virtual host is listening on port 80 for a domain request of example.com or www.example.com. It then re-directs this request to the same domain, except now it is using the HTTPS protocol.

<h3>Configuring SSL</h3>
The same virtual host is also listening on port 443 for a domain request of example.com. SSL is enabled and the relevant certificates and private key are entered with their respective directive. You will have one private certificate, one private personal certificate and one or more certificates depending on the CA. These are chain certificates and are used for the security of the CA. So for the <strong>SSLCertificateChainFile </strong>directive you may have to put in one or more intermediate certificates.

Commented out at the bottom are the self-signed certificate and key.
The above configuration is used with a virtual host, but if you are not using virtual hosts the same config can be placed inside either httpd.conf or ssl.conf depending on your version of Apache.
