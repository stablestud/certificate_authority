Note: `.pem` can contain `.crt` and `.key` pieces. To generate `.pem` simply add the
needed files together and name it `.pem`

STEPS TO CREATE A AUTHORITY SIGNED TLS CERTIFICATE USED FOR SECURE INTERNAL
NETWORING

1. Create key file    
`openssl genrsa -out **domain**.key 4096`

2. Create Certificate Signing Request (csr)    
`openssl req -new -sha256 -out **domain**.csr -key **domain**.key`

3. Create Extension file to add multiple domains/IP addresses (SANs),     
if not needed just insert the domain into CN (Common Name) instead    

Note: if creating * Wildcard certificates, set it in SANs and not in the CN as Chromium dislikes that.

`**domain**.ext`:

```
authorityKeyIdentifier=keyid,issuer
basicConstraints=CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names

[alt_names]
IP.1=127.0.0.1
IP.2=0000:0000:0000:0000:0000:0000:0000:0001
IP.3=10.4.2.1
DNS.4=localhost
DNS.5=**domain**.local.lab
DNS.6=**domain**.local
DNS.7=**domain**
```



4. Create Signed Certificate    
`openssl x509 -req -in **domain**.csr  -CA ca.crt  -CAkey ca.key -CAcreateserial -out **domain**.crt -days 1825 -sha256 -extfile **domain**.ext`

5. Install onto Server    
Copy `**domain**.key` and `**domain**.crt` onto the server.
Or if both combined `**domain**.pem`, see above.
