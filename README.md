<h1> Creating/inspecting key pair, encrypting/decrypting and sign/verify using OpenSSL </h1>
<h2>Description</h2>
<p>In this lab, I will create and inspect key pairs, encrypt and decrypt, sign and verify using OpenSSL.</p>
<br />
<br />
<h2>Utilities Used</h2>
<ul>
    <li><b>Ubuntu</b> -Operating system used for the configuration</li>
    <li><b>OpenSSL</b> -A commercial-grade utility toolkit for Transport Layer Security (TLS) and Secure Sockets Layer (SSL) protocols</li>
</ul>
<br />
<h3>Task 1: Generate a private key</h3>
<p align="center">
<img src="https://i.imgur.com/NNgwj2a.png" height="80%" width="80%" alt="apt update"/>
</p>
<p align="left"> 
    
```
openssl genrsa -out private_key.pem 2048
```
    
This command creates a 2048-bit RSA key, called "private_key.pem", this is private key. The 'cat' command reads/ displays the file content.</p>

```
cat private_key.pem
```

<br />
<br />
<h3>Task 2: Generate a public key</h3>  
<br /> 
<p align="center">
<img src="https://i.imgur.com/nXwHSsZ.png" height="80%" width="80%" alt="mv files"/>
</p>

```
openssl rsa -in private_key.pem -outform PEM -pubout public_key.com
```
<p align="left"> The public key is generated from the private key to establish a pair for asymmetric encryption. The can display public key with the 'cat' command.

```
cat public_key.com
```

</p> 
<br /> 
<br />
<h3>Task 3: Encrypt the message</h3>
<p align="center">
<img src="https://i.imgur.com/C9j0yJ4.png" height="80%" width="80%" alt="show webpage"/>
</p>

```
echo 'This is a secret message, for authorized parties only' > secret.txt
```
<p align="left"> The above 'echo' command writes the message and saves it to the file 'secret.txt'. The second command encrypts the message using the public key. 

```
echo openssl rsautl -encrypt -pubin -inkey public_key.pem -in secret.txt -out secret.enc
```
<br />
Below you can see the output of the encrypted file using the simple text editor Nano.</p> 
<br />

```
nano secret.enc
```

<p align="center">
<img src="https://i.imgur.com/sNU0BoA.png" height="80%" width="80%" alt="config2"/>
</p>
<br />
<br />
<h3>Task 4: Decrypt Message</h3>
<p align="center">
<img src="https://i.imgur.com/HyugeKZ.png" height="80%" width="80%" alt="show webpage"/>
</p>

```
openssl rsautl -decrypt -inkey private_key.pem in secret.enc
```

<p align="left"> You can read the content of the message in plain text by decrypting the message with private key.</p> 
<br />
<br />
<h3>Task 5: Creating a hash digest</h3>
<p align="center">
<img src="https://i.imgur.com/4h3kHYu.png" height="80%" width="80%" alt="show webpage"/>
</p>

```
openssl dgst -sha256 -sign private_key.pem -out secret.txt.sha256 secret.txt
```
```
openssl dgst -sha256 -verify public_key.pem -signature secret.txt.sha256 secret.txt
```
<p align="left">First create a hash digest of the message, then use the public key and the hash digest to verify that the file hasn't been modified since it was hashed. This allows you to ensure that your message wasn't altered or forged. </p> 
<br />
<br />
</p>
<h3>Conclusion:</h3>
<p> In this lab, I used OpenSSL to create both a public and a private key using RSA encryption in Linux. I then used these keys to demonstrate file encryption and decryption. Finally, I used a **SHA-256** hash to verify the contents of the private key encryption and the public key encryption.</p> 
