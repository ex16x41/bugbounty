You can use this S3 hacking guide for your own work - I tested everything and organized how I like it and how it makes sense to me from a workflow perspective.

OSINT & Active Methods to Identify AWS S3 of a Target IP / Company / Domain

| Method | Detail (if available) |
|-----:|---------------:|
|   Weppalyzer | Identify technologies on target web  |
|    HTML inspection, CSS & JS, files, comments | e.g., " img src="https://s3.amazonaws.com/my-bucket/my-image.jpg" alt="My Image">"  you can also use linkfinder to find endpoints/hyperlinks or use linkgopher   |
|   Network requests  | When a webpage loads, it may make network requests to an S3 bucket to fetch resources such as images, videos, or other files. You can use your browser's developer tools to monitor network requests and look for requests to S3 bucket URLs.  |
|  Cookies  | Some websites may use cookies to store S3 bucket URLs or other sensitive information. You can inspect the cookies of a website using your browser's developer tools or a browser extension such as EditThisCookie.   |
|   Configuration files | If the website is built using a framework or content management system (CMS), it may store S3 bucket URLs or other configuration settings in configuration files such as config.php or settings.ini  |
|enum via Tools on GitHub |Lazy S3, bucket_finder, AWS Cred Scanner, sandcastle, Mass3, Dumpster Diver, S3 Bucket Finder, S3Scanner|
| other tools to enum s3 | https://github.com/sa7mon/S3Scanner , https://github.com/clario-tech/s3-inspector , https://github.com/jordanpotti/AWSBucketDump (Contains a list with potential bucket names) , https://github.com/fellchase/flumberboozle/tree/master/flumberbuckets , https://github.com/smaranchand/bucky , https://github.com/tomdev/teh_s3_bucketeers , https://github.com/RhinoSecurityLabs/Security-Research/tree/master/tools/aws-pentest-tools/s3 , https://github.com/Eilonh/s3crets_scanner , https://github.com/belane/CloudHunter| 
| Content-Security-Policy Response headers | * | 
| Burp Suite | spider > go trough resulst | 
| dig -x | target domain or IP will result in s3-site-us-east-1.amazonaws.com | 
| https://osint.sh/buckets/ | a little better than grayhat because not limited to filtering by filetype (no reg req)  | 
| https://buckets.grayhatwarfare.com/ | * | 
| Google dorks | site:http://s3.amazonaws.com intitle:index.of.bucket, site:http://amazonaws.com inurl:".s3.amazonaws.com/", site:.s3.amazonaws.com "Company" intitle:index.of.bucket, site:http://s3.amazonaws.com intitle:Bucket loading , site:*.amazonaws.com inurl:index.html,  Bucket Date Modified | 

## Visual Examples of all methods above to identify s3 buckets (how it looks like in practice)

**Weppalyzer** 
![image](https://github.com/ex16x41/bugbounty/assets/44981946/19098495-5303-4bad-a3ef-89f6c2a84e7a)

**view source code (S3 Bucket URL hardcoded in HTML of webpage also... in IP addresses too, not only www.domain.com format)**

![image](https://github.com/ex16x41/bugbounty/assets/44981946/6201e729-f33a-49d3-9ca9-2c0faf00f009)

**inspect network traffic - see server GET requests** (can filter keyword as per usual url formats)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/dc6aec45-de04-4d4c-9409-5293fd4458dd)

**s3 in robots.txt (or generally ext:txt)** 

![image](https://github.com/ex16x41/bugbounty/assets/44981946/23700247-f462-4cac-b68c-b2e1f09ad355)

**.json files** 

![image](https://github.com/ex16x41/bugbounty/assets/44981946/5bde726a-f059-4143-9ec1-bfe412b04f31)

**Google dorking** 

![image](https://github.com/ex16x41/bugbounty/assets/44981946/b895255e-7013-4a32-89a2-12f6b87831c6)

**using LeakIX premium plugins + query leaks find buckets + access keys** 

![image](https://github.com/ex16x41/bugbounty/assets/44981946/28696147-705f-422f-a194-c053e0057625)

**shoan or censys , fofa, zoomeye with similar query, changed region** 

![image](https://github.com/ex16x41/bugbounty/assets/44981946/6f86fc9a-af4a-49a4-b319-49f86324eebf)


# S3 buckets IRL:

**example URL one (here the url format is targetbucket.amazon)** here to read bucket we would do s3://divvy-tripdata

![image](https://github.com/ex16x41/bugbounty/assets/44981946/fc44f23e-0afb-4dfa-ad9a-2da9f3ac3ac9)


**example URL two (here the url format is amazon.targetbucket)** here to read bucket we would do s3://capitalbikeshare-data

![image](https://github.com/ex16x41/bugbounty/assets/44981946/0b4bdcdf-4cdf-4c1b-8c6a-e67005464dae)


**example URL three (here the domain is not revealing the bucket directly, but instead under name tags that differ)** here to read bucket we would do s3://dpa-prd

![image](https://github.com/ex16x41/bugbounty/assets/44981946/572c8421-cd1b-415b-a580-ea3cfc926aad)


**example URL four (here the name of the subdomain and bucket name match)** here to read bucket we would do s3://flaws-cloud

![image](https://github.com/ex16x41/bugbounty/assets/44981946/d15189e3-646b-4b7a-914a-c2c5f189892a)

# Interesting file types to look for in s3
|filetype|
|-----:|
|PS1 |
|XML|
|TXT|
|CSV|
|XLSX|
|TF|

