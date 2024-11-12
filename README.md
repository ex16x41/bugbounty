
# Cloud AWS hacking (Public Repository)

**You can use this s3 hacking guide for your own work - I tested everything and organized how I like it and how it makes sense to me from workflow pov**

## OSINT & Active Methods to Identify AWS s3 of a Target IP / COMANY / DOMAIN

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


# What actions can we do on s3 ?
 
    Enumeration: use AWS CLI commands like aws s3 ls or aws s3api list-objects to enumerate the contents of your bucket and gather information about the exposed files and directories.

    Access and Download: If  S3 bucket has public read access, we can use AWS CLI commands such as aws s3 cp or aws s3 sync to download the files from the bucket to their local system.

    Upload or Modify Objects: If the bucket has public write access or allows unauthorized uploads, we may use commands like aws s3 cp or aws s3 sync to upload malicious files, overwrite existing files, or modify the content within the bucket.

    Bucket and Object Deletion: In cases where the bucket has misconfigured or weak access control, we might attempt to delete or remove objects from the bucket using commands like aws s3 rm.

    ACL and Policy Modification: If the bucket's access control settings are misconfigured, we may use AWS CLI commands like aws s3api put-bucket-acl or aws s3api put-bucket-policy to modify the access control lists (ACLs) or bucket policies, granting themselves or others unauthorized access.


# First let's understand how s3 buckets look like in real life? we have multiple scenarios

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

**visual example of files (filetypes) in bucket**

![image](https://github.com/ex16x41/bugbounty/assets/44981946/fbe3e7f4-89b1-4d09-bea0-48483c48e532)


# Gathered some real life case scenarios of aws s3 attacks

# from nosuchkey to full listing of bucket

**access from web gives "nosuchkey", but with --no-sign-request it works** 
![image](https://github.com/ex16x41/bugbounty/assets/44981946/afd0df70-39d5-4322-a1a5-74028401f187)
![image](https://github.com/ex16x41/bugbounty/assets/44981946/9d87809b-e761-4f9e-875f-af42a87f1c94)


# find access keys in file in bucket, authenticate, escalate

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

# writeable (upload malicious poc file)
![image](https://github.com/ex16x41/bugbounty/assets/44981946/3e485e0b-9330-4ab4-b42a-c8e8e91e6755)

# from ID get access keys 

![image](https://github.com/ex16x41/bugbounty/assets/44981946/fab46b77-d1ea-48fc-b0f3-b88c2b4a64bf)



TO ADD: 
IAM abuse cases 
add from 
https://cloud.hacktricks.xyz/pentesting-cloud/aws-security/aws-unauthenticated-enum-access/aws-iam-and-sts-unauthenticated-enum 
+ 
https://github.com/RhinoSecurityLabs/Security-Research/tree/master/tools/aws-pentest-tools

## AWS CLI IAM Enumeration & Exploitation Commands

| Command | Detail (if available) |
|-----:|---------------:|
|* | * |
| * | * |
|*  | * |


## AWS CLI ID Exploitation Commands (Get Keys)

| Command | Detail (if available) |
|-----:|---------------:|
|* | * |
| * | * |
|*  | * |



## Now let's see how configurations look like form the inside of the aws console (and what leads to abuse of them)


|Notes|
|-----:|
|  If internally the bucket permissions enabled only to AWS users then cannot use --no-sign-request (will not work, must use creds config'd in cli) |


![image](https://github.com/ex16x41/bugbounty/assets/44981946/291331c2-762d-42aa-ac24-70e4e9664ccf)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/40768724-0de8-4bcf-9713-cb1c59e9b5da)


|Notes|
|-----:|
| with --no-sign-request does not work because of configuration  |


![image](https://github.com/ex16x41/bugbounty/assets/44981946/cf5a21f5-e028-4448-ab68-3a07004d0423)

|Notes|
|-----:|
| this one is used to enumerate the contents of your bucket and gather information about the exposed files and directories. | 


![image](https://github.com/ex16x41/bugbounty/assets/44981946/85f2fff8-9184-4fce-bac3-62186716cd91)


|Notes|
|-----:|
| If internally the bucket permissions enabled only to everyone (all public) users then can use --no-sign-request and with creds also | 

![image](https://github.com/ex16x41/bugbounty/assets/44981946/14da7b3a-c6fd-42bf-949d-27b895ed029e)


|Notes|
|-----:|
| The actions and commands that are successfully executed epend entirely on the configuration of permissions, for example this setting is configured to everyone allowed to list but not read ACP, this is why when attempting a read of acp (policy) we dont get access  | 



![image](https://github.com/ex16x41/bugbounty/assets/44981946/5f075d0f-e117-4ecb-adb5-1ee922c39324)



    
    
## More inside view of poor configurations or possible configurations   

![image](https://github.com/ex16x41/bugbounty/assets/44981946/386f6eec-62b5-49dc-a46c-094eff6ed1b6)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/e85e78ed-ca71-401c-9ce5-931d5d9d1f2b)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/67d2eecb-6a8b-46c9-8e4e-c8852108ed73)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/fb673ad2-1bfb-4e1f-83ff-13bb8c5ff29e)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/2f13e7ee-13cb-4bf1-9964-797e727f32cc)

![image](https://github.com/ex16x41/bugbounty/assets/44981946/18ff1b85-ea72-4f21-9936-07161360cd26)





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

## CASE SCENARIOS

# CASE 1
Found IP, this IP from nmap has open port 3000 with description node js express framework, you access via web on this port and see there is site come up, this site in source code shows bucket, you try to access bucket using "aws s3 cp s3://hugelogistics-data" but it doesnt work, you try with "--no-sign-request" it does not work, We might think to just download all the files from the bucket using aws s3 cp s3://hugelogistics-data . --recursive , but this also fails. we then can shift into looking at ACL of the bucket, so we run aws s3api get-bucket-acl --bucket hugelogistics-data, but that fails too. We then want to check if instead of ACL we can try policy, so we run aws s3api get-bucket-policy --bucket hugelogistics-data - and successfully so we get: 
![image](https://github.com/user-attachments/assets/8ea95ed7-40d5-4c49-8f2a-52ee456249f9)
This bucket policy can be summarized as follows:
    Any authenticated AWS user globally can access the ACL and the content of the two specified files (backup.xlsx and background.png) in the hugelogistics-data bucket.
    They can also retrieve the policy of the hugelogistics-data bucket.
Even though we weren't able to list the contents of the bucket, we're still able to leak the contents and access them! Let's transfer the Excel file locally.
we can run this command to download the file exposed from policy to see if it will have more data for us to pivot from using, aws s3 cp s3://hugelogistics-data/backup.xlsx . - > Attempting to open this in LibreOffice or Microsoft Office we're prompted to enter a password. Let's see if we can crack it. First download the Python script office2john.py .  wget https://raw.githubusercontent.com/openwall/john/bleeding-jumbo/run/office2john.py This script takes an Office file as input and creates a hash taking into account the version of the office document. generate a hash of the document that we can subject to an offline brute force attack using this command python3 office2john.py backup.xlsx > hash.txt - Remove the filename backup.xlsx: from the hash and save it. Running the command below we crack the password for the spreadsheet in under two minutes! hashcat -a 0 -m 9600 hash.txt rockyou.txt
![image](https://github.com/user-attachments/assets/72a0ac3a-6b9a-4ffe-b311-f89e992e34fd)
Opening the XSLX file we see table of creds 
![image](https://github.com/user-attachments/assets/9b74b2e4-cae6-4195-9750-e506b10cd505)
this one here mentions CRM.. what makes sense is to go back to site and bruteforce dis on the IP:port for any other logins that unique to CRM based access and use these creds 
![image](https://github.com/user-attachments/assets/d210809f-09c6-4758-8f97-a571426dbff8)
![image](https://github.com/user-attachments/assets/4cc1d208-5e4b-493a-9248-519653454d89)
![image](https://github.com/user-attachments/assets/d32262e0-49c9-413b-aa4b-a0f09430bcf1)
