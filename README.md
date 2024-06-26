# Cloud AWS Recon & Hacking (s3) ;^)  -if you find bugs using this rep, credit <3


# Understanding S3 from the inside (for bugbounty)

I have not seen anything as comprehensive as this, therefore I created this guide, on everything from a to z about s3 hacking and understanding how it works, the commands we try and why some work some don't. enjoy.



# First let's identify how s3 buckets look like in real life? we have multiple scenarios

**example URL one (here the url format is targetbucket.amazon)**

![image](https://github.com/ex16x41/bugbounty/assets/44981946/fc44f23e-0afb-4dfa-ad9a-2da9f3ac3ac9)



**example URL two (here the url format is amazon.targetbucket)**

![image](https://github.com/ex16x41/bugbounty/assets/44981946/0b4bdcdf-4cdf-4c1b-8c6a-e67005464dae)




**example URL three (here the domain is not revealing the bucket directly, but instead under name tags that differ)**

![image](https://github.com/ex16x41/bugbounty/assets/44981946/572c8421-cd1b-415b-a580-ea3cfc926aad)



**example URL four (here the name of the subdomain and bucket name match)** 

![image](https://github.com/ex16x41/bugbounty/assets/44981946/d15189e3-646b-4b7a-914a-c2c5f189892a)



# How and where to find buckets directly on target? manually

**view source code (S3 Bucket URL hardcoded in HTML of webpage)**

![image](https://github.com/ex16x41/bugbounty/assets/44981946/6201e729-f33a-49d3-9ca9-2c0faf00f009)

**inspect network traffic - see server GET requests** (can filter keyword as per usual url formats)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/dc6aec45-de04-4d4c-9409-5293fd4458dd)

# other methods to find s3 buckets 

**reverse IP lookup** 

**3rd party sites like git rep/code**

**bruteforce** 


# Find s3 buckets using tools 

https://github.com/nahamsec/lazys3/ 


## Understanding terms 


    Bucket – basically, a top-level Amazon S3 folder.

    Prefix – basically, a folder in a bucket.

    Object – basically, any item inside a bucket.
    
 ## Configuring S3 bucket securely consists of 3 major categories. 

    IAM roles creation and Assignment 

    Public and Private availability with Read / Write access in Bucket policies 

    Access Control lists 


## Permissions Abuse Testing 

Fun fact: most permission misconfigurations happen because bucket owner configure the buckets using manual config. 
"if you need to grant write access for this grantee (anyone with aws acc or public), you can use the AWS CLI, AWS SDK, or the Amazon S3 REST API. " 
## CASE1: configured read access to aws accounts
* If internally the bucket permissions enabled only to AWS users then cannot use --no-sign-request (will not work, must use creds config'd in cli)

![image](https://github.com/ex16x41/OSINT-mine/assets/44981946/153094c1-fd57-4134-994b-9ea9e9ca1fc9)

test reading acl 

![image](https://github.com/ex16x41/OSINT-mine/assets/44981946/9e9c062a-c449-4acd-8f0b-c55e31a98553)

The unique ID numbers associated with AWS entities, such as owners or grantees, are internal identifiers used by AWS for tracking and managing permissions. These IDs alone do not provide any direct means to bypass permissions or launch attacks.

with --no-sign-request does not work because of configuration 

![image](https://github.com/ex16x41/OSINT-mine/assets/44981946/2a5fa2aa-6c05-41bd-8aa5-22d9e665ab13)

this one is used to enumerate the contents of your bucket and gather information about the exposed files and directories.

![image](https://github.com/ex16x41/OSINT-mine/assets/44981946/c04d4713-789e-4dab-9c76-d020912dc500)

## CASE2: configured read access to everyone (public)
* If internally the bucket permissions enabled only to everyone (all public) users then can use --no-sign-request and with creds also

![image](https://github.com/ex16x41/OSINT-mine/assets/44981946/e9144253-1433-402f-a157-9b0ca48efbe1)

The actions and commands that are successfully executed epend entirely on the configuration of permissions, for example this setting is configured to everyone allowed to list but not read ACP
![image](https://github.com/ex16x41/OSINT-mine/assets/44981946/59531fb7-6224-4e6f-9ec3-d7e709839510)

this is why when attempting a read of acp (policy) we dont get access 
![image](https://github.com/ex16x41/OSINT-mine/assets/44981946/43f913a9-15c8-415f-aeda-cf6db032e6b6)

# Information stored in logs during upload/download/access 

The server access logs in Amazon S3 typically include the following information:

    Bucket and Object: The name of the bucket and the key (path) of the object accessed.
    Requester: The Amazon S3 requester, which can be an AWS account or an anonymous user.
    Request Time: The timestamp of the request.
    Request Action: The type of action performed, such as GET, PUT, DELETE, etc.
    Requester IP Address: The IP address of the requester making the request.
    Response Status and Bytes Sent: The HTTP status code of the response and the number of bytes sent.

    Enumeration: Hackers may use AWS CLI commands like aws s3 ls or aws s3api list-objects to enumerate the contents of your bucket and gather information about the exposed files and directories.

    Access and Download: If your S3 bucket has public read access, hackers can use AWS CLI commands such as aws s3 cp or aws s3 sync to download the files from the bucket to their local system.

    Upload or Modify Objects: If the bucket has public write access or allows unauthorized uploads, hackers may use commands like aws s3 cp or aws s3 sync to upload malicious files, overwrite existing files, or modify the content within the bucket.

    Bucket and Object Deletion: In cases where the bucket has misconfigured or weak access control, hackers might attempt to delete or remove objects from the bucket using commands like aws s3 rm.

    ACL and Policy Modification: If the bucket's access control settings are misconfigured, hackers may use AWS CLI commands like aws s3api put-bucket-acl or aws s3api put-bucket-policy to modify the access control lists (ACLs) or bucket policies, granting themselves or others unauthorized access.
    
## Inside view of poorly configured bucket, some things to keep in mind     

![image](https://github.com/ex16x41/OSINT-mine/assets/44981946/801c418d-e029-4a4c-8df6-79d5ca8259cf)

![image](https://github.com/ex16x41/OSINT-mine/assets/44981946/324ca66f-6db1-4bc7-8d4e-40ba852fe9ef)

![image](https://github.com/ex16x41/OSINT-mine/assets/44981946/4f04ca00-a5a7-46e2-bde5-2dff5c1d2582)

![image](https://github.com/ex16x41/OSINT-mine/assets/44981946/241876d1-629d-49e6-9c2c-56d745009c41)

![image](https://github.com/ex16x41/OSINT-mine/assets/44981946/f4557965-4ea5-48b2-ad49-a3b3fc202306)

![image](https://github.com/ex16x41/OSINT-mine/assets/44981946/df0ce2a5-e994-4dbd-8121-c966c25a1256)

![image](https://github.com/ex16x41/OSINT-mine/assets/44981946/bda254aa-0495-4858-8a1d-257e8b57d6d5)

![image](https://github.com/ex16x41/OSINT-mine/assets/44981946/48a253af-eed6-40f6-93c2-b55fb7f7c50d)

![image](https://github.com/ex16x41/OSINT-mine/assets/44981946/efb39c3c-2634-4853-986f-dae6b6ad714c)



## Step 1 -  dig for buckets manually

| Method | Detail if available|
|-----:|---------------:|
|    HTML inspection, CSS & JS files, comments | e.g., " img src="https://s3.amazonaws.com/my-bucket/my-image.jpg" alt="My Image">"     |
|   Network requests  | When a webpage loads, it may make network requests to an S3 bucket to fetch resources such as images, videos, or other files. You can use your browser's developer tools to monitor network requests and look for requests to S3 bucket URLs.  |
|  Cookies  | Some websites may use cookies to store S3 bucket URLs or other sensitive information. You can inspect the cookies of a website using your browser's developer tools or a browser extension such as EditThisCookie.   |
|   Configuration files | If the website is built using a framework or content management system (CMS), it may store S3 bucket URLs or other configuration settings in configuration files such as config.php or settings.ini  |
|Tools on GitHub |Lazy S3, bucket_finder, AWS Cred Scanner, sandcastle, Mass3, Dumpster Diver, S3 Bucket Finder, S3Scanner|


## Misconfiguration Types to look for

| Method | Detail if available|
|-----:|---------------:|
| Public access (completely external) | One of the most common issues is when S3 buckets are set to public access, meaning that anyone on the internet can access the contents of the bucket. This can happen if the bucket is created with default settings or if the access control list (ACL) is misconfigured. !!!!! note public access config has various levels to it depending on permissions (read,write,delete)  |
| Overly permissive IAM policies (req some lvl of access) | AWS Identity and Access Management (IAM) allows you to control access to your AWS resources. If IAM policies are too permissive, users may have more access than they need, potentially allowing them to access S3 buckets that they shouldn't be able to.  |
|  Misconfigured bucket policies (external testing) | S3 bucket policies define the permissions for a bucket, including who can access it and what they can do with its contents. If these policies are misconfigured or too permissive, attackers may be able to gain unauthorized access to sensitive data. ALSO --- !!!! An attacker can try to access the bucket through AWS Management Console, AWS CLI, or other tools. If the bucket is misconfigured, the attacker can access its contents directly. If not accessible, the attacker can exploit misconfigured bucket policies using tools like Pacu to find and exploit IAM policy vulnerabilities. Once access is gained, the attacker can read, modify, or delete the bucket's contents, resulting in the theft of sensitive data, insertion of malware or backdoors, or other malicious activity.  |
|   Lack of encryption | If data stored in S3 buckets is not encrypted, it may be vulnerable to interception or theft. S3 supports several types of encryption, including server-side encryption and client-side encryption. |
|Insecure pre-signed URLs | S3 allows users to generate pre-signed URLs that grant temporary access to specific objects or resources. If these URLs are leaked or improperly secured, attackers may be able to use them to access sensitive data.|  
|Cross-origin resource sharing (CORS) misconfiguration | If CORS settings are misconfigured, attackers may be able to bypass same-origin policy protections and access data stored in S3 buckets.|  


AWS S3 comes equipped with a range of permissions and access control mechanisms which if in the case overlooked by administrators and improperly implemented can act as a treasure of data

Misconfigured AWS S3 buckets that leave unauthorized access are thus abused by attackers to compromise the privacy of the data stored in those buckets breaching the privacy of millions of users around the world. If the case misconfigured S3 Bucket contains EC2 snapshot instances, then attackers might be able to retrieve the snapshot instance and then get security keys for the EC2 instance itself. 


# Discover vuln/exposed/misconfig'd s3 buckets

## Sources for external search (osint only)

1. https://osint.sh/buckets/ - a little better than grayhat because not limited to filtering by filetype (no reg req) 

![image](https://github.com/ex16x41/bugbounty/assets/44981946/ef73ae2b-67e6-4e02-b418-0873517125a1)

2. https://buckets.grayhatwarfare.com/

![image](https://github.com/ex16x41/bugbounty/assets/44981946/f9c53007-c327-4d08-b0cc-3aa520ed650b)




# commands to run tests with

**list contents of bucket aws** s3 ls s3://bucket --no-sign-request

**recsuisively list files** aws s3 ls s3://bucket --no-sign-request --recursive

**download files test** aws s3 cp s3://bucket/folder/file . --no-sign-request

**upload file test permissions** aws s3 cp localfile s3://[name_of_bucket]/test_file.txt –-no-sign-request

to list dirs close with /dir/

good to test --recrusive if there is folder forbidden for ls 

curl -I https://s3.amazonaws.com/bucket - this will show region configured in this bucket

Identify overly permissive policies (e.g., Action set to "*")





# Read access control list

At bucket, level allows to read the bucket’s Access Control List and at the object level allows to read the object’s Access Control List. Read ACL can be tested with the AWS command line using the following command

aws s3api get-bucket-acl --bucket [bucketname] --no-sign

aws s3api get-object-acl --bucket [bucketname] --key index.html --no-sign-request




**notes:**
some buckets will allow ls using --no-sign-request but will not allow download of files from it (forbidden) 



# Let's talk about non direct recon 

**here we have two options, one is google dorks, another is 3rd party site tools** 

**tools** 
https://buckets.grayhatwarfare.com/ - some paid features 



**dorks:**

site:http://s3.amazonaws.com intitle:index.of.bucket

site:http://amazonaws.com inurl:".s3.amazonaws.com/"

site:.s3.amazonaws.com "Company"

intitle:index.of.bucket

site:http://s3.amazonaws.com intitle:Bucket loading

site:*.amazonaws.com inurl:index.html

Bucket Date Modified
