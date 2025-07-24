 I explored secret-key encryption fundamentals by working hands-on with encryption algorithms, encryption modes, padding schemes, initialization vectors, as well as understanding the differences between public and private keys. I also studied common vulnerabilities and attacks on encryption systems to better understand potential pitfalls and strengthen my skills as a developer.

Task 1: Frequency Analysis of a Monolithic Substitution Cipher

I started by implementing a monolithic substitution cipher, where each letter in the plaintext is consistently replaced by another letter based on a fixed substitution key. My process involved several key steps:

Generating an Encryption Key: I created a substitution pattern to map plaintext letters to ciphertext letters.

![Encryption Key Generation](https://media.discordapp.net/attachments/645079991310090243/1398023295022006440/gen_ecrypt_key.png?ex=6883da27&is=688288a7&hm=cae463b49494cd3c11afb3e6d69e3614917bb1d5fed36a3162fe2f47d1fee65d&=&format=webp&quality=lossless)
)

Preprocessing the Text: I simplified the source text by converting all uppercase letters to lowercase and removing punctuation and numbers. 
This involved using Unix tr commands to clean and prepare the text data for encryption.

![Preprocessing Text](https://media.discordapp.net/attachments/1174554222323318844/1398025370304774347/preprocess_text.png?ex=6883dc16&is=68828a96&hm=469e2ab77053bd45a6e26b8260a41a60656bea75fea79dedd62bf440c8976ed4&=&format=webp&quality=lossless)

Encrypting the Plaintext: I applied the substitution cipher using tr to convert the cleaned plaintext into ciphertext based on my encryption key.

![Encrypting](https://media.discordapp.net/attachments/1174554222323318844/1398025953799704638/encrypting_text.png?ex=6883dca1&is=68828b21&hm=a8dce90d2480c9e13399fba11ed5a1ad0431bf25e45d29f82e0392378080446b&=&format=webp&quality=lossless)

Frequency Analysis and Decryption: I wrote and used a Python script (freq.py) to analyze the frequency distribution of letters and n-grams in the ciphertext. 
By comparing this distribution with known English language statistics, I gradually deciphered the ciphertext. 
This iterative substitution approach allowed me to crack the cipher step-by-step, demonstrating the power of frequency analysis against substitution ciphers.


