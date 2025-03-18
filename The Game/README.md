# The Game
## Challenge

Cipher has gone dark, but intel reveals he’s hiding critical secrets inside Tetris, a popular video game. Hack it and uncover the encrypted data buried in its code.

>It is provided a zip with a executable inside it

## Solution

This challenge was very easy. We extracted the zip and isolated the executable. With the program *strings* we found the flag.

> $ strings Tetrix.exe | grep THM
