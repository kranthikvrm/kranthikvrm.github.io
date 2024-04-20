---
layout: post
author: kranthikvrm
title: My experience as a SOC Analyst at Infosys
description: In this blog post, I am sharing my experiences from my first year at RGUKT Nuzvid, where I experienced new faces, challenges, and exciting opportunities on my journey towards becoming an engineer.
author: Kranthi Kumar
date: 2022-12-13 02:34:00 +0800
categories: [Personal expereince]
tags: [SOC Analyst, SOC]
img_path: /images
image:
  path: my_soc_experience.jpg
pin: true
---

Hey, Hi, I am Kranthi Kumar. In this blog post, I will share my experience working in the SOC, what I did, how I learned things, the timings, and how it feels. You can read more about me here.

SOC is the first line of defense for a company, so people working in SOC should be careful because sometimes it may affect the entire company if they leave something without proper analysis.

## How I started in SOC

After my Bachelor of Technology (BTech) in Computer Science, I received an offer from Infosys. Having penetration testing experience, they considered me for SOC because I know security basics and have an idea of how things work in the security domain. That's how I started my journey as a SOC analyst at Infosys.

## Training or KT

Initially, I received KT (Knowledge Transfer) from my team lead and other team members, similar to training sessions. As days passed, I became friends with PremChand, he is one of the good friends I can talk to without any hesitation. In security there is nothing static, things change very often, and we should learn every day and ask questions too.

## Daily routine - A typical day in SOC

With training from team members, I started working, and I believe those who want to get into SOC know about SIEM, so not need to elaborate about it. we used Splunk from our client (cilent gave us) and mostly IBM Qradar as a SIEM tool (from Infosys side). With SIEM, we can check for malware alerts, phishing email alerts, information leaks, brute force attacks, failed logins, and many more.

Once an alert is seen, according to the work environment, we assign tickets to work on. 

### Example

For example, if I receive a phishing email alert from SIEM, I take action on it. Often, the system will automatically “quarantine” emails or block them (Proofpoint) from actually hitting the mailbox until the email is approved after analysis. I perform some basic analysis like:

- Email addresses that are close but a little off.
- Links that reveal an unfamiliar address when hovered over.
- Domain names that are close to those of a company or person but not quite right.
- Grammar and spelling errors.
- Suspicious attachments and sense of urgency.
- Emails requesting login credentials, payment information, or sensitive data.
  
Additionally, I check and test the domain using (https://urlfiltering.paloaltonetworks.com/) only if your organization has a Palo Alto firewall, and I conduct email header analysis using https://mxtoolbox.com/EmailHeaders.aspx.

Alongside these, I check the three main email security protocols DMARC, DKIM, and SPF. Implementing them all provides the best protection.

> Sender Policy Framework (SPF) is an email authentication standard that domain owners use to specify the email servers they send email from, Domain spoofing can be avoided with SPF.

> Using DKIM, a sender can attach DKIM signatures to an email (a header that is added to the message and is secured with encryption).

> We check DMARC because the domain the end-user sees is the same as the domain validated by DKIM and SPF.

Similarly, we conduct phishing email analysis. Proofpoint offers a sandbox environment to test attachments like macros and links for analysis. I believe I've given a general idea of phishing email analysis.

## False positives

How SOC analysts deal with false positives??? Practice and experience, double-checking things with different sources, and if you really aren't sure even after exhausting all other options, you can ask colleagues for another opinion. It's also important to understand what behavior triggered that alert.

It's quite common to get false positives in SIEM, people feel a little scared when they just start (from my own experience 😁), but at the end of the day, we learn and progress.

## EDR Tools

There are many Endpoint Detection and Response (EDR) tools like CrowdStrike, Sentinel, and Microsoft Defender. The functionality is mostly the same, we have visibility into endpoint activities and access to what processes are running on the host systems, what activities the users are doing. We can isolate a system (containment) if we find any malicious activity running or a system infected with malware. These EDR tools continuously monitor and analyze host and process behavior to detect suspicious activities. We get all this data into SIEM in the form of logs. Most EDR tools use machine learning algorithms and behavioral analysis.

I have used Microsoft Defender as an EDR tool, and we get data like local and external addresses to which a particular host is connected, all the user accounts that have logged in, archive file creation, processes execution, and the use of external media storage like (Pendrives, etc.).

This data is useful for our analysis to make decisions.

## IDS/IPS and Firewall (Technical controls)

At Infosys, they used Palo Alto firewalls. To be honest here, we don't really configure or do integrations as Tier 1 analysts. we understand how Firewalls, IDS/IPS work and know the differences and their functionalities in real-time. We mainly conduct log analysis on the logs generated by these security controls.

Firewall: A firewall is a security system that monitors and controls network traffic based on a set of security rules. It works and detects based on predefined rules that we write.
  
IDS (Intrusion Detection System): An IDS is an application that monitors network traffic and searches for known threats and suspicious or malicious activity. IDS only detects but won't take any action on it. We should act on it by utilizing the generated alerts.
  
IPS (Intrusion Prevention System): An IPS is a network security tool (which can be a hardware device or software) that continuously monitors a network for malicious activity and takes action to prevent it, including reporting and blocking.

## Tools that SOC Analysts use mostly

In day-to-day activities, we use VirusTotal to check for IOCs of files, AbuseIP DB for checking malicious IPs (a cybersecurity tool that operates as a community-based IP blacklist database), Proofpoint for phishing email analysis, and Any.run as a sandbox to test malicious executable files to understand their behavior. We use SIEM and ticketing tools like JIRA and SolarWinds, Defender 365 and CrowdStrike for EDR.

## Conclusion

Finally, as a SOC Analyst at Infosys, I learned a lot about blue teaming, security working culture, and corporate management. We have to do rotational shifts to fulfill the work requirements and keep learning and upgrading every time we encounter something new. Make friends to support you and have fun wherever you go.

Thank you for reading, my digital warriors!!!

If You have any queries or thoughts, then feel free to share them with me on <a href="https://www.linkedin.com/in/kranthi-kumar-manda/">LinkedIn</a>.
