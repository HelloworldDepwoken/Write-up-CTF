# Fawn

**Difficulty:** Very Easy
## 1. Setup

To connect to the target machine, I used OpenVPN with the configuration file provided by Hack The Box (HTB). Alternatively, you can use Pwnbox to access the lab environment without setting up a VPN on your own computer.

![OpenVPN connection](ImgF/OpenVPN.png)

After downloading the Starting Point VPN configuration file, I opened the terminal and ran the following command to connect to the VPN.

```bash
sudo openvpn <path-to-file>
```

![Terminal OpenVPN connection](ImgF/OpenVPNconnect.png)

To get the target's IP address, I pressed the **Start Machine** button on the HTB website.

![Get IP address](ImgF/Pwan.png)

After waiting for a while, the target machine's IP address will appeared on the page. Keep in mind that the IP address may change each time you start a machine, so make sure to use the IP address currently displayed on the HTB website.

![IP address](ImgF/FawnIP.png)

After connecting to the VPN, I used `ping` command with the target's IP address to check whether the machine was reachable.

```bash
ping <TARGET_IP>
```

![Ping response](ImgF/IP.png)

If the target responds to the ping requests, it indicates that the machine is reachable over the network. You can stop the command by pressing `Ctrl + C`. However, some machines block ping requests, so no response does not always mean the machine is offline.

Now that the connection was set up, I was ready to start investigating the target machine.

## 2. Tools Used

- **Nmap:** Nmap is used to scan the target machine by sending network packets to its ports and analyzing the responses. These responses help determine which ports are open, closed, or filtered by a firewall. It can also identify the services running on open ports. When using the `-sV` option, Nmap sends additional probes to identify the services and their versions, if possible. This information helps us understand what the target machine is running and decide which services need further investigation. Knowing the service version can also help us identify potential vulnerabilities.
  
- **FTP (File Transfer Protocol):** FTP uses TCP to communicate between a client and a server. It commonly uses port 21 for the control connection, which carries commands such as listing directories and requesting files. During file transfers, FTP uses a separate data connection to transfer file contents or directory listings. How this data connection is established depends on whether FTP is operating in active or passive mode. When a data transfer finishes, the data connection is typically closed, while the control connection remains open for additional commands until the user disconnects.

## 3. Commands Used

| Command | Purpose |
|---|---|
| `nmap -sV <TARGET_IP>` | Scan the target machine and identify its running services and versions. |
| `ftp <TARGET_IP>` | Connect to the target machine's FTP service. |
| `ls` | List the files and directories in the current directory. |
| `cat <FILE>` | Display the contents of a file. |
| `pwd` | Check the current working directory. |
| `get <FILE>` | Download a file from the FTP server to my computer. |

## 4. Enumeration
so at first right after we are making sure that the server was reachable i use nmap to see which service was running on the server Nmap -sV [Target IP]
![nmap](ImgF/)
as we can see i found that the server was running a FTP service an FTP service is on Service that using for Transfer a File mostly it open on port 21 but FTP is an old service that mostly running on Legacy server because the FTP service Transfer a File with out encyption them and some even allow to login using Username as anonymous the in newwer version it should use SFTP so right in about that we will try to reach the service by using FTP [Target IP] 
![FTP](ImgF/)
and we are in one way to see if we were in the service is by checking the responds code by the succe connect it will show us 220 and now it asking for the username so let try using Anonymous if it work 
![FTP_User](ImgF/)
as we are in it asking for the password left it blank or just press enter because we are in by using annoymous 
![FTP_Anonymous](ImgF/)
ah it work and now we are in the server by checking the responds code by the succe Login it will show us 230 and as we are in let see what we can found so frist i will use ls to check what file inside the Server
![FTP_Ls](ImgF/)
and there the flag we are caming for and becuase the file was in the server we cannot use cat to see what inside the file we have to download it into our own computer using Get [file name] and if we were got everything we want just type in bye to disconnect from the server and the respond code of 221
![FTP_Get](ImgF/)
and after we are download the file we can open it by found the file in our meachine or just viwe it by using cat in this case i will use cat so first i will check what path we are on so i use Pwd command to check it Pwd
![Pwd](ImgF/)
as you can see the Pwd showing us the User name of the Login and a path after we know that let use ls to show if the file in this path ls
![ls](ImgF/)
and we can see it in now we viwe the file using Cat [File name]
![Cat](ImgF/)
and we got the flag

## 5. Findings

Explain what you discovered during the challenge and how you reached your conclusions.

## 6. Lessons Learned

Summarize the technical concepts you learned and what you would investigate differently next time.
