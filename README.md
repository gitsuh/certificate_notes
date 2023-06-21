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
