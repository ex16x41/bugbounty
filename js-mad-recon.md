# Where to dig thru? - medium/high/critical - low hangin fruit 
JS files, HTML source code (comments, hrefs), function calls, API documentation, Configuration files, Server responses (errors, debug), 

# Endpoints: how may be hidden ;^)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/e10c0188-5af3-484e-b953-b5fee7cd0b72)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/77462f2f-a5ba-4a1e-921a-265bbd605080)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/948f1aee-3a68-41bd-b32a-05919b8b19d2)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/d8a27130-eb3e-4668-b215-19d56de98336)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/cd452fdd-b069-4f05-a366-82155c8b295a)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/6c0a0a61-f853-4800-b8a3-c645332ee09d)

## What else to look for on the high level: 
| type |about |
|:---:|:---:|
|JS sinks |JavaScript sinks refer to functions or APIs that are used to receive data from user input or external sources without proper validation or sanitization, making them vulnerable to attacks such as XSS (Cross-site scripting). Examples of JavaScript sinks include document.write(), innerHTML, and eval(). | 
|HTML sinks| HTML sinks refer to HTML attributes that accept input from user or external sources without proper validation or sanitization, making them vulnerable to attacks such as XSS. Examples of HTML sinks include src, href, and onclick attributes. |
|hidden params|

## JS SINK SAMPLE
![image](https://github.com/ex16x41/bugbounty/assets/44981946/bc255539-ed34-401e-8209-caf7bed11ffa)

In this example, prompt() is a JavaScript source that receives user input, and document.write() is a sink that displays the user input on the page without proper validation or sanitization, making it vulnerable to XSS attacks.

## HTML SINK SAMPLE

![image](https://github.com/ex16x41/bugbounty/assets/44981946/444445e3-2ce6-4c81-aded-df457dba7f95)

In this example, the href attribute is an HTML sink that executes a JavaScript code when the link is clicked. The code is vulnerable to XSS attacks because it displays the contents of the document.cookie object without proper validation or sanitization.

# be on the lookout for:

| type | value |
|:---:|:---:|
|Sensitive data|database information| 
|Sensitive data|API keys| 
|Sensitive data|auth tokens| 
|Sensitive data|config data| 
|Sensitive data|debug info| 
|Sensitive data|func names| 
|Sensitive data|aws keys - js files|
|Sensitive data|firebase urls - js files |
|Sensitive data| json file in js file|
|Sensitive data|s3 buckets in js ref| 
|Sensitive data|secrets| 
|Other|paths|
|Other|ip addrs| 
|Other|file upload field in js ref|
|Other|URLs, domains, etc which can cause possible exploits|
|Other|Potential wildcard entries|
|Other|outdated or old frameworks with known vulnerabilities.|


## TIP :

The types of JavaScript files that may include hidden endpoints can vary, but commonly they include files related to AJAX requests, API integrations, user authentication, and data storage or retrieval. These files may be named in a way that suggests their purpose, such as "api.js", "ajax.js", "auth.js", or "data.js", but not necessarry

# Tools

Burp Pro > sitemap > filter/engagement tools > find scripts > js 

# Git tools

gau - https://github.com/lc/gau

linkfinder - https://github.com/GerbenJavado/LinkFinder

getSrc - https://github.com/m4ll0k/Bug-Bounty-Toolz/blob/master/getsrc.py

SecretFinder - https://github.com/m4ll0k/SecretFinder

antiburl - https://github.com/tomnomnom/hacks/tree/master/anti-burl

antiburl.py - https://github.com/m4ll0k/Bug-Bounty-Toolz/blob/master/antiburl.py

ffuf - https://github.com/ffuf/ffuf

getJswords.py - https://github.com/m4ll0k/Bug-Bounty-Toolz/blob/master/getjswords.py

BurpSuite - http://portswigger.net/

jsbeautify.py - https://github.com/m4ll0k/Bug-Bounty-Toolz/blob/master/jsbeautify.py

collector.py - https://github.com/m4ll0k/Bug-Bounty-Toolz/blob/master/collector.py

# scripthunter https://github.com/robre/scripthunter 


reading stuff 

https://pravinponnusamy.medium.com/find-the-treasure-hidden-in-javascript-546827e1a4e2 

https://thehackerish.com/javascript-enumeration-for-bug-bounty-hunters/
