---
ID: 804
post_title: Public Key Infrastructure
author: crm
post_excerpt: ""
layout: post
permalink: >
  http://chrismepham.co.uk/blog/academia/public-key-infrastructure/
published: true
post_date: 2016-04-30 14:29:12
---
<strong>Why is PKI necessary?</strong>
The trouble with communication on the internet is that it is very easy for a third party to intercept the data being sent between two people. Even when using encryption it is relatively easy for a third party to pretend to be the person you wish to communicate with, send you their own public key which you use to encrypt your data, which will pair with their own private key for decrypting the data.
Wouldn't it be better if we could have strong encryption but also reliably know that the public key came from the person we want to communicate with? This is what PKI provides with its digitally signed certificates.
[caption id="attachment_813" align="aligncenter" width="1205"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2016/04/Untitled-1.png"><img src="http://chrismepham.co.uk/blog/wp-content/uploads/2016/04/Untitled-1.png" alt="PKI diagram" width="1205" height="472" class="size-full wp-image-813" /></a> PKI diagram[/caption]

<strong>What is PKI?</strong>
Public Key Infrastructure is a framework (or set of rules) for <strong>confidential</strong> and <strong>authenticated</strong> communication using the internet. When implementing PKI an organisation or individual must use Asymmetric cryptography (Public/Private key pair), but they can choose the encryption key length and the encryption algorithm type.

<strong>What is Asymmetric cryptography?</strong>
This is a type of encryption that requires two keys to decipher an encrypted message. They are a public/private key pair. If someone encrypts a message with the public key the message can <strong>ONLY</strong> be deciphered with the private key, and vice versa. This is great except that we need to be sure the person we want to communicate with is the person that sent the public key. It is very possible for a third party to intercept a request for a public key, and send you their public key instead, meaning the third party can decipher the messages you encrypt, that is why we need to authenticate the recipient using PKI.

<strong>What is a digitial certificate?</strong>
A digitial certificate is the thing that authenticates the person/company you want to communicate with as the owner of the key pair. So when your web browser requests a secure Secure Sockets Layer (SSL) connection with a web server, the server responds with a digital certificate containing identifiable information, its validity period, the public key, and the Certificate Authorities (CA) details. Normally of the x.509 certificate standard.

<strong>What is a Certificate Authority?</strong>
A CA is a trusted third party organisation that will confirm the identity of an individual or organisation. All CA's will, at the very least, automatically check to ensure that the details provided correspond to a registered domain owners details. More expensive options will include actual people checking various details, and even requesting further identification. Generally, a digital certificate is requested by submitting a Certificate Signing Request (CSR). If sticking to the x.509 standard the CSR will contain your identifiable information and your public key (from a previously generated public/private key pair). The CA will then validate the information in the CSR and send you back a digitally signed certificate using the CA's private key.
[caption id="attachment_810" align="aligncenter" width="320"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2016/04/cert.png"><img src="http://chrismepham.co.uk/blog/wp-content/uploads/2016/04/cert.png" alt="x.509 certificate" width="320" height="241" class="size-full wp-image-810" /></a> x.509 certificate[/caption]

<strong>What about self-signed certificates?</strong>
It is possible to generate your own self-signed certificate. These are not trusted by web browsers because your identity has not been validated by a trusted CA. Self-signed certificates will still work and a secure connection to your server is possible. Self-signed certificates are useful on intranets or personal websites that you know are safe.

Read <a href="http://chrismepham.co.uk/blog/guide/how-to-convert-a-web-application-from-http-to-https/">How to convert a web app from HTTP to HTTPS</a> for information on configuring a web server for secure asymmetric communication.

Read <a href="http://chrismepham.co.uk/blog/uncategorized/cryptography-explained/">Cryptography explained!</a> to learn more about Symmetric and Asymmetric key encryption and key exchange.