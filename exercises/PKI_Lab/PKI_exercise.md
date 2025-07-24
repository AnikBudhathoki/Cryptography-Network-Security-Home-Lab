

# PKI Lab

---

## Task 1: Create CA

In this task, our goal was to become a **Certificate Authority (CA)**. A CA is a trusted entity that issues digital certificates.

Using the `openssl.config` manual and the SEED lab manual, I generated a self-signed certificate. During the creation of the CA, I was prompted to enter details such as email, state, country code, etc.

After the CA was created, I used the following commands to output its details and observe elements like the public key, private key, modulus \(n\), exponents, etc.:


openssl x509 -in ca.crt -text -noout
openssl rsa -in ca.key -text -noout

![Openssl](https://media.discordapp.net/attachments/1174554222323318844/1398040454691553351/PKI_1.png?ex=6883ea22&is=688298a2&hm=6afc0f32dff1159f5ce6203cca847009b1199ac971ce39fd012b90f66ec84387&=&format=webp&quality=lossless)

![PEM Passphrase](https://media.discordapp.net/attachments/1174554222323318844/1398040454100160603/PKI_2.png?ex=6883ea22&is=688298a2&hm=8d4887c524110d71696e2ae42a15c3c418e99efffb94b85e1e84befb4674fff2&=&format=webp&quality=lossless)

Passphrase used: dees

What indicates this is a CA’s certificate?
The X509v3 constraints extension shows "CA: TRUE". This indicates the certificate is a valid CA certificate, establishing trust in digital communications.

![X509 Extension](https://media.discordapp.net/attachments/1174554222323318844/1398040453839851602/PKI_3.png?ex=6883ea22&is=688298a2&hm=4a2072158fea5d341a93bf124e1cfd4c55fe56e5edb390ed54f350b873f3e86c&=&format=webp&quality=lossless)

How do you know this is a self-signed certificate?
Because the issuer and the subject of the certificate are the same, it indicates the certificate is self-signed.

Where are the public/private exponent, modulus, etc.?
The public exponent (65537 or 0x10001) is found just above the X509v3 extensions.

The private exponent 
𝑑
d is accessible after entering the passphrase; the key length is 2048 bits.

![Private Exponent](https://media.discordapp.net/attachments/1174554222323318844/1398040453630263316/private_exponent.png?ex=6883ea22&is=688298a2&hm=667fcbb3488988c2d181cc808e9e3c35aa9af09f8d0262e99f6536afa0b4c0cc&=&format=webp&quality=lossless)

The modulus appears in both the public and private key sections.

![Modulus](https://media.discordapp.net/attachments/1174554222323318844/1398040453374414980/modulus.png?ex=6883ea22&is=688298a2&hm=071c4ab183923d0979f8e956e1fd0587afb0fc4bc60bf0fbf76cd9fce4a6ff72&=&format=webp&quality=lossless)

The two primes used to generate the RSA key are listed under private key details after entering the passphrase.

![Primes](https://media.discordapp.net/attachments/1174554222323318844/1398040453131272305/primes.png?ex=6883ea22&is=688298a2&hm=797ec6df1edde1845659edd8ee686752080667309fcf2f3321342a1dbcbdd92c&=&format=webp&quality=lossless)

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

![Certificate Request](https://media.discordapp.net/attachments/1174554222323318844/1398040452808315022/certificate_request.png?ex=6883ea22&is=688298a2&hm=90b0a32b6ba183f7891bb8060ac7ceed0db920272b9154f02d45efee5ed70d76&=&format=webp&quality=lossless)

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

![Certificate Generation](https://media.discordapp.net/attachments/1174554222323318844/1398040452342612099/certificate.png?ex=6883ea22&is=688298a2&hm=e71b9b6156de5792a4311f323a886116276ecab274ec1a5dbbc2158562296338&=&format=webp&quality=lossless)


# Summary of PKI Lab
Public Key Infrastructure (PKI) is used to verify ownership of public keys for secure communications.

A Certificate Authority (CA) issues digital certificates.

Other entities request public key certificates by creating Certificate Signing Requests (CSRs).

The CA signs these CSRs to produce valid certificates.

Using OpenSSL commands, you can view details such as primes, exponents, and modulus used in key generation.

This lab provided hands-on experience with creating and managing certificates, keys, and requests within PKI.

