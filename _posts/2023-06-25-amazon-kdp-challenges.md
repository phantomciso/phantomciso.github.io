---
layout: post
title:  "Amazon KDP Challenges"
author: mishaal
categories: [ book ]
image: assets/post-images/kdp-account-closed.jpg
toc: true
---


During the creative process of writing The Phantom CISO, one of the questions we discussed was, “How are we going to publish?” It’s no surprise that many authors contemplate this question. After a thoughtful discussion, we decided to self-publish for the following reasons:
1. More control over the content, editing, and ownership
2. Faster turnaround and quicker updates
3. Better margins

Of course, there’s a learning curve to self-publishing but it wasn’t complicated to set up. Unfortunately, after the setup process, we encountered complications that would discourage any self-publisher, and with perseverance, we overcame our obstacles.

We scoured the internet for answers, and while there were tidbits of information scattered throughout that helped us, we wanted to outline the obstacles and experiences in one place for self-publishing on Amazon so we can help others self-publish but also be aware of what we encountered, and how we managed through it.

# Amazon KDP
>TLDR: Self-publishing

Upon finalizing the book’s content, we decided to go with Amazon Kindle Direct Publishing (KDP) because they were the apparent leader in self-publishing. They list the book for free, have the highest reach, and it is the easiest option for consumers to purchase. Amazon KDP will publish, print and sell your book for you while keeping a 40% royalty fee minus book printing costs. They are one of Amazon’s oldest products for print-on-demand books and ebooks.

We wanted to configure KDP to represent both authors, so we performed the following tasks to ensure we were legitimate and also get the book ready to market:
- Bought a domain name and created an email address with our domain name to create a KDP account
- Created a legal entity to represent both authors
- Registered the entity with the IRS for tax purposes
- Used the free ISBN Number with KDP

Afterward, when we uploaded our book, it took a few days, but we were finally in the marketplace. Little did we know we were in for an insane ride with Amazon’s hyperactive brainless account flagging system.

# Account Suspension: Different Systems, Same Login
> TLDR: Using a Privacy.com card, SSO: KDP, eCommerce, Affiliates, AWS

After uploading the book to the KDP portal, we published it, and it went live on Amazon’s e-commerce marketplace. We saw an option to order author copies in KDP for ourselves at a discounted rate, so we ordered two copies using a virtual credit card service by privacy.com in Amazon’s e-commerce account. There are advantages to using privacy.com besides protecting your privacy, of course, such as segregating credit card numbers by merchant, setting limits, pausing transactions, or simply burning the card when it’s not required anymore. I’ve also used privacy.com for my personal amazon account. 

After a few hours we used the card to order the copies, our KDP login would not work, and we got the "Account Suspension" screen at logon. On the same page, there was a link to a form requesting us to verify the credit card information by providing an image of the card showing a name and a bank statement with the same name and address. This was obviously not possible as privacy.com is a virtual card, and any name and zip code can be used to authorize it to maintain privacy for online orders. We filled out the form and explained this along with providing a redacted screenshot of the card. 

So while our main Amazon e-commerce account was temporarily suspended, the KDP account was not suspended. We only knew that once we reached out to KDP support, and they mentioned that we needed to reach out to the main Amazon support team. 

After multiple calls and submissions with the main Amazon account team and being denied without reason, they finally understood our use of a virtual credit card. Roughly five days later, the account was reinstated.

During the time we were working with the account teams, fortunately the book remained live on the marketplace, and people were buying it, even though we couldn’t log into both accounts.

<p class="card p-4 text-center">
It's important to note that the Amazon ecosystem has multiple departments that function independently with separate support teams with their own terms and conditions. The only common element is the login procedure, a single sign-on (SSO) service to access completely different portals.
</p>

# Account Termination
>TLDR: Having the same bank account information on two different KDP accounts

In the following two weeks, we made some great sales, about 45 books, by promoting it only on LinkedIn. Then suddenly, our account status went to "**Terminated**" and the login screen said, "**This account has been closed.**" A week earlier, my personal account was also closed with the same message. There was no activity on my personal account. It did not seem like a coincidence.

The reason given was a generic "*content violation.*"

Now this is where there is a serious flaw in Amazon's support system:
- We could not dispute it; the email clearly stated they would NOT reinstate the account as we broke some policy they would not tell us.
- On further email inquiry, they refused to tell us the reason due to "security concerns." How are we supposed to dispute it if you don’t tell us a reason Amazon!
- They also said they would not transfer us any royalties earned, thereby "stealing" our book income.
- The email also said that this was a permanent ban and we could never use any of their services again. What a shocker, especially if no explanation is given.
- We could not open a case or get phone support as that requires logging into the KDP dashboard first, which we could no longer access. Opening a support case from another account was also impossible as they kept saying we had to open a case from the affected account, which was logically impossible. So their system was designed to trap us in this loop of helplessness.

At this point, it was clear that the Amazon support staff was not acting logically, rationally, or reasonably. Our frustration was real as there seemed no way through this.

We continued to reply to the automated and templated responses from KDP support on the original email thread. After 7-8 replies, their reasoning changed to "having multiple accounts." I realized that I configured my personal Amazon KDP account with the same bank account but my personal account was in my name and social security number for tax purposes, while the book account was in the name of another legal entity, with its own EIN tax number, shared by two authors. So legally, we did not have two accounts under one name and did not break any terms. Our only mistake was to have a common personal bank account between both accounts, as we were exploring bank options for the book’s legal entity at the time. But that shouldn’t matter as the two accounts were separate legal entities and we did not break any terms.

We were confident we had a legitimate case, but Amazon was not willing to review it for more than 5 seconds before auto-generating a templated response every single time.

# Quick Alternative
>Ingram Spark to the rescue

The same day the KDP account got banned, we researched other self-publishing options and opened an account with Ingram Spark, the largest publisher that caters heavily to self-publishing authors. We bought a new ISBN for $85 from bowker.com via Ingram Spark’s portal, and our book was live with them in 3 days. While our book was removed from Amazon, Ingram Spark pushed it to Amazon with the new ISBN, so we saw it live again, but this time sold by a third party. The upside was that the book was now available in bookstores like Barnes & Noble and any other store or library that ordered it. The downside was that the shipping time was about ten days, and the margins were negligible. But at least the book was back online while we sorted out the KDP fiasco.

# Methods Tried

After spending countless hours watching youtube videos and going through forums, we realized that thousands of people were going through the same account issues. A lot of them were bestselling authors with over 20 books. Almost all of them could not resolve it for many months and gave up. I noted all the techniques they mentioned and tried each one, hoping that at least one method would work (one will work if you're lucky).

## 1.  Opening Multiple Support Cases
>TLDR: Templated responses

As mentioned earlier, you cannot open any support cases if you cannot log into your account. Other accounts cannot reference a separate account. By filling out the online form on the account closure screen, you start a new case thread. But the results were always the same. They are so overwhelmed with cases that they do not give more than 5 seconds per case before clicking on a dropdown with a templated response which in most cases is completely unrelated. Like, *"content violation"* in my case for both accounts. Replies like *"We cannot offer details of our investigations"* or *"We reserve the right to terminate your account and Agreement at any time"* were also not helpful. 

## 2. Phone Support
>TLDR: No help, updates cases

While you can log into your "regular" Amazon account for product ordering, if you ask for a phone call back for a case from that portal and talk to them about your KDP account, they cannot help. They confirm that KDP does not have phone support, and the best they can do is put a note on that case for an update. I tried this 4-5 times each on both accounts, and at best, I got another generic response on the cases with something like *"We reviewed your case and stand by our original decision."*

## 3. The Jeff Bezos Email Method
>TLDR: Does not work

A popular method online is to write an email to jeff@amazon.com
This method does not work. I tried it nonetheless and have never gotten a response. I believe the executive team initially used this email for HR-related violations.

## 4. Chatting with KDP support members on LinkedIn
>TLDR: They ignore you

I found quite a few individuals on LinkedIn that worked for KDP support with keyword searches like:

- **Amazon KDP CS** (Customer Support)

All of them are out of two countries primarily: India and South Africa (except for a few executives out of Washington State, their HQ).

I sent a message to all of the LinkedIn contacts asking for a brief conversation. Almost all of them did not reply, and the few who did were not allowed to discuss any case-related issues outside the official channels. Another dead end.

## 5. Reaching out to the Head of Fraud
>TLDR: Reviews support cases, same templated response

I reached out to a few friends who worked in different departments of Amazon. They had access to the company phone directory and org chart. So I had them look up a few names for the KDP support staff I found on LinkedIn to see who they report to. They had titles like:

- **Fraud and Abuse Manager**
- **Books Risk Management**

I found the head of KDP customer support. I did not want to call or email him as he would question how I got his information, and he would simply not entertain any cases outside their portal. So my friend chatted with him internally and gave him my email address to look up the case. He said he would ask his team to look into it. The next day, I got the same scripted response from their support, saying they stand by their decision. Back to square one! But I was determined.

## 6. Letter to WA Attorney General
>TLDR: Official complaint, no follow-up

When no human was willing to discuss the case with me, I decided to complain to the Washington Attorney General as an official way to [file a complaint](https://www.atg.wa.gov/file-complaint) against a company headquartered in their state. The complaint goes in their public record. Their website also noted that they are overwhelmed with over 2000 cases a month. So, I did not expect any outcome and have not heard back from them.

## 7. Complaint to BBB
>TLDR: Useless, don't waste your time

A popular method is to file a complaint against a business on the Better Business Bureau website. No action is taken from them, and it only serves as a portal to look at public complaints against a company. We did not waste our time there.

## 8. Legal Demand Letter
>TLDR: Legal Action.

At this point, I drafted a legal demand letter using some online templates. (You can use a service like [PeopleClerk](https://www.peopleclerk.com/) to draft a free demand letter). I kept it very simple, defining the problem and that I just wanted my accounts reinstated, otherwise I would take further legal action against Amazon Inc. We hired a lawyer, a friend specializing in consumer rights cases, to send the letter on our behalf for better impact.

You can contact him here and reference this article: [TariqLaw.com](https://www.tariqlaw.com/)

Within a few days, Amazon's legal team emailed him acknowledging receipt and said they would look into it.

About ten days later, I randomly tried to log into our KDP account, and to my surprise, both the book and my personal account were reinstated. The same day I got an email from KDP support stating that they had reinstated the accounts "as a one-time exception" and that "any further violation to the content guidelines will negatively impact the account status." This was hilarious as it was clearly due to the legal threat.

The next day our attorney got an email from Amazon's legal team saying that both accounts were reinstated on further investigation, and they apologized for any inconvenience.

## 9. Small Claims Court
>TLDR: Last Resort

If the accounts had not been reinstated, our next step was to file a claim under the small claims court as a final step. Thankfully it did not get to that.

# Royalties Inaccessible
The book royalties dashboard still said "account closed," but it was resolved within a day after I opened a support case. It shows that all their internal portals are maintained and managed separately, often breaking the integration.

# Lesson

Some valuable lessons learned after this ordeal:
- Take the time to separate everything for your business (emails, tax IDs, bank accounts)
- Always have a redundancy plan. Publish the book on Ingram Spark and buy your own ISBN ($85). Then publish the same book under the same ISBN on KDP. People buying through Amazon will buy the print-on-demand version from Amazon with Prime benefits. If KDP bans your account, the underlying Ingram Spark version will show up and still be orderable via third-party sellers, or Amazon will order the book from Ingram and ship it once they receive it in stock. It will also be distributed to brick-and-mortar bookstores like Barnes & Noble and libraries.
- Ensure you don’t use copyrighted or “googled” images for your cover. They will often flag them, even if they are royalty-free images. We noticed many cases like this in our research. Make sure your artwork is original. Create it yourself or hire an artist to design it.
- Be patient and follow through. Do not give up; all it takes is one method to succeed. Be persistent, polite, and professional. Everything is recorded and will be "on file." If you are in the right, continue the fight.

If you are in a similar situation, hopefully this experience will help you either set up your infrastructure correctly or follow the right method to resolve your issue.


