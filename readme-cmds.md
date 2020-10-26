https://dzone.com/articles/extracting-a-private-key-from-java-keystore-jks

https://security.stackexchange.com/questions/3779/how-can-i-export-my-private-key-from-a-java-keytool-keystore

Create a simple keystore
keytool -genkeypair -alias notebook -keyalg RSA -dname "CN=naga,OU=dev,O=bft,L=mt,C=USA" -keystore identity.jks -keypass keypassword -storepass storepassword

Convert JKS to the PKCS12 format:
keytool -importkeystore -srckeystore identity.jks -srcstorepass storepassword -srckeypass keypassword -srcalias notebook -destalias notebook -destkeystore identity.p12 -deststoretype PKCS12 -deststorepass password -destkeypass password

keytool -importkeystore -srckeystore <source keystore>.jks -srcstorepass <source keystore password> -srckeypass <source key password> -srcalias <source alias> -destalias <destination alias> -destkeystore <destination keystore>.p12 -deststoretype PKCS12 -deststorepass <destination keystore password> -destkeypass <destination key password>

Open JKS
keytool -list -keystore identity.jks -v

Exporting the private key from the PKCS12 format keystore:
openssl pkcs12 -in identity.p12 -nodes -nocerts -out private_key.pem

-nodes - No DES - No Encryption

Exporting the Public Key
openssl pkcs12 -in identity.p12 -nokeys -out cert.pem

Exporting Keys to RSA Format
openssl rsa -in -cert.pem  -out rsacert.pem

openssl rsa -in private_key.pem  -out rsaprivateKey.pem
