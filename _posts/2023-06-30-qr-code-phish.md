---
layout: post
title:  "QR Code Phishing"
author: matt
categories: [ technical, security ]
tag: [ Technical ]
image: assets/post-images/qr-phone.jpg
---

While QR codes have been around for a while, this is the first time I've seen this phishing technique used in a real attack. Attackers are sending users QR codes to scan using their mobile devices. This approach typically bypasses all of your corporate security controls unless you tightly manage all of your users personal **mobile** devices.

How do you defend against this?

1. First, you need to make sure you are regularly **training** your users on phishing defense. Make them aware of these kinds of attacks.
2. Second, make sure you are using **MFA** on all externally facing applications to reduce the risk of attackers being able to use stolen credentials.
3. Third, make sure you are able to **detect** the use of stolen credentials, watching for sign-in's from IP addresses you don't recognize or access outside of business hours.


![QR Code Phish](/assets/post-images/qr-code-phishing.jpg)
