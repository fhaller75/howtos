SSL certs & config
==================
##### Retrieve a root CA from a server url:
---
```bash
echo -n | openssl s_client -showcerts -servername myserverurl.com -connect myserverurl.com:443 2>/dev/null  \
  | sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p') 
```
-> can be saved into a .pem and added to the CA-certificates directory/file of the client unix host

##### Check cert expiration date inside a pfx:
---
```bash
openssl pkcs12 -in keystore.pfx -passin pass:"${passwd}" -nokeys | openssl x509 -noout -enddate
```
