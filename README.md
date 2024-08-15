# Creating an Isolated Network in VirtualBox
(Very old project, just updating the writeup)
For some context, I hope to run a vulnerable web server in a virtual machine to be able to practice my ethical hacking. I don't want this web server to be open to the internet as there are serious security concerns with that, so I want to create an isolated sandbox environment to use.

### Creating an Isolated Network
First, I created a DHCP server for an Isolated Network in VirtualBox by typing `vboxmanage dhcpserver add --network=NAME --server-ip=10.22.1.1 --lower-ip=10.22.1.110 --upper-ip=10.22.1.130 --netmask=255.255.255.0 --enable` in Windows Command Prompt (as my normal machine is a Windows device). I simply choose TESTNET1 as the name of the network, for practice.

![image](https://github.com/rat-v/Explorations/assets/169432484/9eb35a14-8f5f-45b9-b671-b05b19c74965)

Then, I configured the VirtualBox Network settings for each virtual machine by going to Settings --> Network --> Adapter set to Internal Network --> TESTNET1

### SIDE NOTE - FILE INTEGRITY VERIFICATION
I wanted to practice verifying files with hashes so I ran `get-filehash -algorithm MD5 mrRobot.ova` in Windows Powershell. I noticed that this command did not work on the regular command prompt. I didn't know that there were any differences before today, so it was good to learn. After a little bit of research about the specific differences, it seems that powershell also has scripting capabilities and is very important in ethical hacking making it a powerful tool.

![image](https://github.com/rat-v/Explorations/assets/169432484/291fd965-05c1-4627-8b66-550b873f6ab5)

The MD5 Hash was identical to the one listed on vulnhub.com, so it was verified.

Running the Kali VM with the `ip address` command verifies that the VM is running on the isolated network set up earlier.

![image](https://github.com/rat-v/Explorations/assets/169432484/595c155a-a452-4c50-b401-ee8e59fceb64)

Pinging the machine from my home network confirms that it is indeed isolated, as there is no response.

![image](https://github.com/rat-v/Explorations/assets/169432484/1a4d1b11-49bc-4956-9cee-e2e826290c4c)

I plan on working on the Web Server later. First, I want to learn more and gain additional experience with fundamental tools such as Nmap, Wireshark, and Metasploit. 

This was an enjoyable introductory project, gaining experience in mainly working with VirtualBox and using a terminal.

### Some more random notes about Windows Powershell
When experimenting around more with powershell, I realized that I couldn't simply put in the command `vboxmanage (PARAMETERS)` like I would in command prompt, but instead had to first inform the terminal that I would like to run the program as it wasn't recognizing "vboxmanage" or "vboxmanage.exe" as a proper term. I learned how to do this with the `&` command acting as a "call operator", and designating the full directory path, in order to actually execute the program with the proper parameters. I first tried to utilize `start-process` but I couldn't figure out the proper way to set up the command, and found that `&` worked much easier.

![image](https://github.com/rat-v/Explorations/assets/169432484/c1d1fe65-2735-48c7-be2a-ce92efa036fd)

![image](https://github.com/rat-v/Explorations/assets/169432484/c388d1a0-eacb-40c0-a937-fb8c2949bac5)

