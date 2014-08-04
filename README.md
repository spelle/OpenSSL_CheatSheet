OpenSSL_CheatSheet
==================

Examples

Note: in these examples the '\' means the example should be all on one line.

Display the contents of a certificate:
$ openssl x509 -in cert.pem -noout -text

Display the certificate serial number:
$ openssl x509 -in cert.pem -noout -serial

Display the certificate subject name:
$ openssl x509 -in cert.pem -noout -subject

Display the certificate subject name in RFC2253 form:
$ openssl x509 -in cert.pem -noout -subject -nameopt RFC2253

Display the certificate subject name in oneline form on a terminal supporting UTF8:
$ openssl x509 -in cert.pem -noout -subject -nameopt oneline,-esc_msb

Display the certificate MD5 fingerprint:
$ openssl x509 -in cert.pem -noout -fingerprint

Display the certificate SHA1 fingerprint:
$ openssl x509 -sha1 -in cert.pem -noout -fingerprint

Convert a certificate from PEM to DER format:
$ openssl x509 -in cert.pem -inform PEM -out cert.der -outform DER

Convert a certificate to a certificate request:
$ openssl x509 -x509toreq -in cert.pem -out req.pem -signkey key.pem

Convert a certificate request into a self signed certificate using extensions for a CA:
$ openssl x509 -req -in careq.pem -extfile openssl.cnf -extensions v3_ca \
-signkey key.pem -out cacert.pem

Sign a certificate request using the CA certificate above and add user certificate extensions:
$ openssl x509 -req -in req.pem -extfile openssl.cnf -extensions v3_usr \
-CA cacert.pem -CAkey key.pem -CAcreateserial

Set a certificate to be trusted for SSL client use and change set its alias to "Steve's Class 1 CA "
$ openssl x509 -in cert.pem -addtrust clientAuth \
-setalias "Steve's Class 1 CA" -out trust.pem

###
# extract p12
##       

###############################################################
# CERTIFICATE (lui donner une passphrase, à toi de choisir) ###
###############################################################
openssl pkcs12 -clcerts -nokeys -in mycert.p12 -out usercert.pem
chmod 0600 usercert.pem
###############################################################
# PRIVATE KEY (lui donner une passphrase, à toi de choisir) ###
###############################################################
openssl pkcs12 -nocerts -in mycert.p12 -out userkey.pem
chmod 0400 userkey.pem

If you want to extract  from a pfx file and write it to PEM file
$ openssl pkcs12 -in publicAndprivate.p12 -nocerts -out privateKey.pem

If you want to extract the CERTIFICATE file (the signed public key) from the pfx file
$ openssl pkcs12 -in publicAndprivate.p12 -clcerts -nokeys -out publicCert.pem

To remove the password from the private key file.
$ openssl rsa -in privateKey.pem -out private.pem
