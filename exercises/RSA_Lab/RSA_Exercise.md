# RSA Encryption and Signature Lab Report
# Task 1: Deriving the Private Key
For this task, I was provided with the following values:

p=
textF7E75FDC469067FFDC4E847C51F452DF

q=
textE85CED54AF57E53E092113E62F436F4F

e=
text0D88C3

I modified the provided bn_sample.c code to compute the private and public keys. In RSA, the public key is represented as (n,e) and the private key as (n,d), where d is the modular inverse of e modulo 
phi(n). The computation of d was performed within the C program:
![Python Code1](https://media.discordapp.net/attachments/1174554222323318844/1398036476872233051/RSA_Code_1.png?ex=6883e66e&is=688294ee&hm=175c02e4094db80b8e906e8ebc66077aadde39c363374cbec9b6b76d182e3952&=&format=webp&quality=lossless)
![Python Code2](https://media.discordapp.net/attachments/1174554222323318844/1398036476603666532/RSA_Code_2.png?ex=6883e66e&is=688294ee&hm=4c3a3c7f395182ade02524c3aac3fe7b69ad18200c4c719aa64aed63166993a1&=&format=webp&quality=lossless)
![Python Code3](https://media.discordapp.net/attachments/1174554222323318844/1398036476322775201/RSA_Code_3.png?ex=6883e66e&is=688294ee&hm=a77915f9f5dbe7526ec7eecb7f8f731c80d70b17833663fb84280b01a9462ee6&=&format=webp&quality=lossless)


# Task 2: Encrypting Messages
Given our public key (e,n), the goal was to encrypt the message "A top secret!".

ASCII String to Hex String Conversion
First, the ASCII string "A top secret!" was converted into its hexadecimal representation.

Encryption Process
Using the public key (e,n) and the hexadecimal representation of the message, the message "A top secret!" was encrypted to produce a ciphertext. To verify the encryption, the corresponding private key (d,n) was used to decrypt the ciphertext back into its original hexadecimal ASCII string.

Console Results
The encryption and subsequent decryption yielded the following results:

Message Encrypted (Ciphertext): 6FB078DA550B2650832661E14F4F8D2CFAEF475A0DF3A75CACDC5DE5CFC5FADC

Original Hex String (after decryption): 4120746F702073656372657421

The decrypted hexadecimal string successfully matched the initial hexadecimal string used for encryption, confirming the correctness of the encryption and decryption process.

# Task 3: Decrypting a Message
Given that we have the same public and private keys from Task 2, I proceeded to decrypt the following ciphertext C:

C=
text8C0F971DF2F3672B28811407E2DABBE1DA0FEBBBDFC7DCB67396567EA1E2493F

Decryption Process
Running the decryption code with the provided ciphertext resulted in the following hexadecimal message:

Decrypted Hex Message: 50617373776F72642069732064656573

Converting Hex Message Back to ASCII String
To obtain the original message in readable ASCII, I used the bytes.fromhex() command in Python 3:
python3 -c 'print(bytes.fromhex("50617373776F72642069732064656573").decode("utf-8"))'

This conversion revealed the original message to be: "Password is dees".

# Task 4: Signing a Message
For this task, using the same public and private keys, I was required to sign the message "I owe you $2000.". Additionally, I had to observe the effect of a slight message modification on the resulting signature by changing the message to "I owe you $3000.".

Hex String Generation
First, both ASCII strings were converted into their hexadecimal representations using Python 3:
python3 -c 'print("I owe you $2000.".encode("utf-8").hex())'
Example result for "I owe you $2000.": 49206f776520796f752024323030302e

python3 -c 'print("I owe you $3000.".encode("utf-8").hex())'
Example result for "I owe you $3000.": 49206f776520796f752024333030302e

Encrypt Message using Public Key (Signing Process)
Using the previously derived public key (e,n), I "encrypted" (signed) both messages. In RSA digital signatures, the sender signs a message by encrypting its hash with their private key. However, for this lab, it appears we were instructed to observe the effect of "encrypting" the message content directly using the public key as part of the signature generation demonstration.

After running the signing code, the following message signatures were obtained:

Signature - Message 1 ("I owe you $2000."): 3A759CBF53901AC41373EEC603955A8E6AF8D3BCD5E9F6DD62C873CBB675051E

Signature - Message 2 ("I owe you $3000."): D06908047527906C724937169FA68CE0AC442FEB99D1880438D331A88F44B074

Even with only a slight change to the original message, a dramatic difference in the generated signatures was observed. This effectively demonstrated the sensitivity and strength of cryptographic signatures, where even minor alterations lead to entirely different outputs.

# Summary of RSA Encryption Lab
Through this lab, I gained a practical understanding of the RSA public-key cryptosystem. I learned that RSA relies on the generation of two large prime numbers (p and q) to construct a public key (n,e) and a private key (n,d). The process involves several key steps:

Calculating n: The product of the two large primes, n=p
timesq.

Calculating Euler's Totient 
phi(n): 
phi(n)=(p−1)(q−1).

Choosing a Public Exponent e: A number such that $1 \< e \< \\phi(n)$ and 
textgcd(e,
phi(n))=1.

Calculating the Private Exponent d: The modular multiplicative inverse of e modulo 
phi(n), meaning d
cdote
equiv1
pmodphi(n).

I learned that the core formulas for RSA encryption and decryption are:

Encryption: C=M^e
 
pmodn, where C is the ciphertext and M is the message.

Decryption: M=C^d
 
pmodn, where M is the original message and C is the ciphertext.

Furthermore, I became familiar with using the BIG NUM API, which greatly facilitates computations involving the large numbers inherent in RSA cryptography. This hands-on experience deepened my appreciation for the mathematical principles underlying secure communication.
