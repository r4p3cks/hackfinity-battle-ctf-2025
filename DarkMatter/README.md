# Dark Matter
## Challenge

The Hackfinitiy high school has been hit by DarkInjector's ransomware, and some of its critical files have been encrypted. We need you and Void to use your crypto skills to find the RSA private key and restore the files. 
After some research and reverse engineering, you discover they have forgotten to remove some debugging from their code. The ransomware saves this data to the tmp directory.

Can you find the RSA private key?

>It is provided a VM with the necessary!

Starting the provided VM, it is prompted the following:

![image](https://github.com/user-attachments/assets/a56c4e85-7c63-460a-b85e-0fcd91f6b2b4)

## Solution

It is said that the tmp directory was used to save data from the debugging of the ransomware. This is what tmp contains:

![image](https://github.com/user-attachments/assets/5620bcc1-8798-4cfe-816c-e1890d5c543a)

At first glance, the files that look promising are __*encrypted_aes_key.bin*__ and __*public_key.txt*__. As said in the challenge statement, we need to find the RSA private key, so we can exclude the __*encrypted_aes_key.bin*__. Opening the __*public_key.txt*__
we can confirm that this key is a RSA public key because of the *n* and *e*.

![image](https://github.com/user-attachments/assets/3ad7de75-b760-4d47-9905-aeaa044a01c9)

>This *n* is called the modulus and is calculated by *p * q* (Two large prime numbers that are kept secret) operation.
> The public exponent, is typically a small prime number chosen to be relatively prime to (p−1)(q−1).
>What we want is *d* the private exponent, calculated as:

>![image](https://github.com/user-attachments/assets/6967d533-0ac2-44fa-91c3-35b434df5426)

So if we obtain *p* and *q* we can obtain *d* (private key). If *n* is a small number, it is computationally feasible to factorize it and obtain p and q, which it is. We used a online number facotrizer to be more fast in the process, rather than doing a python script.
We used this site (https://www.numberempire.com/numberfactorizer.php). 

The p and q are the following numbers:

![image](https://github.com/user-attachments/assets/dbb8fb1b-96c8-458f-8fb8-bdaa15e2584e)

Calculating *d* with what we have, we obtain __196442361873243903843228745541797845217__. This number is the private key. When used in thee ransomware note the files are decrypted with success.

![image](https://github.com/user-attachments/assets/4d19e0a4-738e-4abd-a6a2-fe29418791f3)

The key is in the __*student_grades.docx*__ document.

![image](https://github.com/user-attachments/assets/9fb2a528-d00b-4ac5-a709-a1453a61eeca)
