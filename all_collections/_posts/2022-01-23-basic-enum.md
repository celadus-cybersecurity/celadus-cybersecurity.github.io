---
layout: post
title: Pentesting - Basic Enumeration Tools
image: /assets/img/basic1/1.png
categories: [nmap,wfuzz,gobuster,enumeration,ss]
---

***Only for educational purposes.***
***I am not responsible for any illegal use.***


## Port Scan

Nmap is a **network scanning tool** that uses IP packets to identify all the devices connected to a network and to provide information on the services and operating systems they are running.

**Unauthorized port scanning, for any reason, is strictly prohibited**

```bash
sudo nmap -sS -sV target.local
```

```bash
-sS: TCP SYN Scan Technique
-sV: Probe open ports to determine service/version info
```

![[1.png]]

## Sub-domain Enumeration

Wfuzz is **a tool designed for bruteforcing Web Applications**, it can be used for finding resources, directories, scripts, subdomains etc.

```bash
wfuzz -w /usr/share/amass/wordlists/subdomains-top1mil-110000.txt  -u http://target.local/ --hc 301 -v -c -H "Host:FUZZ.target.local"
```

```bash
-w: Specify a wordlist file
-u: Specify a URL for the request

--hc: Hide responses with the specified code

-v: Verbose information
-c: Output with colors
-H: Use header (ex:"Cookie:id=1312321&user=FUZZ" or "Host:FUZZ.target.local")
```

## Directory Enumeration

Gobuster is **a tool used to brute-force URIs including directories and files as well as DNS subdomains**.

```bash
gobuster dir -u http://target.local/ -w directory-list.txt -x .php,.bak
```

```bash
dir: Uses directory/file enumeration mode
-u: The target URL
-w: Path to the wordlist
-x: File extension(s) to search for, in our case .php and .bak
```

## Monitor Network Connections

- Assume that we spawn a low level shell in our target machine

- The ss command is **a tool that is used for displaying network socket related information on a Linux system**.

- The grep command can **search for a string in groups of files**.

```bash
ss -an | grep 127.0.0.1
```

```bash
-a: retrieve a list of both listening and non-listening ports
-n: dont resolve service names

Symbol | : A pipe is a form of redirection (transfer of standard output to some other destination) that is used in Linux and other Unix-like operating systems to send the output of one command/program/process to another command/program/process for further processing.

grep 127.0.0.1 : search for string that contains the IP 127.0.0.1
```


