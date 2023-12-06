# Weak Reset Password Implementation

The bug name which I found was “Password Reset Link Not Expired After Use”. This comes under the VRT of “Insufficient Security Configurability >Weak Reset Password Implementation > Token Not Invalidated After Use”

Steps To Find This Bug:

    Go to https://target.com/ password reset page.
    Enter your email, and ask for a password reset link.
    Now go to mail and open that link in two tabs.
    Reset the password from one tab, reload the other tab , and if it let’s you reset password again then it is vulnerable to token not invalidated after use as we are resetting the password two times with same token.

Impact/Exploit Scenario: If victim’s email account is still logged into his/her Office Computers or any public Internet Café. Then any external attacker can use the used token to reset victims password.

Severity: Now due to this difficult to happen exploit scenario , which requires user interaction it is given as a P4 bug under Bugcrowd VRT.

Now this feature can be also used to sometimes chain it with other vulnerabilities, to get higher severity depending on the functionalities present in the website.


# bypass 403 to 200 

How to Bypass 403 restrictions?

There are many headers and paths which you can use to bypass 403 restrictions.

    Adding in URL Paths: Adding this in paths of the URL and the file which is forbidden
    /*
    /%2f/
    /./
    /
    /*/
    Adding Headers in request :By adding different headers in request with value 127.0.0.1 can also help in bypassing restrictions.

X-Custom-IP-Authorization
X-Forwarded-For
X-Forward-For
X-Remote-IP
X-Originating-IP
X-Remote-Addr
X-Client-IP
X-Real-IP

Reference: https://github.com/yunemse48/403bypasser

3. Changing the request method type: Changing method from GET to POST , etc can also lead to bypass.

Reference: https://infosecwriteups.com/403-forbidden-bypass-leads-to-hall-of-fame-ff61ccd0a71e

So now this is a general concept and methodologies for bypassing 403, now let’s move forward to what I did in my case.
Steps I Did:

1)First I went to pagespeed admin panel location http://target.com/pagespeed_admin/ and found out it was 403-Forbidden.
Restricted Pagespeed Admin Panel

2)I used the above specified methods via a automated tool (which is basically a bash script for 403 bypass methods)

Link: https://github.com/iamj0ker/bypass-403

Found that in one case response code changed from 403 -> 200 , so I tested it manually in browser and it finally BYPASSED!!😈

3)Method was http://target.com//pagespeed_admin/ just adding single slash bypassed the 403 and got complete access to pagespeed admin.
BBypassed Pagespeed Admin Panel

# SXSS

So in one of the subdomain of the program I received, had a feature of styling a page of app by adding different features and styles.
Feature Page
https://miro.medium.com/v2/resize:fit:720/format:webp/1*Uofls0J7jc-7cNpzP7lkTA.png 

In there in each and every section like “ Name” , “A little about yourself” etc I injected XSS Payload “><img src=x onerror=alert(document.cookie)>
Injected Payload
https://miro.medium.com/v2/resize:fit:720/format:webp/1*qdNBuMn2vKRPexGdQzZ6Kg.png 


Now as I clicked on “Add Content” I got XSS Pop Up.
Payload Executed
https://miro.medium.com/v2/resize:fit:720/format:webp/1*AovyvCNKMe8N5qsCA-xx1g.png 

But here as you can see, it has no get parameters or anything or not even share feature, which I could use to send this to other user, otherwise this is right now Self Stored XSS, which is a P5/no-impact vulnerability☹️.

So I started looking for ways with which I can increase the impact, or any methods I can send this page to other users, then the QR Code on the top right corner just caught my eye🧐, so I thought of testing it.

As soon as I scanned this QR Code it opened up a site, In which my XSS payload executed😍, so finally I have converted Self XSS to Non-Self XSS hance now P2 severity😈.

https://miro.medium.com/v2/resize:fit:720/format:webp/1*Yuh6s-H2ZvWgrXLMDIQxlQ.png 
Non Self Executed XSS
