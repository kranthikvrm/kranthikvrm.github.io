---
layout: post
author: kranthikvrm
title: An IDOR and SQLi bugs leads to the leak of sensitive information.
description: In this blog post, I am sharing my experiences from my first year at RGUKT Nuzvid, where I experienced new faces, challenges, and exciting opportunities on my journey towards becoming an engineer.
author: Kranthi Kumar
date: 2023-08-24 08:13:00 +0800
categories: [CTF, Bug Bounty]
tags: [CTF, Bug Bounty]
img_path: /images
image:
  path: idor_post.jpg
---

Hello, I am Kranthi Kumar. You can read more <a href="https://kranthikvrm.github.io/about/">about me here</a>. In this blog post, I will share how I randomly found an IDOR bug that led to a sensitive information leak.

While randomly checking my bank details and stuff, I came across a web portal where I could check my uploaded documents. Thus, I began to review the documents I had uploaded. Interestingly, the document ID parameter is passed on the URL. Since I often check for IDOR and XSS vulnerabilities if anything seems suspicious, I attempted to change the document ID value in the URL. Boooommmm!! I accessed a document containing PAN card details, bank statements, and other sensitive information belonging to a person I don't even know.

Realizing the vulnerability on the site, I conducted reconnaissance and attempted a basic SQL injection. I received SQL errors which could potentially lead to data exfiltration from the database. Attackers could easily dump the entire database.

Although there may be other bugs, I don't have permission to conduct a pentest on that application. Even attempting the above mentioned activities was not allowed. However, I do have an account with them, which means my data is also at risk, along with that of other customers. Therefore, I immediately sent an email to the Bank IT team. One of the members replied, stating, "Our team is looking into the issue." 

![IDOR and SQLi bugs](idor_bug_details.png)

After two days or so, they remediated the issue, and I received a THANK YOU!!! email from them.
![IDOR and SQLi bugs](idor_bug_details2.png)
