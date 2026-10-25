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

Document the scan results, the services you identified, and why you decided to investigate them.

## 5. Findings

Explain what you discovered during the challenge and how you reached your conclusions.

## 6. Lessons Learned

Summarize the technical concepts you learned and what you would investigate differently next time.
