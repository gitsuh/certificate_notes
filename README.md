# certificate_notes
I am too dumb to remember.

1. Generate a certificate signing request
  
3. Request a PFX (personal informationexchange) certificate from the thing
 
4. Extract the key pair with openssl binary
    `#openssl pkcs12 -in sample.pfx -nocerts -nodes -out sample.key`

5. Get the Private Key from the key-pair
    `#openssl rsa -in sample.key -out sample_private.key`

6. Get the Public Key from key pair
    `#openssl rsa -in sample.key -pubout -out sample_public.key`

7. Modify the private key to pkcs8 format
    `#openssl pkcs8 -topk8 -inform PEM -in sample_private.key -outform PEM -nocrypt`
    Copy the output and save it as sample_private_pkcs8.key

> public key:  sample_public.key

> private key: sample_private_pkcs8.key

---
x509
PEM
DER
P7B
PKCS7
PFX
PKCS8

---

***PKI File Types***

*.cer – typically a PEM formatted Base64, ASCII certificate
*.crt – typically a PEM formatted Base64, ASCII certificate
*.der – binary form of a certificate
*.pem – typically a PEM formatted Base64, ASCII certificate
PKCS#7 – also known as P7B – a Base64, ASCII file that contains certificates and Intermediate CA certificates, does not include private keys
PKCS#8 – a Base64, ASCII file that contains a private key
PKCS#12 – also known as PFX – a binary format for storing the server certificate, intermediate certificate and private key in one file. Typically used on MS Windows to import \ export certificates and private keys.


---
***Convert x509 to PEM***
`#openssl x509 -in certificatename.cer -outform PEM -out certificatename.pem`



***Convert PEM to DER***
`openssl x509 -outform der -in certificatename.pem -out certificatename.der`



***Convert DER to PEM***
`openssl x509 -inform der -in certificatename.der -out certificatename.pem`



***Convert PEM to P7B***

Note: The PKCS#7 or P7B format is stored in Base64 ASCII format and has a file extension of .p7b or .p7c.
A P7B file only contains certificates and chain certificates (Intermediate CAs), not the private key. The most common platforms that support P7B files are Microsoft Windows and Java Tomcat.
`openssl crl2pkcs7 -nocrl -certfile certificatename.pem -out certificatename.p7b -certfile CACert.cer`



***Convert PKCS7 to PEM***
`openssl pkcs7 -print_certs -in certificatename.p7b -out certificatename.pem`



***Convert pfx to PEM***

Note: The PKCS#12 or PFX format is a binary format for storing the server certificate, intermediate certificates, and the private key in one encryptable file. PFX files usually have extensions such as .pfx and .p12. PFX files are typically used on Windows machines to import and export certificates and private keys.
`openssl pkcs12 -in certificatename.pfx -out certificatename.pem`



***Convert PFX to PKCS#8***
Note: This requires 2 commands

STEP 1: Convert PFX to PEM
`openssl pkcs12 -in certificatename.pfx -nocerts -nodes -out certificatename.pem`



STEP 2: Convert PEM to PKCS8
`openSSL pkcs8 -in certificatename.pem -topk8 -nocrypt -out certificatename.pk8`



***Convert P7B to PFX***
Note: This requires 2 commands

STEP 1: Convert P7B to CER
`openssl pkcs7 -print_certs -in certificatename.p7b -out certificatename.cer`


STEP 2: Convert CER and Private Key to PFX
`openssl pkcs12 -export -in certificatename.cer -inkey privateKey.key -out certificatename.pfx -certfile  cacert.cer`

 ---

 

Inspect a Certificate Signing Request

`openssl req -text -noout -verify -in my-csr.csr`

Inspect a Certificate

`openssl x509 -in certificate.crt -text -noout`

Note: Removing -in will allow you to past the Base 64 text from the console. 
