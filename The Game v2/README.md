# The Game v2
## Challenge

Cipher’s trail led us to a new version of Tetris hiding encrypted information. As we cracked its code, a chilling message emerged: "The game is never over."

>It is provided a zip with a executable inside it

## Solution

This challenge was harder than the v1 version of this. This time using *strings* was not possible to obtain the flag or any useful info.
To gather more information we executed the game in a secure environment. We compared it to the version 1 and it was different. The most different thing was that the v2 has a string saying the following:

![image](https://github.com/user-attachments/assets/ccb56200-5a24-4935-8a63-13c523197a5f)

This must be a hint to obtain the flag. It was time for some game hacking. We used cheat engine to be able to modified values in the process running the game. The first thing that we thought was to modified the score to a number higher to 999999.
Unsuccessfully. 

![image](https://github.com/user-attachments/assets/abe3378a-bca0-4c35-a20d-14ebe13f20e0)

Five results, when searching for the score value. We tried to change every value of the five addresses. Nothing...

If changing the score does nothing, what about changing the minimum score. 

![image](https://github.com/user-attachments/assets/bccd03aa-b892-4e5b-8b72-cb15222589ca)

This looked promising, so we changed the value in the first address to 100. So if we scored 100 points maybe the program would show something. And it did.

![image](https://github.com/user-attachments/assets/bfd2fb51-07ea-4c12-be22-2176225d18da)
