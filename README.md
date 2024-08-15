# Setting Up VirtualBox and a Vulnerable Web Server for Penetration Testing Practice  

## Setting Up a Virtual Machine and Vulnerable Web Server
A Kali Linux OS and a "Mr. Robot" Vulnerable Web Server (VWS) from VulnHub was installed and set up on VirtualBox.

### Creating an Isolated Network
Because I am running a vulnerable web server, I would like to be completely secure just in case any bad actors may detect this web server I am running and use vulnerabilities from it in order to compromise my home network.

First, I created a DHCP server for an Isolated Network in VirtualBox by typing `vboxmanage dhcpserver add --network=NAME --server-ip=10.22.1.1 --lower-ip=10.22.1.110 --upper-ip=10.22.1.130 --netmask=255.255.255.0 --enable` in Windows Command Prompt (as my normal machine is a Windows device). 

![image](https://github.com/rat-v/Explorations/assets/169432484/9eb35a14-8f5f-45b9-b671-b05b19c74965)

Then, I configured the VirtualBox Network settings for each machine ((Settings --> Network --> Adapter set to Internal Network --> Name set to TESTNET1)

### SIDE NOTE - FILE INTEGRITY VERIFICATION
Running the VWS resulted in a Windows Defender notification, so the file was verified by running `get-filehash -algorithm MD5 mrRobot.ova` in Windows Powershell. I noticed that this command did not work on the regular command prompt, so I learned there was some differences in functionality between cmd prompt and powershell. After a little bit of research about the specific differences, it seems that there is nothing that cmd prompt can do that powershell can't, while powershell also has additional functionalities. 

![image](https://github.com/rat-v/Explorations/assets/169432484/291fd965-05c1-4627-8b66-550b873f6ab5)

The MD5 Hash was identical to the one listed on vulnhub.com, so it was deemed safe and that it was just flagged due to the nature of the program. 

Running the VM with the `ip address` command verifies that the VM is running on the isolated network set up earlier.

![image](https://github.com/rat-v/Explorations/assets/169432484/595c155a-a452-4c50-b401-ee8e59fceb64)

Pinging the machine from my home network confirms that it is indeed isolated, as there is no response.

![image](https://github.com/rat-v/Explorations/assets/169432484/1a4d1b11-49bc-4956-9cee-e2e826290c4c)

I plan on working on the Web Server later. First, I want to learn more and gain additional experience with fundamental tools such as Nmap, Wireshark, and Metasploit. 

This was an enjoyable introductory project, gaining experience in mainly working with VirtualBox and navigating directories in a terminal. Important things I learned here was learning how to set up a closed network in VirtualBox, superficial cryptography experience with file integrity verification, and the difference between cmd prompt and powershell.

### Rambling about Windows Powershell
When experimenting around more with powershell, I realized that I couldn't simply put in the command `vboxmanage (PARAMETERS)` like I would in command prompt, but instead had to first inform the terminal that I would like to run the program as it wasn't recognizing "vboxmanage" or "vboxmanage.exe" as a proper term. I learned how to do this with the `&` command acting as a "call operator", and designating the full directory path, in order to actually execute the program with the proper parameters. I first tried to utilize `start-process` but I couldn't figure out the proper way to set up the command, and found that `&` worked much easier.

![image](https://github.com/rat-v/Explorations/assets/169432484/c1d1fe65-2735-48c7-be2a-ce92efa036fd)

![image](https://github.com/rat-v/Explorations/assets/169432484/c388d1a0-eacb-40c0-a937-fb8c2949bac5)

