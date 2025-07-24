<img width="549" height="361" alt="image" src="https://github.com/user-attachments/assets/b5a418ed-ba0e-4204-ba63-c0c6697d038b" />### Task 3: ECB vs CBC Modes

#### ECB Encryption of BMP File

I encrypted a BMP image file using AES-256 in ECB mode with the command:  
openssl enc -aes-256-ecb -in pic_original.bmp -out ecb_encrypted.bmp

However, I initially forgot to include the password option -k, so I was prompted to manually enter the password bmp1.

After encryption, I obtained a new BMP file (ecb_pic_new.bmp). Upon inspecting this file, I noticed the image appeared highly pixelated and distorted. Large blocks of pixels were grouped together and encoded, which caused visible blocky patterns. Although some flashes of the original image were still visible, the overall picture was very distorted due to ECB mode's deterministic encryption of identical blocks.

CBC Encryption of BMP File
Next, I encrypted the same BMP file using AES-256 in CBC mode with the command:
openssl enc -aes-256-cbc -in pic_original.bmp -out cbc_encrypted.bmp -k bmp2


ECB and CBC Encryption Using My Own Image
I also tested both modes on my own BMP image pokhara.bmp.

For CBC encryption:
openssl enc -aes-256-cbc -in pokhara.bmp -out pokhara_cbc.bmp -k pokhara2

For ECB encryption:
openssl enc -aes-256-ecb -in pokhara.bmp -out pokhara_ecb.bmp -k pokhara1

When comparing both encrypted images, it was difficult to recognize the original picture in either. Both looked like static noise from an old television, with colors scrambled and heavily distorted. This demonstrated how CBC mode provides better diffusion than ECB mode, which tends to leak patterns.



![Original Image](https://media.discordapp.net/attachments/1174554222323318844/1398032607698092263/original_pokhara_bmp_image.png?ex=6883e2d3&is=68829153&hm=f2481e7bf5d755761279b5b346cb4f04bf6e424f1a8602267f5da4a2c4066420&=&format=webp&quality=lossless)

![EBC Encrypted Image](https://media.discordapp.net/attachments/1174554222323318844/1398032607433719961/EBC_pokhara_bmp_image.png?ex=6883e2d3&is=68829153&hm=d1c58d4625cb5ab950abc5774b49a8e388e769ac46ee6afc61da5fa623f15a7d&=&format=webp&quality=lossless)



Through this task, I learned firsthand how ECB mode's block-by-block encryption can expose patterns in data like images, whereas CBC mode adds randomness that helps obscure such patterns.
