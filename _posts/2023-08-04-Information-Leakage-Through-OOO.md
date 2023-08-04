---
layout: post
title:  "Information Leakage Through OOO: Out-Of-Office Auto Responder"
author: mishaal
categories: [ technical, security, policy ]
tag: [ email ]
image: assets/post-images/leak.jpg
---

You may have gotten the following messages from business contacts several times in your professional career when emailing them. See if you can spot any information leakage:


`"I will be out of office from June 20 to 30. I will not have access to emails or phone service. Please reach out to Mark at 123-456-789 for urgent matters."`

`"....for urgent matters, please contact me at my mobile number (123) 456-789"`

`"I will be outside the US on business at This Expo from 22-25 Oct. For urgent matters, please contact jane.doe@email.com"`


Let's look at it from a hacker's perspective. A hacker can receive these emails as a result of their phishing campaigns to hundreds of harvested email addresses. They can now use these additional details for a more targeted attack. They can potentially:

1. Spoof that user's emails and pretend to be them to social engineer other employees. Since the user cannot be contacted for confirmation, it makes the hacker's requests easier. The email request may also look legit if the hacker mentions their travel plans with some emergency access requests.
2. The personal mobile number can be used for caller ID spoofing and vishing calls.
3. Revealing travel plans can alert potential attackers to target individuals' homes or offices during their absence.
4. Disclosing specific company projects or sensitive details in the autoresponder might provide valuable information to competitors or malicious actors.

While OOO messages serve a valuable purpose by informing senders about our unavailability and managing expectations, they may inadvertently lead to information leakage, potentially putting sensitive data at risk. 

## Best Practices to Mitigate Risks

Here's a perfect example of an out-of-office auto-responder message that does not leak any information while serving its purpose.

`"I am currently out of the office, please expect a delay in my responses."`

You may have the following concerns:
This simple sentence does not provide dates. The people who may be affected by your short absence, like for a project, will be informed well in advance. No one else needs to know the specifics.
It does not provide details of business or vacation. This information does not benefit anyone.
It does not provide a phone number or email of anyone else. Those in regular communications with you know your personal cell phone number or other team members to contact if you suddenly go off-grid for a few days.

Furthermore, you can limit the recipients of this autoresponder in most email clients. You can set one for internal users and one for outside the company or only set it for internal emails. You can also include this in your **information security policy** and provide instructions on *"how to set your out-of-office email message"* on your internal wiki page.

This is one additional layer of security, although a thin layer, that may protect against accidental information leakage. By understanding the potential risks and implementing best practices, we can safeguard sensitive data and ensure a more secure digital presence. 