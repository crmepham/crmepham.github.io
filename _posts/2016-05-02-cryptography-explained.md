---
classes: wide
tags: [cryptography]
---
Cryptography (encryption) is the process of protecting information by transforming it into an unreadable format, called cipher text. This will usually be done using cryptographic key systems to encrypt and decrypt cipher text.

These systems include the Diffie-Hellman key exchange, as well as Advanced Encryption Standard (AES) and the Data Encryption Standard (DES) for Symmetric encryption, and <strong>RSA</strong> for Asymmetric encryption.

<strong>Diffie-Hellman</strong>
DH key exchange in itself is not a data encryption algorithm but a public-key technology used to agree on a single secret key via a public network to be used in a symmetric encryption system. DH uses two different numbers to derive a single secret key. DH is asymmetric because each communicant has a different key to start with and they end up with the same secret key which is used to encrypt and decrypt a message. But it is important to remember that Diffie-Helman is only used to create and share a single symmetric key that both communicants can use to encrypt and decrypt messages to one another. The process it uses to do this is asymmetric.
<strong>
Simplified DH example:</strong>
<em>Alice and Bob decide, publicly on a number (15). Alice then chooses a secret number(2) that no one knows and takes the public number and puts it to the power of her secret number (15^2=225) and sends the result (225) to Bob. 

Bob then does the same exact thing that Alice does, but with his secret number(3). So he takes the public number(15) and puts it to the power of his secret number (15^3=3375) and then sends the result (3375) to Alice. 

At this point in the game Alice has Bob's result 3375 and Bob has Alice's result of 225. Now the fun part. Alice takes' Bob's result (3375) and puts it to the power of her secret number(3375^2=11390625). Then Bob takes Alice's result and puts it to the power of his secret number (225^3=11390625). Magically(or shall we say "mathically") they come up with the same number!</em>

<strong>RSA</strong>
The acronym stands for <strong>Rivest</strong>, <strong>Shamir </strong>and <strong>Adelman</strong>, the inventors of the public-key encryption agorithm. RSA is the most widely used asymmetric public-key encryption algorithm. RSA implements a Public/Private key pair system whereby a message encrypted with the public key can only be decrypted with the private key, and vice versa. 

The RSA encryption algorithm relies on the fact that there is no efficient way to factor very large prime numbers. Take the following example: <strong>? * ? = 6,700,283</strong>. It would take trial and error, computer resources and a lot of time to compute the factors of a very large prime number. An encryption key greater than 2048 bits for example, would take all of the worlds combined computing resources many hundreds of years to work out what two prime numbers were multiplied together, i.e find out the encryption key pair. This <strong>time </strong>factor is important. The RSA algorithm is breakable, but the time it would take would be so long that the information that was encrypted would no longer have any relevance.


<strong>Symmetric(private-key) vs Asymmetric(public-key) encryption</strong>
- Symmetric encryption uses the same key to encrypt and decrypt data, whereas asymmetric encryption uses a key-pair (public and private), where the data encrypted with a public key can ONLY be decrypted by the private key and vice versa.
- Symmetric encryption is generally faster than Asymmetric encryption and consumes less resources, which is an important consideration when needing to encrypt large amounts of data.
- Because symmetric encryption relies on the key always being kept secure, provided it is kept secure, then it can't be "brute-forced" the same way asymmetric encryption can be. Because in asymmetric encryption anyone can use the public key in the key-pair as a basis for working out the private key.
- The fundamental trade-off between choosing Symmetric or Asymmetric encryption will be one of Performance(Symmetric) vs. Security(Asymmetric).
