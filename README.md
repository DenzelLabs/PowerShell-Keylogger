# PowerShell Keylogger

## Objective
<p>
You are a malware analyst investigating a suspected PowerShell malware sample. The malware is designed to establish a connection with a remote server, execute various commands, and potentially exfiltrate data. Your goal is to analyze the malware’s functionality and determine its capabilities.

File Location: C:\Users\LetsDefend\Desktop\ChallengeFile\sample.7z

File Password: infected
</p>

<br><br>

## Skills Learned
<ul>
  <li>Script analysis using Notepad++.</li>
  <li>Identified keylogging and persistence functions.</li>
  <li>Detected data exfiltration and storage methods.</li>
  <li>Recognized DLL imports and regex filtering.</li>
  <li>Understood connection retry logic.</li>
</ul>


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

<p>What is the command used by the script to upload data?</p>
<strong>Answer: upload:</strong>
<p>I found on line 215 a reference to an upload: command, indicating the script includes an upload/exfiltration mechanism.</p>
<img width="853" height="367" alt="image" src="https://github.com/user-attachments/assets/46c082de-288d-42a2-b37f-13d3b9adbf65" />

<br><br>

<p>What is the regex used by the script to filter IP addresses?</p>
<strong>Answer: ^(127\.|169\.254\.)</strong>
<p>inspected the script in Notepad++, looked at Get-NetIPAddress on line 86, and found the -nomatch regex ^(127\.|169\.254\.) which excludes loopback and link-local IPs.</p>
<img width="1041" height="285" alt="image" src="https://github.com/user-attachments/assets/2120b07c-3762-4dfe-a9eb-32c7ab78cd74" />

<br><br>

<p>What is the DLL imported by the script to call keylogging APIs?</p>
<strong>Answer: user32.dll</strong>
<p>I inspected the Start-Keylogger function and found DllImport references to user32.dll on lines 99, 101, 103, and 105, which provide access to GetAsyncKeyState (line 119) for monitoring keystrokes.</p>
<img width="1059" height="373" alt="image" src="https://github.com/user-attachments/assets/b307b164-85eb-4834-bb73-9eee64193b68" />

<br><br>

<p>How many seconds does the script wait before re-establishing a connection?</p>
<strong>Answer: 60</strong>
<p>I searched the script for Seconds/Start-Sleep and found on line 276 a Start-Sleep 60 in the Establish-Connection error path, which pauses 60 seconds before retrying to reconnect to the C2 server.</p>
<img width="920" height="279" alt="image" src="https://github.com/user-attachments/assets/42a21aa6-723f-4b81-b45a-40be89076947" />





