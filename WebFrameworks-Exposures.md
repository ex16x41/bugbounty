# Table 

| By Priority| 
| ------------- |
| Laravel (X framework) | Dork | 
| **Blind xss (part of persistant)** Blind cross-site scripting is similar to stored cross-site scripting, but in a blind XSS attack, the web application stores the payload sent by an attacker and only executes it later – at a different time, in a different place, or possibly even in another web application.  - https://www.acunetix.com/websitesecurity/detecting-blind-xss-vulnerabilities/ Example of web applications and web pages where blind XSS attacks can occur: Contact/Feedback pages, Log viewers, Exception handlers, Chat applications / forums, Customer ticket applications, Web Application Firewalls, Any application that requires user moderation  | 
| **Reflected** -when a user clicks on a malicious link or submits a form containing the script, which is then immediately reflected back and executed in the user’s browser. **e.g., via url parameter** | 
| DOM - TBD | 

# XSS Contexts? 

| By type of context e.g., code specific /urls| 
| ------------- |
| **HTML attributes:** When user input is improperly sanitized and used as an attribute value in HTML tags, an attacker can inject malicious scripts that execute when the attribute is triggered, like an “onclick” or “onmouseover” event.| 
| **JavaScript:** When user input is directly inserted into JavaScript code, it can lead to XSS vulnerabilities. For example, an attacker could exploit a vulnerable script that uses user input as part of a “document.write()” function.  **Examples:** **Generic:** Payloads from the general.js file are launched on all tags. **AngularJS:** Payloads from angular.js are launched on detected templates. **Script:** Payloads from script.js in injected in all possible content. **Link:** Payloads from link.js are launched for all href a tags.| 
| **URL parameters:** If user input is not properly sanitized before being used in URL parameters, attackers can inject malicious scripts that execute when the URL is loaded. | 

# Common Security Measures

| Common web app security measures | 
| ------------- |
| Web app targets may use security measures such as (encoding of characters) = this makes it difficult to use pre-defined payloads where specific chars may be encoded, not resulting in successful payload exec. or (filtering) | 
| Using alternative encoding may cause the application to interpret the characters as harmless text, while the browser still renders it as executable code.| 

# Advanced Evasion Techniques

| Ideas what to do to successfully attempt exec payload on security measures in place | 
| ------------- |
| Bypassing XSS filters: Some web applications implement filters to block known XSS payloads. To bypass these filters, you may need to use less common payloads, encode characters differently, or split the payload into parts. For example, instead of using <script>, you can try <scr<script>ipt>. | 
| Bypass encodings: Some applications may filter or encode characters like <, >, and “. Experiment with different encodings (e.g., &#60; for <) or alternative characters (e.g., using backticks instead of quotes) to bypass these filters.| 


# Where to test for xss? - Any user input area

| Examples| 
| ------------- |
| STORED XSS best at : comment sections(blogs, cms comment area)| 
| REFLECTED XSS best at: search bars | 
| REFLECTED ORSTORED XSS best at: input (registration, subscription, etc) forms| 
| REFLECTED XSS best at: parameteres in the urls where you have x="value" test on value| 


# Payloads / Cheat Sheets 

| Examples| 
| ------------- |                                                                                                                                             
| https://portswigger.net/web-security/cross-site-scripting/cheat-sheet| 
                                                                                                                                                

                                                                                                                                                
# Payloads from submissions

| Other users tested successful| 
| ------------- |
|##[Click here](javascript:alert(1))##|
|##"> <img src=x onerror=alert(document.domain)>##|  
                                                                                                                                                
                                                                                                                                                
                                                                                                                                                
# Identify indexable user input areas via Google Dorks

| Examples query for site:*.domain.com| 
| ------------- |
| "leave a comment" -sign in or with sign in| 
| "search" OR "find" -www|                                                                                                                                     | inurl:"search" OR .php? | 
                                                                                                                                                
 

# Identify indexable user input areas via scripts / automation

| Examples of tools for automatic assessment of xss| 
| ------------- |
| XSS RADAR https://github.com/bugbountyforum/XSS-Radar - limited to no urls, doesnt work well | 


# XSS specific to software / CVE

| Software known to allow xss | 
| ------------- |
| TBD| 

# Escalate XSS further to:

| Other attacks e.g.,| 
| ------------- |
|RCE https://www.bugcrowd.com/blog/the-ultimate-guide-to-finding-and-escalating-xss-bugs/  | 
| STEAL SESSION TOKENS| 
| BYPASS SOP (SAME ORIGIN POLICY)| 
| OPEN REDIRECT| 




