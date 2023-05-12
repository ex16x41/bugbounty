# types of redirects in exploiting the vuln

The vulnerability in all types of redirect attacks (reflected, stored, and DOM-based) is due to improper input validation or sanitization

| types | meaning | example | to loc try
|:---:|:---:|:---:|:---:|
|reflected (most common type) server side | A reflected open redirect occurs when an attacker can inject a redirect URL into a request parameter that is immediately reflected back to the user in the application's response.| https://www.example.com/login.php?redirect_url=https://www.attacker.com/malicious-page.html | dorks, linkgopher filter, manual inspection, js, html, links, hrefs,  | 
| stored (server side)| A stored open redirect occurs when an attacker can inject a redirect URL into a server-side storage mechanism (such as a database) that is later retrieved and executed by the application.| 1. A news website that allows users to submit comments on articles could be vulnerable to stored open redirects. An attacker could submit a comment that includes a malicious redirect URL, which could be stored in the website's database and later executed when other users view the article and its comments. For example, the attacker could inject a URL that redirects the user to a malware download page. https://www.newswebsite.com/article/12345#comment-67890?url=http://maliciouswebsite.com/malware
 the user is viewing article number 12345 on the news website and is looking at comment number 67890 on the same page. The attacker has injected a malicious URL parameter url that points to a malware download page. The news website may have stored this URL in its database as part of the comment, and other users who view the same article and comment could be redirected to the attacker's malware download page if the website does not properly validate or sanitize the input. | 
|DOM based (client side) | A DOM-based open redirect occurs when an attacker can manipulate the client-side DOM (Document Object Model) to cause a redirect to occur, without any server-side involvement. This type of vulnerability is specific to client-side scripting languages such as JavaScript.| 

# types of redirects by design

| types | meaning | input
|:---:|:---:|:---:|
| Internal or Local Redirects |  These redirects occur within the same website. They are used to redirect users from one page to another within the same domain. Internal redirects are commonly used for site maintenance, updating content, and improving navigation.| can be great for testing for info exposure with local 127.x.x type/ trusted | 
| External Redirects (high priority)| These redirects occur when a user is redirected to a page on a different website or domain. External redirects can be useful for linking to external resources, tracking clicks, and managing affiliate programs.| 


# pivot from redir to other 

| type |
|:---:|
| XSS |
| XSS |
| XSS |
| XSS |

# test for open redirect vulns via dorks 

| value |
|:---:|
| inurl:redirect= |
| inurl:rdir=  |
| inurl:to=  | 
| inurl:destination= |
| inurl:ReturnURL=  |
| inurl:redirect_uri= |
| inurl:/allowcookies= | 
| inurl:next= | 
| inurl:url=https | 
| inurl:url=http |
| inurl:redirect?https | 
| inurl:redirect?http | 
| inurl:url=http |
| inurl:?goto= | 
| inurl:/?node= | 
| inurl:/setLanguage.php?return= | 
| inurl:?url= |
| inurl:?sUrl= | 
| inurl:?from= | 
| inurl:?home= | 
| inurl:?redir= | 
| inurl:?link= | 
| inurl:?r= | 
| inurl:?resource= | 
| inurl:?return= |
| inurl:?referer= |
| inurl:?ref= | 
| inurl:?retour= | 
| inurl:?back= | 
| inurl:?file= | 
| inurl:?rb= | 
| inurl:?end_display= | 
| inurl:?urlact= | 
| inurl:?redirectBack= | 
| inurl:/search?q= | 
| inurl:/r.php?u= | 
| inurl:?page= | 
| inurl:?l= | 
| inurl:?loc= | 
| inurl:?path= | 
| inurl:?r2= |
|redirect.html?open&url= |
| redirects/redir.cgi?full_url= |


# Note
* run search excluding words that can include false positives and links which include login portals because often will require authentication to redirect (in most cases anyway) but changing action e..g, logout = may be successful 

use something like: 

inurl:logout?returnUrl= -tickets -user -docs -kr  -account  -signup -signin -login -support -enroll -register -questions -logon -help -signin -log -password

a good example would be checkout, logout, signout, allowcookies, etc. 


# Automation 


