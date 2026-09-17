# Juice Shop Observations


## Challenge 1: Access a Confidential Document

**Method:** I went to the about page, and then accessed the site’s legal information. From there, I simply had to delete part of the URL to traverse the directory. This allowed me to access a series of confidential documents.

**Detection:** When I tried to access files that generated 403 errors, Security Onion generated “GPL WEB_SERVER 403 Forbidden” alerts. However, when I tried to access files that generated no errors, Security Onion did not generate any alerts. It did generate zeek notifications under hunt, but those require a bit more digging to find. Essentially, in order for a NIDS to work properly, the network itself must be properly configured for the NIDS to recognize suspicious activity which can then be acted upon.


## Challenge 2: Determine the answer to Emma’s security question

**Method:** I looked up the emails associated with the domain, juice-sh.op. One such was emma@juice-sh.op, associated with the user E=ma2. I looked at the site’s photo wall and found a photo of her first workplace, which included the company’s title upon zooming in. As it turns out, that was the answer to her security question, allowing me to log on to the site with her account and change her password.

**Detection:** Security Onion did not generate any alerts for my exploitation. It did generate zeek.http logs under hunt, but those could easily blend in with ordinary traffic if security professionals did not pay full attention. Upon inspecting the notification, it does detail a change of password from the Kali VM’s IP address. This proves that it is important to inspect suspicious logs, even if they are just a little out of the ordinary. Furthermore, the vulnerability proves the importance of obfuscating personal information, because even if it is hard to find, an attacker can still use it for exploits.
