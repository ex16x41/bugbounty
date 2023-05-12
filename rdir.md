# types of redirects

| types | meaning
|:---:|:---:|
| local only  | Some websites will blacklist some requests to only allow requests to theirsite.com or /localendpoint. Armed with an open redirect on their domain, depending on their framework and how they handle redirects, you can sometimes bypass their blacklsit and achieve SSRF or RCE (depending on the circumstances). Imagine you have an endpoint which takes an ?url= parameter but it will only allow you to input local endpoints, such as /example. Now imagine you also have an open redirect at /redirect?goto=//127.0.0.1/. Pointing ?url= to this endpoint may cause their web application to trust the user input (since it is pointing to local endpoint), but process the redirect & show you sensitive information.  |
|reflected (most common type) | A reflected open redirect occurs when an attacker can inject a redirect URL into a request parameter that is immediately reflected back to the user in the application's response.| 
| stored | A stored open redirect occurs when an attacker can inject a redirect URL into a server-side storage mechanism (such as a database) that is later retrieved and executed by the application.| 
|DOM based | A DOM-based open redirect occurs when an attacker can manipulate the client-side DOM (Document Object Model) to cause a redirect to occur, without any server-side involvement. This type of vulnerability is specific to client-side scripting languages such as JavaScript.| 


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


