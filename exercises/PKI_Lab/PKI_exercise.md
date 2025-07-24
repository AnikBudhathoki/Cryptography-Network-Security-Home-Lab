# PKI Lab

---

## Task 1: Create CA

In this task, our goal was to become a **Certificate Authority (CA)**. A CA is a trusted entity that issues digital certificates.

Using the `openssl.config` manual and the SEED lab manual, I generated a self-signed certificate. During the creation of the CA, I was prompted to enter details such as email, state, country code, etc.

After the CA was created, I used the following commands to output its details and observe elements like the public key, private key, modulus \(n\), exponents, etc.:


openssl x509 -in ca.crt -text -noout
openssl rsa -in ca.key -text -noout

Passphrase used: dees

What indicates this is a CA’s certificate?
The X509v3 constraints extension shows "CA: TRUE". This indicates the certificate is a valid CA certificate, establishing trust in digital communications.

How do you know this is a self-signed certificate?
Because the issuer and the subject of the certificate are the same, it indicates the certificate is self-signed.

Where are the public/private exponent, modulus, etc.?
The public exponent (65537 or 0x10001) is found just above the X509v3 extensions.

The private exponent 
𝑑
d is accessible after entering the passphrase; the key length is 2048 bits.

The modulus appears in both the public and private key sections.

The two primes used to generate the RSA key are listed under private key details after entering the passphrase.

# Task 2: Certificate Request (CSR)
We simulated a company requesting a public key certificate from our CA.

The following command was used to generate a CSR for the domain www.XfinityTwo.com:
openssl req -newkey rsa:2048 -sha256 \
  -keyout server.key -out server.csr \
  -subj "/CN=www.XfinityTwo.com/O=XfinityTwo Inc./C=US" \
  -passout pass:dees \
  -addext "subjectAltName = DNS:www.XfinityTwo.com, DNS:www.XfinityTwoA.com, DNS:www.XfinityTwoB.com"
To view the decoded contents of the CSR:
openssl req -in server.csr -text -noout
To view the private key details, including primes and private exponents:
openssl rsa -in server.key -text -noout

# Task 3: Certificate Generation
We simulated signing the CSR files using the CA.

By default, the openssl ca command does not copy extension fields. We edited the openssl.conf file to uncomment the line that allows extension copying.

Then, the following command was run to generate the X.509 certificate from the CSR:
openssl ca -config openssl.conf -policy policy_anything -md sha256 -days 3650 \
  -in server.csr -out server.crt -batch -cert ca.crt -keyfile ca.key


We entered the passphrase when prompted, and the certificate was generated.

To verify that the alternative names are present in the certificate:
openssl x509 -in server.crt -text -noout

Under X509v3 extensions, I verified that the alternative names were listed, including:

XfinityTwo.com

XfinityTwoA.com

XfinityTwoB.com

# Summary of PKI Lab
Public Key Infrastructure (PKI) is used to verify ownership of public keys for secure communications.

A Certificate Authority (CA) issues digital certificates.

Other entities request public key certificates by creating Certificate Signing Requests (CSRs).

The CA signs these CSRs to produce valid certificates.

Using OpenSSL commands, you can view details such as primes, exponents, and modulus used in key generation.

This lab provided hands-on experience with creating and managing certificates, keys, and requests within PKI.

