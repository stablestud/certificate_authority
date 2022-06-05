1. Generate ca key file - keep it private!    
`openssl genrsa -sha256 -out ca.key 4096`

2. Create ca certificate and sign it. Note .pem or .crt does not matter    
`openssl req -x509 -new -nodes -key ca.key -sha256 -days 1825 -out ca.crt`
