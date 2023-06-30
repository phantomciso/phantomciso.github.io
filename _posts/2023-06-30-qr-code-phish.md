---
layout: post
title:  "QR Code Phishing"
author: matt
categories: [ technical, security ]
tag: [ Technical ]
image: 
---

This is the first time I've seen this #phishing technique. Attackers are sending your users QR codes to scan using their mobile devices. This approach typically bypasses all of your corporate security controls unless you tightly manage all of your users personal devices.

How do you defend against this?

First, you need to make sure you are regularly training your users on phishing defense. Make them aware of these kinds of attacks.

Second, make sure you are using MFA on all externally facing applications to reduce the risk of attackers being able to use stolen credentials.

Third, make sure you are able to detect the use of stolen credentials, watching for sign in from IP addresses you don't recognize or access outside of business hours.

As part of a vulnerability management program its important to run a vulnerability scan of your systems on a regular basis. When the scan is complete there are usually thousands of vulnerabilities identified. Customers frequently ask how they should prioritize remediating those vulnerabilities since nobody has time to do them all.

![QR Code Phish](/assets/post-images/1687798480506.jpg)
