### Task 2: Different Ciphers and Modes

In this task, I worked with several symmetric encryption algorithms and modes using OpenSSL to encrypt and decrypt a sample text file (`article.txt`).

- **AES-256-CBC**  
  I encrypted the original `article.txt` file using the command:  
  ```bash
  openssl enc -aes-256-cbc -in article.txt -out encrypted_aes.bin -k password1 -iv 00112233445566778899aabbccddeeff

This produced an encrypted binary file. I then decrypted it using:
openssl enc -aes-256-cbc -d -in encrypted_aes.bin -out decrypted_aes.txt -k password1 -iv 00112233445566778899aabbccddeeff

Finally, I compared the decrypted file with the original to verify the process.

![AES-256](https://media.discordapp.net/attachments/1174554222323318844/1398029186550993098/AES_256_CBC.png?ex=6883dfa4&is=68828e24&hm=3a3d10169befd7d755d81d1acce722e0e705a6bac760cb54a818694e2ef71194&=&format=webp&quality=lossless)

DES-EDE3-CBC (Triple DES)
I encrypted with:
openssl enc -des-ede3-cbc -e -in article.txt -out encrypted_des-ede3-cbc.bin -k password2 -iv 00112233445566778899aabbccddeeff

And decrypted with:
openssl enc -des-ede3-cbc -d -in encrypted_des-ede3-cbc.bin -out decrypted_des.txt -k password2 -iv 00112233445566778899aabbccddeeff

Then, I verified that the decrypted output matched the original plaintext.

![DES](https://media.discordapp.net/attachments/1174554222323318844/1398029186089881710/DES-EDE3-CBC.png?ex=6883dfa4&is=68828e24&hm=d2afaa6a22d17cfe81f7494f06cdf32b76c8ad71e727cdad0cc59723052e07b2&=&format=webp&quality=lossless)

AES-128-CBC
Encryption command: openssl enc -aes-128-cbc -e -in article.txt -out encrypted_aes128.bin -k password3 -iv 00112233445566778899aabbccddeeff

Decryption command: openssl enc -aes-128-cbc -d -in encrypted_aes128.bin -out decrypted_aes128.txt -k password3 -iv 00112233445566778899aabbccddeeff

I validated the decrypted file against the original to ensure correctness.

![AES-128](https://media.discordapp.net/attachments/1174554222323318844/1398029185808601099/AES-128.png?ex=6883dfa4&is=68828e24&hm=3d4c7c04bbea3e92a108782987cf02d2c3c339f465757965e520ebf088f9376b&=&format=webp&quality=lossless)

![Cipher Check](https://media.discordapp.net/attachments/1174554222323318844/1398029664500580434/Cipher_check.png?ex=6883e016&is=68828e96&hm=0a6982a5c2a41715f168306f0b087fea52b27cdfa30f625c7bd2881a1ab982e2&=&format=webp&quality=lossless)

Through this exercise, I gained practical experience 
applying different symmetric encryption algorithms and cipher modes with OpenSSL and understanding their workflows.

