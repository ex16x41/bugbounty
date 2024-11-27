api recon 
passive
active 

public apis with or without auth 
auth for public apis will depend on sensitivity of data that is handled 
if public api handles only public data = no need for auth 
in most other instances auth will be required 
public apis meant to be consumed by end users (to facilitate this api providers share documentatiton -> this servers as instruction manual for a given api)
partner apis = meant to be used exclusively by partners of the provider = harder to find if not partner, documentation may be available but limited to partner 
private apis only for private use within an org, documented less than partner apis if at all, if any documentation exists its harder to find = here learn how to reverse eng api req's 


public apis = find apis to attack by discovering the api itself, or api documentation 
if as end user you find api or and api documentation = success

another way to find api is look trough target landing page for links to api or dev portal 


some telling signs you discovered web api : 
in URL naming formats example: 

https://target-name.com/api/v1 

https://api.target-name.com/v1 

https://target-name.com/docs

https://dev.target-name.com/rest

Look for API indicators within directory names like:
/api, /api/v1, /v1, /v2, /v3, /rest, /swagger, /swagger.json, /doc, /docs, /graphql, /graphiql, /altair, /playground

Also, subdomains can also be indicators of web APIs:

api.target-name.com

uat.target-name.com

dev.target-name.com

developer.target-name.com

test.target-name.com


Another indicator of web APIs is the HTTP request and response headers. The use of JSON or XML can be a good indicator that you have discovered an API. 

HTTP Request and Response Headers containing "Content-Type: application/json, application/xml"

 

Also, watch for HTTP Responses that include statements like:
{"message": "Missing Authorization token"}


One of the most obvious indicators of an API would be through information gathered using third-Party Sources like Github and API directories.

Gitub: https://github.com/ 

Postman Explore: https://www.postman.com/explore/apis

ProgrammableWeb API Directory: https://www.programmableweb.com/apis/directory 

APIs Guru: https://apis.guru/ 

Public APIs Github Project: https://github.com/public-apis/public-apis 

RapidAPI Hub: https://rapidapi.com/search/ 

any api endpoints discovered and gathered in passive stage of recon will be used for active recon later 
credential info will help test as auth'd user or admin 
version info will help test for any improper asset mgmt vulns
api documentation will say exactly how to test taregt api 

info on api business purpose can give insight into business logic flaws 

with OSINT (passive recon) you can find API keys, creds, JWT, secrets, leaked PII, sensitive info, etc 

passive recon tools 
git dorks
google dorks
api dirs
wayback 
shodan 


active recon on apis is basically building your api attack surface directly from target 


active recon tools 
nmap -p-
nmap -sC -sV target
amass enum -active -d target | grep api
