# OpenSSL commands and java equivalence

This repository propose a list of openssl commands with its java code equivalence.

## Certificates

### Create CA
openssl req -x509 -newkey rsa:2048 -sha256 -days 365 -nodes -passout pass:"1234" -keyout root.key -out root.crt -subj "/CN=%CNRoot%" 

### Generate rsa
openssl genrsa -aes256 -passout pass:"1234" -out rsa.key 2048

### Autosign
openssl req -x509 -new  -key rsa.key -passin pass:"1234" -sha256 -days 365 -out root.pem -nodes -subj "/CN=%CNRoot%"
openssl x509 -in root.pem -noout -text 

### Sign CSR
openssl x509 -req -in %CN%.csr -days 365 -CA root.crt -CAkey root.key  -CAcreateserial -out %CN%.crt -extensions "usr_cert"
openssl x509 -in %CN%.crt -noout -text

### Verify chain untrusted: sef-signed 
openssl verify -verbose  -CAfile root.crt  %CN%.crt

### Extract chain  
openssl s_client -servername example.com -connect example.com:443
