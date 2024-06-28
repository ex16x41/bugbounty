
# Cloud AWS Recon & Hacking (s3 only) ;^) 

**You can use this s3 hacking guide for your own bugbounty/work - i tested everything and organized how I like it and how it makes sense to me from workflow pov**

## Step 1 : Get familiar with terms / concepts

| Term | Detail (if available) |
|-----:|---------------:|
|   Bucket | a top-level Amazon S3 folder  |
|   Prefix | a folder in a bucket |
|  Object  | any item inside a bucket |


## OSINT & Active Methods to Identify AWS s3 on Target

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

![image](https://github.com/ex16x41/bugbounty/assets/44981946/f20d3a19-9219-4cbf-917d-a681c46e7e6b)



## Important notes on access related actions to public or "semi public" buckets

| Note | Detail (if available) |
|-----:|---------------:|
| To access the bucket you can try from web (browser) navigate and open in URL the target bucket instance | this can look like in the format of amazonaws domain like [bucket].s3.amazonaws OR s3.amazonaws/[bucket] OR subdomain.targetdomain.tld | 
| to access via aws cli | you can use command aws s3 ls s3://bucket to list all contents including --no-sign-request at the end of the command, because otherwise some buckets due to config may present 'accessdenied' or 'nosuchbucket' - but with the '--no-sign-request' it may in a sense bypass that | 
|   https://github.com/redhuntlabs/BucketLoot | Bucket inspector that can help users extract assets, flag secret exposures and even search for custom keywords as well as Regular Expressions from publicly-exposed storage buckets by scanning files that store data in plain-text.  |



## AWS CLI S3 Enumeration & Exploitation Commands

| Command | Detail (if available) |
|-----:|---------------:|
|   Bucket | List and read contents of bucket  |
|   Prefix | a folder in a bucket |
|  Object  | any item inside a bucket |


## AWS CLI IAM Enumeration & Exploitation Commands

| Command | Detail (if available) |
|-----:|---------------:|
|   Bucket | a top-level Amazon S3 folder  |
|   Prefix | a folder in a bucket |
|  Object  | any item inside a bucket |


## AWS CLI ID Exploitation Commands (Get Keys)

| Command | Detail (if available) |
|-----:|---------------:|
|   Bucket | a top-level Amazon S3 folder  |
|   Prefix | a folder in a bucket |
|  Object  | any item inside a bucket |
















## Permissions Abuse Testing 

Fun fact: most permission misconfigurations happen because bucket owner configure the buckets using manual config. 
"if you need to grant write access for this grantee (anyone with aws acc or public), you can use the AWS CLI, AWS SDK, or the Amazon S3 REST API. " 
## CASE1: configured read access to aws accounts
* If internally the bucket permissions enabled only to AWS users then cannot use --no-sign-request (will not work, must use creds config'd in cli)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/40768724-0de8-4bcf-9713-cb1c59e9b5da)


test reading acl 

![image](https://github.com/ex16x41/bugbounty/assets/44981946/e2dad919-eb6f-413a-ae7a-406501fbb899)


The unique ID numbers associated with AWS entities, such as owners or grantees, are internal identifiers used by AWS for tracking and managing permissions. These IDs alone do not provide any direct means to bypass permissions or launch attacks.

with --no-sign-request does not work because of configuration 

![image](https://github.com/ex16x41/bugbounty/assets/44981946/cf5a21f5-e028-4448-ab68-3a07004d0423)


this one is used to enumerate the contents of your bucket and gather information about the exposed files and directories.

![image](https://github.com/ex16x41/bugbounty/assets/44981946/85f2fff8-9184-4fce-bac3-62186716cd91)


## CASE2: configured read access to everyone (public)
* If internally the bucket permissions enabled only to everyone (all public) users then can use --no-sign-request and with creds also

![image](https://github.com/ex16x41/bugbounty/assets/44981946/14da7b3a-c6fd-42bf-949d-27b895ed029e)


The actions and commands that are successfully executed epend entirely on the configuration of permissions, for example this setting is configured to everyone allowed to list but not read ACP

![image](https://github.com/ex16x41/bugbounty/assets/44981946/291331c2-762d-42aa-ac24-70e4e9664ccf)



this is why when attempting a read of acp (policy) we dont get access 

![image](https://github.com/ex16x41/bugbounty/assets/44981946/5f075d0f-e117-4ecb-adb5-1ee922c39324)


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

![image](https://github.com/ex16x41/bugbounty/assets/44981946/386f6eec-62b5-49dc-a46c-094eff6ed1b6)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/e85e78ed-ca71-401c-9ce5-931d5d9d1f2b)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/67d2eecb-6a8b-46c9-8e4e-c8852108ed73)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/fb673ad2-1bfb-4e1f-83ff-13bb8c5ff29e)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/2f13e7ee-13cb-4bf1-9964-797e727f32cc)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/18ff1b85-ea72-4f21-9936-07161360cd26)




# First let's understand how s3 buckets look like in real life? we have multiple scenarios

**example URL one (here the url format is targetbucket.amazon)** here to read bucket we would do s3://divvy-tripdata

![image](https://github.com/ex16x41/bugbounty/assets/44981946/fc44f23e-0afb-4dfa-ad9a-2da9f3ac3ac9)



**example URL two (here the url format is amazon.targetbucket)** here to read bucket we would do s3://capitalbikeshare-data

![image](https://github.com/ex16x41/bugbounty/assets/44981946/0b4bdcdf-4cdf-4c1b-8c6a-e67005464dae)




**example URL three (here the domain is not revealing the bucket directly, but instead under name tags that differ)** here to read bucket we would do s3://dpa-prd

![image](https://github.com/ex16x41/bugbounty/assets/44981946/572c8421-cd1b-415b-a580-ea3cfc926aad)



**example URL four (here the name of the subdomain and bucket name match)** here to read bucket we would do s3://flaws-cloud

![image](https://github.com/ex16x41/bugbounty/assets/44981946/d15189e3-646b-4b7a-914a-c2c5f189892a)





## Misconfiguration Types to look for

| Method | Detail if available|
|-----:|---------------:|
| Public access (completely external) | One of the most common issues is when S3 buckets are set to public access, meaning that anyone on the internet can access the contents of the bucket. This can happen if the bucket is created with default settings or if the access control list (ACL) is misconfigured. !!!!! note public access config has various levels to it depending on permissions (read,write,delete)  |
| Overly permissive IAM policies (req some lvl of access) | AWS Identity and Access Management (IAM) allows you to control access to your AWS resources. If IAM policies are too permissive, users may have more access than they need, potentially allowing them to access S3 buckets that they shouldn't be able to.  |
|  Misconfigured bucket policies (external testing) | S3 bucket policies define the permissions for a bucket, including who can access it and what they can do with its contents. If these policies are misconfigured or too permissive, attackers may be able to gain unauthorized access to sensitive data. ALSO --- !!!! An attacker can try to access the bucket through AWS Management Console, AWS CLI, or other tools. If the bucket is misconfigured, the attacker can access its contents directly. If not accessible, the attacker can exploit misconfigured bucket policies using tools like Pacu to find and exploit IAM policy vulnerabilities. Once access is gained, the attacker can read, modify, or delete the bucket's contents, resulting in the theft of sensitive data, insertion of malware or backdoors, or other malicious activity.  |
|   Lack of encryption | If data stored in S3 buckets is not encrypted, it may be vulnerable to interception or theft. S3 supports several types of encryption, including server-side encryption and client-side encryption. |
|Insecure pre-signed URLs | S3 allows users to generate pre-signed URLs that grant temporary access to specific objects or resources. If these URLs are leaked or improperly secured, attackers may be able to use them to access sensitive data.|  
|Cross-origin resource sharing (CORS) misconfiguration | If CORS settings are misconfigured, attackers may be able to bypass same-origin policy protections and access data stored in S3 buckets.|  

# Interesting file types to look for in s3 

![image](https://github.com/ex16x41/bugbounty/assets/44981946/fbe3e7f4-89b1-4d09-bea0-48483c48e532)

PS1, XML, TXT, CSV


AWS S3 comes equipped with a range of permissions and access control mechanisms which if in the case overlooked by administrators and improperly implemented can act as a treasure of data

Misconfigured AWS S3 buckets that leave unauthorized access are thus abused by attackers to compromise the privacy of the data stored in those buckets breaching the privacy of millions of users around the world. If the case misconfigured S3 Bucket contains EC2 snapshot instances, then attackers might be able to retrieve the snapshot instance and then get security keys for the EC2 instance itself. 


# public access abuse case 1 

**access from web gives "nosuchkey", but with --no-sign-request it works** 
![image](https://github.com/ex16x41/bugbounty/assets/44981946/afd0df70-39d5-4322-a1a5-74028401f187)
![image](https://github.com/ex16x41/bugbounty/assets/44981946/9d87809b-e761-4f9e-875f-af42a87f1c94)


# "priv esc" case study 

**find file with admin creds, login, access further folders/files that were otherwise restricted** 
found admin keys

![image](https://github.com/ex16x41/bugbounty/assets/44981946/c5f53c34-b5bb-4e0f-a917-ad12de0e7b65)


aws configure (auth with admin keys)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/5f44146b-a4c6-4673-96c4-2fd556497804)


ls admin folder + contents (that wasnt accessible as --no-sign-request) 

![image](https://github.com/ex16x41/bugbounty/assets/44981946/6511db37-76d0-42c3-957f-153f48dcd0dd)



# 404 no such bucket to subdomain takeover

developer delete s3 bucket but not delete cname pointing to that s3 bucket

![image](https://github.com/ex16x41/bugbounty/assets/44981946/6f3fb260-489f-4fd1-b587-98b7036684be)

use this https://github.com/EdOverflow/can-i-take-over-xyz?source=post_page-----81a68823af74-------------------------------- 

    Go to S3 panel
    Click Create Bucket
    Set Bucket name to source domain name (i.e., the domain you want to take over from error)
    Click Next multiple times to finish
    Open the created bucket
    Click Upload
    Select the file which will be used for PoC (HTML or TXT file). I recommend naming it differently than index.html; you can use poc (without extension)
    In Permissions tab select Grant public read access to this object(s)
    After upload, select the file and click More -> Change metadata
    Click Add metadata, select Content-Type and value should reflect the type of document. If HTML, choose text/html, etc.
    (Optional) If the bucket was configured as a website
    Switch to Properties tab
    Click Static website hosting
    Select Use this bucket to host a website
    As an index, choose the file that you uploaded
    Click Save


# exploit EBS snapshots by AWS acc ID 

https://github.com/WeAreCloudar/s3-account-search/

issue the command python3 -m pip install s3-account-search to install the tool s3-account-search. Next we need to provide the Amazon Resource Name (ARN) of the role under our control (i.e. in our own AWS account), as well as a target S3 bucket in the AWS account whose ID we want to enumerate.

![image](https://github.com/ex16x41/bugbounty/assets/44981946/ff25e10b-135e-4952-9a9e-a8990c683c9e)

writeable (upload malicious poc file)
![image](https://github.com/ex16x41/bugbounty/assets/44981946/3e485e0b-9330-4ab4-b42a-c8e8e91e6755)


TO ADD: 
IAM abuse cases 
add from 
https://cloud.hacktricks.xyz/pentesting-cloud/aws-security/aws-unauthenticated-enum-access/aws-iam-and-sts-unauthenticated-enum 
+ 
https://github.com/RhinoSecurityLabs/Security-Research/tree/master/tools/aws-pentest-tools

# commands to run tests with

**list contents of bucket aws** s3 ls s3://bucket --no-sign-request

**recsuisively list files** aws s3 ls s3://bucket --no-sign-request --recursive

**download files test** aws s3 cp s3://bucket/folder/file . --no-sign-request

**upload file test permissions** aws s3 cp localfile s3://[name_of_bucket]/test_file.txt –-no-sign-request

to list dirs close with /dir/

good to test --recrusive if there is folder forbidden for ls 

curl -I https://s3.amazonaws.com/bucket - this will show region configured in this bucket

Identify overly permissive policies (e.g., Action set to "*")

If you go to URL to see bucket content at root domain like bucket.amazon.com/ (ensure there is no double // because that will show 'nosuchbucket')





# Read access control list

At bucket, level allows to read the bucket’s Access Control List and at the object level allows to read the object’s Access Control List. Read ACL can be tested with the AWS command line using the following command

aws s3api get-bucket-acl --bucket [bucketname] --no-sign

aws s3api get-object-acl --bucket [bucketname] --key index.html --no-sign-request




**notes:**
some buckets will allow ls using --no-sign-request but will not allow download of files from it (forbidden) 










LABS to practice 

https://pwnedlabs.io/dashboard 
