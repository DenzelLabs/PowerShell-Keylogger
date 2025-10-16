# PowerShell Keylogger

<br><br>

## Investigation

<p>What is the proxy port used by the script?</p>
<strong>Answer: 9050 </strong>
<p>
I opened C:\Users\LetsDefend\Desktop\ChallengeFile\sample.7z with the password infected in Notepad++, searched for "port" with Ctrl+F, and found the proxy port.
</p>
<img width="724" height="455" alt="image" src="https://github.com/user-attachments/assets/2401081e-f5f6-4361-9d49-9acebafc50d4" />

<br><br>

<p>What function-method is used for starting keylogging?</p>
<strong>Answer: start-keylogger</strong>
<p>I searched the script in Notepad++ for "keylogger" instead of reading the entire file and on line 94 found the function Start-Keylogger, indicating the keylogging function.</p>
<img width="721" height="354" alt="image" src="https://github.com/user-attachments/assets/dd0072db-3b94-478a-a9f6-61a9ee4844c0" />

<br><br>

<p>What is the name of the file used by the script to store the keylog data?</p>
<strong>Answer: keylog.txt</strong>
<p>I examined the Start-Keylogger function in Notepad++ and found on line 134 an AppendAllText call that writes keystrokes to keylog.txt.</p>
<img width="803" height="360" alt="image" src="https://github.com/user-attachments/assets/59467eb7-fc5c-4bf6-8084-40fd7e20cefc" />

<br><br>

<p>What command is used by the script to achieve persistence?</p>
<strong>Answer: persist</strong>
<p>I searched the script and found on line 245 the condition $command -eq "persist" with a comment noting persistence logic, but no active persistence mechanism was implemented.</p>
<img width="717" height="395" alt="image" src="https://github.com/user-attachments/assets/b54eaacc-d748-4c86-99d1-cc2c59855eba" />

<br><br>





