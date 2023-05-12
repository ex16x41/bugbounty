# Where to dig thru? - medium/high/critical - low hangin fruit 
JS files, HTML source code (comments, hrefs), function calls, API documentation, Configuration files, Server responses (errors, debug), 

# ENDPOINST : How endpoints may be hiding ;^)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/e10c0188-5af3-484e-b953-b5fee7cd0b72)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/77462f2f-a5ba-4a1e-921a-265bbd605080)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/948f1aee-3a68-41bd-b32a-05919b8b19d2)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/d8a27130-eb3e-4668-b215-19d56de98336)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/cd452fdd-b069-4f05-a366-82155c8b295a)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/6c0a0a61-f853-4800-b8a3-c645332ee09d)

## What else to look for on the high level: 
| type |
|:---:|
| HTML/ JS sinks |
|hidden parameters|


# What data to look for for ?!

| type |
|:---:|
| sensitive file paths |
|database information| 
|API keys| 
|auth tokens| 
|config data| 
|debug info| 
|func names| 
|aws keys - js files|
|firebase urls - js files |
| json file in js file|
|s3 buckets in js ref| 
|secrets| 
|paths|
|ip addrs| 
|file upload field in js ref|
|URLs, domains, etc which can cause possible exploits|
|Potential wildcard entries|
|outdated or old frameworks with known vulnerabilities.|


## TIP :

The types of JavaScript files that may include hidden endpoints can vary, but commonly they include files related to AJAX requests, API integrations, user authentication, and data storage or retrieval. These files may be named in a way that suggests their purpose, such as "api.js", "ajax.js", "auth.js", or "data.js", but not necessarry


# Tools enum & crawl thru js urls

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





reading stuff 

https://pravinponnusamy.medium.com/find-the-treasure-hidden-in-javascript-546827e1a4e2 

https://thehackerish.com/javascript-enumeration-for-bug-bounty-hunters/
