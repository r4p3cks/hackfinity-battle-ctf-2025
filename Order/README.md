# Order
## Challenge

We intercepted one of Cipher's messages containing their next target. They encrypted their message using a repeating-key XOR cipher. However, they made a critical error—every message always starts with the header:

>ORDER:

Can you help void decrypt the message and determine their next target?
Here is the message we intercepted:

>1c1c01041963730f31352a3a386e24356b3d32392b6f6b0d323c22243f63731a0d0c302d3b2b1a292a3a38282c2f222d2a112d282c31202d2d2e24352e60

## Solution

The challenge explicitly indicates that the message used repeating-key XOR cipher and every message always start with the header __*ORDER:*__.

>A repeating-key XOR cipher is a type of encryption that uses a key that is repeated to match the length of the plaintext. Each character of the plaintext is XORed with the corresponding character of the key, making it a symmetric encryption method where the same process is used for both encryption and decryption.

If every message starts with header __*ORDER:*__ we can find the first characters in the intercepted message (Because of the XOR). Using a online encrypter and decrypter (https://md5decrypt.net/en/Xor/), we managed to find the following:

![image](https://github.com/user-attachments/assets/895c9154-0f8c-4a47-9bc5-668dd4e2aecc)

This indicates that __*SNEAKY*__ was the key used to encrypt the message. So repeating the process but this time with SNEAKY as the key we can decrypt the message.

![image](https://github.com/user-attachments/assets/a5d12cfd-fc92-4943-8970-61f5e3e5f74a)
