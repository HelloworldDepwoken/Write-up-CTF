# Meow

**Difficulty:** Very Easy

## 1. Setup

To connect to the target machine, I used OpenVPN with the configuration file provided by Hack The Box (HTB). Alternatively, Pwnbox can be used to access the lab environment without configuring a VPN on your own computer.

![OpenVPN connection](images/openvpn.png)

After connecting to the VPN, I used the `ping` command with the target IP address to check whether the target machine was reachable.

```bash
ping <TARGET_IP>
```

![Ping response](images/ping-response.png)

If the target responds to the ping requests, it indicates that the machine is reachable over the network. You can stop the command by pressing `Ctrl + C`.

After verifying the connection, I was ready to investigate the target machine.

## 2. Tools Used

- **Nmap:** Used to scan the target machine for open ports and identify running services.
- **Telnet:** Used to connect to the Telnet service discovered during enumeration.

## 3. Commands Used

| Command | Purpose |
|---|---|
| `ping <TARGET_IP>` | Check whether the target responds to network requests. |
| `nmap -sV <TARGET_IP>` | Scan for open ports and identify running services and their versions where possible. |
| `telnet <TARGET_IP> 23` | Connect to the Telnet service on port 23. |
| `ls` | List files and directories in the current directory. |
| `cat flag.txt` | Display the contents of the flag file. |

## 4. Enumeration

### 4.1 Scanning the Target

After confirming network connectivity, I used Nmap to identify the services running on the target machine.

```bash
nmap -sV <TARGET_IP>
```

![Nmap scan results](images/nmap-scan.png)

The scan revealed an open Telnet service on port 23. Telnet is a protocol that allows remote access to a machine through a text-based terminal.

Since the service was accessible, I decided to investigate whether I could connect to it.

### 4.2 Connecting Through Telnet

I used Telnet to connect to the target machine.

```bash
telnet <TARGET_IP> 23
```

![Telnet connection](images/telnet-connection.png)

The service presented a login prompt. This meant I needed to investigate whether valid credentials were required to access the machine.

### 4.3 Testing Authentication

I tested the `root` username with a blank password to check whether the service allowed access without a password.

![Telnet login](images/telnet-login.png)

The login succeeded, allowing me to access the machine as the root user.

This demonstrated a serious authentication weakness: the account could be accessed without a password. On a real system, this could allow an unauthorized user to gain extensive control over the machine.

### 4.4 Finding the Flag

After gaining access, I used `ls` to list the files in the current directory.

```bash
ls
```

![Directory listing](images/directory-listing.png)

The listing revealed the `flag.txt` file. I used the `cat` command to read its contents.

```bash
cat flag.txt
```

![Flag output](images/flag-output.png)

The file contained the flag required to complete the challenge.

## 5. Findings

The challenge demonstrated how an exposed remote-access service and weak authentication can allow unauthorized access to a machine.

The main steps were:

1. Verified connectivity to the target machine.
2. Used Nmap to identify the open Telnet service.
3. Connected to Telnet and tested whether authentication could be bypassed using a blank password.
4. Accessed the machine and located the flag file.

## 6. Lessons Learned

- **Network connectivity:** Learned how to check whether a target machine is reachable using `ping`.
- **Service enumeration:** Learned how Nmap can identify open ports and running services.
- **Authentication security:** Learned why accounts should use strong authentication and never rely on blank passwords.
- **Linux commands:** Practiced using `ls` to list files and `cat` to read file contents.

In a real environment, Telnet should generally be replaced with a secure alternative such as SSH, and accounts should be protected with appropriate authentication controls.
