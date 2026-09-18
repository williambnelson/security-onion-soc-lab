# Juice Shop Observations


## Challenge 1: Access a Confidential Document

**Method:** I went to the about page, and then accessed the site’s legal information. From there, I simply had to delete part of the URL to traverse the directory. This allowed me to access a series of confidential documents.

**Detection:** When I tried to access files that generated 403 errors, Security Onion generated “GPL WEB_SERVER 403 Forbidden” alerts. However, when I tried to access files that generated no errors, Security Onion did not generate any alerts. It did generate zeek notifications under hunt, but those require a bit more digging to find. Essentially, in order for a NIDS to work properly, security professionals must look for and recognize suspicious activity which can then be acted upon.

## Challenge 2: Leave a Zero-Star Rating

**Method:** I went to the Customer Feedback page, left a comment, and solved the CAPTCHA. However, I did not leave a rating for the store. Instead, I inspected the “Submit” button, found the “disabled=true” field, and deleted it. Upon pressing enter, I left a zero-star rating for the store, which should not have been possible for a normal user.

**Detection:** Security Onion did not generate any alerts for my activity. Even upon looking through hunt, there were no notifications generated besides normal access to the website. This shows certain types of attacks or exploits cannot be detected, even by a well-configured NIDS. It is therefore incredibly important to ensure a web application is secure in its design, so covert attacks like this are less likely to take place.
