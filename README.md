# CTF-anonymous

This will be the first of several series of a CTF that I've been doing as my final project in my Master Degree in Cybersecurity.

In here I will explain the steps I followed and all the tools I used in order to find the different flags.

## Procedures followed

I followed a series of steps in order to succeed in the finding of the flags in the different scenarios.

- Enumeration and fingerprinting of a real machine
- Detection of one or multiple vulnerabilities, as well as weaknesses or configuration flaws in real machines
- Study of mitigation measures
- Detection and implementation of privilege escalation in a real environment
- Detection and exploitation of vulnerabilities in system and web environments

## Lab environment

The lab environment I created and used was the following:

- A MacBook Pro as a main machine under which I launched several VMs
- VM 1: Kali Linux machine using different tools such as Gobuster, Dirbuster, Metasploit, Burpsuite and network scanning tools
- VM 2: Linux Mint running Docker to perform the different pentesting techniques to three different machines (in separete containers)
- VM 3: Debian machine used to perform vulnearbility scan using Tenable Nessus and some Steganography techniques

<p align="center">
  <img src="imgs/LabEnvironment.png">
</p>

# Let's start 😃

## Enumeration and fingerprinting

First of all, I will start with the <b>Enumeration</b> part of this CTF.
To be honest, I already knew upfront the IP's I had to attack, but ususally I should have started using ```Netdiscover``` tool.

<p align="center">
  <img src="imgs/NetdiscoverImage.png">
</p>

>[!TIP]
>In order to install and use it, you can follow the steps on the [Kali](https://www.kali.org/tools/netdiscover/) web page.

Using following command I should be able to allocate some IP's in the current network.

```linux
$ sudo netdiscover -i eth0 -r 192.168.1.0/16
```

<p align="center">
  <img src="imgs/NetdiscoverOutput.png">
</p>

Now that I allocated the ```victim machine```(192.168.1.103), I can scan it and see what ports are open.
```linux
$ nmap -F 192.168.1.103
```

<p align="center">
  <img src="imgs/OoopsMachineScan.png">
</p>

I can see folllowing ports open:

|PORT|STATE|SERVICE|VERSION|
|----|-----|-------|-------|
|21/tcp|open|ftp|vsftpd 3.0.3|
|22/tcp|open|ssh|OpenSSH 7.6p1 Ubuntu|
|8080/tcp|open|http|Apache httpd 2.4.29|

# PORT 21/tcp

By making a more deep scan on ```port 21``` I can see that ```anonymous login``` is allowed.

<p align="center">
  <img src="imgs/Port21Scan.png">
</p>

So I will try to connect to the server using ```anonymous``` as the following credentials: ```login``` and ```password```.

>[!NOTE]
>When I typed the credentials on the password part, it was obviously not visible 💂‍♂️.

<p align="center">
  <img src="imgs/AnonymousLogin.png">
</p>

Once in the server, I list the contact of the actual directory:

```linux
$ ls -la
```
<p align="center">
  <img src="imgs/AnonymousLS-LA.png">
  <img src="imgs/AnonymousLS-LA.2.png">
</p>

After having logged in via ftp session, I decide to <b>list</b> the directory content to see what other folders/files exist in the remote directory.I see that there is a folder called <b>html</b>. I can enter without problems using the cd (change directory) command and inside I list the content again: index.html.bak, index.php

<p align="center">
  <img src="imgs/HtmlFolder_content.PNG">
</p>

I choose to download these files for further exploration. I do this process through the terminal with the GET command.

```linux
get index.html.bak
get index.php
```
<p align="center">
  <img src="imgs/GetCommand.PNG">
</p>

I make a quick listing on my current diretory in the Linux machine to check if the files have been downloaded correctly.

<p align="center">
  <img src="imgs/ListingDownloadedIndexHtmlFiles.PNG">
</p>


>[!NOTE]
>THIS REPO IS STILL UNDER 🚧 CONSTRUCTION 🚧
