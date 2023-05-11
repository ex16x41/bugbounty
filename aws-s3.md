# Discover vuln(ver)/exposed/misconfig'd s3 buckets {My hunting methodlogy}

## Sources for external search (osint only)

1. https://osint.sh/buckets/ - a little better than grayhat because not limited to filtering by filetype (no reg req) 

![image](https://github.com/ex16x41/bugbounty/assets/44981946/ef73ae2b-67e6-4e02-b418-0873517125a1)

2. https://buckets.grayhatwarfare.com/

![image](https://github.com/ex16x41/bugbounty/assets/44981946/f9c53007-c327-4d08-b0cc-3aa520ed650b)


# Internal search - host targeted 

## Identify s3 buckets - passive method 

[x] site:http://s3.amazonaws.com intitle:index.of.bucket

[x] site:http://amazonaws.com inurl:".s3.amazonaws.com/"

[x] site:.s3.amazonaws.com "Company"

[x] intitle:index.of.bucket

[x] site:http://s3.amazonaws.com intitle:Bucket loading

[x] site:*.amazonaws.com inurl:index.html

[x] Bucket Date Modified


## Identify s3 buckets - active method 

| Method | Detail if available|
|-----:|---------------:|
|    HTML inspection & JS files | e.g., " img src="https://s3.amazonaws.com/my-bucket/my-image.jpg" alt="My Image">"     |
|   Network requests  | When a webpage loads, it may make network requests to an S3 bucket to fetch resources such as images, videos, or other files. You can use your browser's developer tools to monitor network requests and look for requests to S3 bucket URLs.  |
|  Cookies  | Some websites may use cookies to store S3 bucket URLs or other sensitive information. You can inspect the cookies of a website using your browser's developer tools or a browser extension such as EditThisCookie.   |
|   Configuration files | If the website is built using a framework or content management system (CMS), it may store S3 bucket URLs or other configuration settings in configuration files such as config.php or settings.ini  |
|Brute-Force | TBD|  
|DNS caching | TBD  |
|Reverse IP lookup (Bing Reverse IP) | TBD  | 
|Tools on GitHub |Lazy S3, bucket_finder, AWS Cred Scanner, sandcastle, Mass3, Dumpster Diver, S3 Bucket Finder, S3Scanner|



## Misconfiguration Types to look for

| Method | Detail if available|
|-----:|---------------:|
| Public access (completely external) | One of the most common issues is when S3 buckets are set to public access, meaning that anyone on the internet can access the contents of the bucket. This can happen if the bucket is created with default settings or if the access control list (ACL) is misconfigured. !!!!! note public access config has various levels to it depending on permissions (read,write,delete)  |
| Overly permissive IAM policies (Some lvl of access) | AWS Identity and Access Management (IAM) allows you to control access to your AWS resources. If IAM policies are too permissive, users may have more access than they need, potentially allowing them to access S3 buckets that they shouldn't be able to.  |
|  Misconfigured bucket policies  | S3 bucket policies define the permissions for a bucket, including who can access it and what they can do with its contents. If these policies are misconfigured or too permissive, attackers may be able to gain unauthorized access to sensitive data.  |
|   Lack of encryption | If data stored in S3 buckets is not encrypted, it may be vulnerable to interception or theft. S3 supports several types of encryption, including server-side encryption and client-side encryption. |
|Insecure pre-signed URLs | S3 allows users to generate pre-signed URLs that grant temporary access to specific objects or resources. If these URLs are leaked or improperly secured, attackers may be able to use them to access sensitive data.|  
|Cross-origin resource sharing (CORS) misconfiguration | If CORS settings are misconfigured, attackers may be able to bypass same-origin policy protections and access data stored in S3 buckets.|  


AWS S3 comes equipped with a range of permissions and access control mechanisms which if in the case overlooked by administrators and improperly implemented can act as a treasure of data

Misconfigured AWS S3 buckets that leave unauthorized access are thus abused by attackers to compromise the privacy of the data stored in those buckets breaching the privacy of millions of users around the world. If the case misconfigured S3 Bucket contains EC2 snapshot instances, then attackers might be able to retrieve the snapshot instance and then get security keys for the EC2 instance itself. 
