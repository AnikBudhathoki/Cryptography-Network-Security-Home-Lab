# Cryptography-Network-Security-Home-Lab

This repository contains my implementations of various cryptography/network labs that I wanted to complete to demonstrate and practice hands-on experience with:

- Secret key encryption (AES, DES, ECB/CBC modes)  
- Public key cryptography (RSA)  
- Public Key Infrastructure (PKI)  
- Hash collisions (MD5)  

---
Below are the follwing sub-labs and activites I completed. Each Exercise consist of a description of what I did and what I learned. Specifics of the steps I completed can be found in exercises folder. 
## 1) Frequency Analysis

### 📜 Description  
A monolithic substitution cipher is a simple encryption method where each letter in the plaintext is replaced by another letter from a fixed substitution pattern. While easy to implement, it’s vulnerable to frequency analysis due to predictable letter patterns.

### What I Learned  
- Frequency analysis is a powerful technique for breaking substitution ciphers.  
- Even basic encryption schemes reveal structure if the input isn’t randomized.  
- Tools like `tr` and `freq.py` allow rapid iteration and substitution testing.

---

## 2) Different Ciphers and Modes

In this task, I experimented with different symmetric encryption algorithms and modes using the OpenSSL command-line utility. Specifically, I used:

- AES-256-CBC  
- Triple DES (DES-EDE3-CBC)  
- AES-128-CBC  

Each cipher was tested by encrypting a sample text file (`article.txt`) and then decrypting it back to verify correctness. I used a consistent Initialization Vector (IV) across all examples for clarity and comparison purposes:  
`00112233445566778899aabbccddeeff`

### What I Learned  
- **Key Size Differences:** Larger key sizes like AES-256 offer stronger security but may introduce slight overhead compared to AES-128.  
- **Triple DES:** Still supported but generally considered outdated due to smaller effective key size and slower performance.  
- **IV Usage:** Using the same IV helped in testing, but in real-world applications the IV should be randomly generated and never reused with the same key to avoid vulnerabilities.  
- **OpenSSL Usage:** The `openssl enc` command is a quick and effective way to test symmetric encryption on files. The `-k` option simplifies key entry, though in practice, key derivation should be handled more securely.

---

## 3) ECB vs CBC Modes (Image Encryption)

In this task, I explored the differences between ECB and CBC encryption modes by applying them to `.bmp` image files using AES-256. The results clearly demonstrated why ECB is considered insecure for image data.

### What I Learned  
- This lab deepened my understanding of secret key cryptography.  
- I saw firsthand how monolithic substitution ciphers are vulnerable when character frequency isn’t masked.  
- Learned to use OpenSSL `enc` for AES and DES file encryption.  
- Explored ECB vs CBC modes and understood why ECB is insecure for visual or repetitive data.  
- Encrypting image files provided a powerful way to visualize how encryption transforms data.  
- I now understand how poor cipher choices can lead to vulnerabilities even when encryption is used.  

This lab gave me foundational cryptography knowledge and a practical sense of how theory meets real-world application.

---

## 4) RSA Encryption and Signature Lab

This lab gave me hands-on experience with RSA, including key generation, message encryption/decryption, and working with hex and ASCII transformations.

### What I Learned  
- How to derive RSA keys from two primes and an exponent using modular arithmetic.  
- How to convert between ASCII and hex for encryption preparation.  
- How to perform RSA encryption and decryption using custom C code.  
- How to verify results by comparing original and decrypted values.  

It was satisfying to see how encryption hides plaintext and decryption reveals it again. This lab made RSA much more approachable and deepened my interest in cryptography.

---
## 5) PKI Lab: Certificate Authority and Certificate Management

In this lab, I explored Public Key Infrastructure (PKI) by acting as a Certificate Authority (CA), generating Certificate Signing Requests (CSRs), and issuing certificates.

### What I Learned  
- A Certificate Authority (CA) is a trusted entity that issues digital certificates verifying ownership of public keys.  
- A Certificate Signing Request (CSR) is how entities request certificates from a CA.  
- Learned to create a self-signed CA certificate, generate CSRs, and sign requests to issue trusted certificates.  
- Explored certificate structure, viewing key details like primes, exponents, and modulus.  
- Reinforced the importance of extensions such as X509v3 constraints and subject alternative names in establishing trust.

## References

- Wikimedia Foundation. (2024, June 17). N-gram. Wikipedia. https://en.wikipedia.org/wiki/N-gram#  
- Awati, R., & Loshin, P. (2021, September 1). What is a Certificate Authority (CA)?. Security. https://www.techtarget.com/searchsecurity/definition/certificate-authority  
- Wikimedia Foundation. (2024b, August 30). MD5. Wikipedia. https://en.wikipedia.org/wiki/MD5  
- GeeksforGeeks. (2024, September 11). RSA algorithm in cryptography. https://www.geeksforgeeks.org/rsa-algorithm-cryptography/  
- RSA calculator. (n.d.). https://www.cs.drexel.edu/~popyack/IntroCS/HW/RSAWorksheet.html
